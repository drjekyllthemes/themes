# Planet Jekyll

Feed list/configuration for [Planet Jekyll](http://planetjekyll.herokuapp.com)

Note: All feeds including the feed lists (that is, [jekyll.ini](jekyll.ini))
get auto-updated (fetched) once a day (that is, every 24 hours).


## Add Your Feed - How To

Step 1: Add your feed to the feed list (that is, [jekyll.ini](jekyll.ini)).

Example:

~~~
[jekyllnews]
  title  = Official Jekyll News
  link   = http://jekyllrb.com/news
  feed   = http://jekyllrb.com/feed.xml
~~~

or

~~~
[parkermoore]
  title  = Parker Moore (Hey, I’m Parker.)
  link   = http://blog.parkermoore.de/categories/jekyll/
  feed   = http://blog.parkermoore.de/categories/jekyll/atom.xml
~~~

Step 2: There's no Step 2 ;-)

That's it. Wait for the next auto-update (max. 24 hours). Welcome on Planet Jekyll.


## Powered by Pluto

Planet Jekyll is powered by the [pluto gem](https://github.com/feedreader).

