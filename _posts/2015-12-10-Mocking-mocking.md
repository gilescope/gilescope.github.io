                                                                                                                                                  |
| Mocking has its place, but many use it everywhere. The secret sauce to testing has almost nothing to do with mocks, and everything to do with...

<!--more-->

Separation of concerns.

Mocking is really useful if you're trying to hide a third party service that you can't substitute any other way.

But if the code is all your own and you are injecting in many mocks you find yourself or anyone else being able to understand the intent of the test 6 months on.

By setting up expectations we reach into the behaviour / implementation of what we're testing to such an extent that any change to the implementation is likely to break the test.

<h3>Mindset</h3>

This high coupling between the tests and the implementations keeps our minds thinking about the implementation.

When we're writing specs, we should be thinking about what we want rather than how to get it.

The best way to understand this mindset is to try it for yourself. Go to the extreme of having the spec in a language separate to the implementation.

Enter the <a title="Gherkin language" href="https://github.com/cucumber/cucumber/wiki/Gherkin">Gherkin</a> language...

By specifying what you want away from the implementation details it puts your head in the right place.

<h3>Taking the mindset on the road</h3>

By using things like <a title="SpecFlow" href="http://www.specflow.org/">SpecFlow</a> you can use Gherkin to specify your tests, but once you've got the idea of the importance of the separation of the spec from the implementation, we can go back and see how we'd structure our tests differently.

In the large I'd argue for having the tests only talking to an exposed API, and that the design of that API is to make testing as easy as possible. I.e. behind that API we hide the test implementation details and we expose a high level 'DSL' that allows our app to be tested.

By separating out our concerns, we have two distinct layers of a test:

Spec/Test                      =&gt; (Testing)API       =&gt; Implementation
(what to test)               (how we test)              (how we implement)

This reduces the tight coupling one gets between tests and implementations, and makes it easier when looking at the tests to specify what you want, rather than how.

By separating out the testing API we effectively create our own testing language (DSL) that allows us to concern ourselves only with what we want tested. |
| Anti-pattern:
IMyInterface x = y as IMyInterface
And then the test code goes on to assume x is not null...

An explicit cast would be better as your stating your expectations more clearly:
IMyInterface x = (IMyInterface) y

And another:

Assert.NotNull(x);
Assert.True(x.Y)

Just skip to:
Assert.True(x.Y)

If there's a null pointer it's not going to take a genius to figure out where it is.                                                                                                                                                   