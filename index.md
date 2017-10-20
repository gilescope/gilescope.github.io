---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: default
---
Welcome

{% for post in site.posts %}	
## [{{ post.title }}]({{post.url}}) {{ post.date | date: "%B %e, %Y" }} {{ post.category }}			
{% endfor %}	


