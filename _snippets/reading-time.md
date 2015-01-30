---
layout: snippets
title:  Reading time template
---

To add the reading time (e.g. 3 mins) to your posts include the read_time.html template in your post layout. Example:

~~~
{% include read_time.html %}
~~~

_includes/read_time.html:

~~~
<span class="reading-time" title="Estimated read time">
  {% assign words = content | number_of_words %}
  {% if words < 360 %}
    1 min
  {% else %}
    {{ words | divided_by:180 }} mins
  {% endif %}
</span>
~~~

Note: assumes a reading speed of 180 words per minute (WPM). 

## Sources

- [Jekyll: Reading time without plugins](http://carlosbecker.com/posts/jekyll-reading-time-without-plugins/) by Carlos Becker, Jan 2015
- [Wikipedia: Words per minute](http://en.wikipedia.org/wiki/Words_per_minute)
