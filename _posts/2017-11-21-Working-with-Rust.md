---
layout: default
title:  "Rusty Trees"
date:   2017-10-14 17:29:24 +0100
categories: rust
---

# Working with Trees in Rust

With Tree structures it seems that using normal references (&) or even named lifetimes just don't give you enough flexability (aka you may find it hard to compile :-) ). 
After much nashing of teeth, I moved to using Rc<RefCell<>> for references. The compiler decided that it would be linient on me and let them through.

My treenodes needed to traverse up the tree as well as down. The compiler again decided to assert it's dominance and put its foot down at that point. 
Circular dependencies are best avoided it seems for an easy life. None the less undetered, I fought a rearguard action by backing down a little. 
Instead of my parent being of type Rc<RefCell<>>, I would have an optional weak reference to my parent. This tamed the savage compiler. All was well with the world.

But obviously when all is well with the world, it's time to write some more code and poke the bear. My next mission was a function that would return a list of ancestors. 
Simple enough in python yes, but I like compilers, even pointy ones with sharp teeth. 

If we were doing plain references the function would look like this:n

   fn get_ancestors(&self) -> Vec<&TreeNode> { ... }
 
but I have the scars to prove that Rc<RefCell<>> was a better plan....

   fn get_ancestors(&self) -> Vec<Rc<RefCell>> { ... }

Well the compiler was happy with the return type, but for reasons I won't go into here, I wanted to include the current treenode in the list. Oh woe is me. What I really wanted to do was something like this:

   fn get_ancestors(self: Rc<RefCell<TreeNode>>) { ... }

or maybe

   fn get_ancestors<D>(self: D) 
   where D: DeRef<TreeNode>
   { ... }

but I'm pretty sure Rust doesn't let you do anything like that. Somehow I needed to get my self while it was wrapped up in a Rc<RefCell<>>. Vexed was I. Then the satoshi dropped, it's just not possible in Rust at the moment, but what would be possible is a static function on the struct that I could pass myself into.

   fn get_ancestors(myself: Rc<RefCell<>>) -> Vec<Rc<RefCell>> { ... }

Ideally it would be nice to work with a references without caring too much whether it's a & or a Rc<> or a Arc<>... I belive RFCs are in the works to help a little in this direction, but for now hopefully this will help someone else learning Rust. 


'no one ever said learning Rust was easy, just that it would be good for you...

