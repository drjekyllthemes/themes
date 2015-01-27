# Jekyll Quick Reference (Cheat Sheet)

## Commands

### Jekyll

- `build` or `b`
- `serve` or `s`
- `new`
- `docs`
- `doctor`

~~~
$ jekyll new my-site
$ cd my-site
$ jekyll build
$ jekyll serve    # => Browse your site; open the page @ http://localhost:4000
~~~


## Folder Structure

~~~
├── _config.yml
├── _posts             
|   ├── 2015-01-01-week-1-factbook.md  # format => YEAR-MONTH-DAY-TITLE.MARKUP
|   ├── 2015-01-08-week-2-hoe.md
|   └── 2015-01-15-week-3-slideshow.md
├── _drafts                            # upcoming posts; not yet published 
|   ├── week-4-kramdown.md             # note: no date required 
|   └── week-5-feedparser.md
├── _layouts
|   ├── default.html
|   └── post.html
├── _includes
|   ├── footer.html
|   └── header.html
├── _data
|   └── members.csv
├── _books                             # collection
|   ├── ruby-under-a-microscope.md
|   └── learn-ruby-the-hard-way.md
├── _site                              # output build folder; site gets generated here
└── index.html
~~~


## `_posts` Folder

The post file name must follow the format: YEAR-MONTH-DAY-TITLE.MARKUP
(e.g. `2015-01-01-week-1-factbook.md`).
The permalinks can be customized for each post,
but the date and markup language are determined by the file name.

~~~
├── _posts             
|   ├── 2015-01-01-week-1-factbook.md
|   ├── 2015-01-08-week-2-hoe.md
|   └── 2015-01-15-week-3-slideshow.md
~~~

### Front Matter

~~~
---
layout: post
title:  "Week #1 - factbook gem - turn the world factbook into open structured data e.g. JSON"
---
~~~

**Excerpt**

~~~
---
excerpt_separator: <!--more-->
---

Excerpt
<!--more-->
Out-of-excerpt
~~~

**Including images and resources**

~~~
![Ruby under a Microscope Book Cover]({{site.url}}/i/book-ruby-under-a-microscope.png)

[Hoe PDF Booklet](http://docs.seattlerb.org/hoe/Hoe.pdf); 6 Pages
~~~



## _draft Folder

Drafts are unpublished posts without a date.

~~~
|-- _drafts/
|   └── a-draft-post.md
~~~


### _includes Folder

### _layouts Folder

### _data Folder

### _<collection> Folder e.g _albums, _links, etc.


### _config.yml  - Configuration

Example:

~~~
url:   'http://openfootball.github.io'
title: 'football.db - Open Football Data'

exclude: ['README.md']

markdown: 'kramdown'
~~~

Note: Do not use tabs in configuration files (the YAML format forbids tabs; allows only spaces).


- site.title  e.g.


- site.url e.g.


- exclude

Exclude directories and/or files from the conversion.
These exclusions are relative to the site's source directory and cannot be outside the source directory.

~~~
exclude: [DIR, FILE, ...]
~~~



## Liquid Global Variables

~~~
site             -- Sitewide information + configuration settings from  _config.yml.
page             -- Page specific information + the YAML front matter. Custom variables set via the YAML Front Matter will be available here.
content          -- In layout files, the rendered content of the Post or Page being wrapped. Not defined in Post or Page files.
paginator        --  When the paginate configuration option is set, this variable becomes available for use.
~~~

## Liquid Site Variables

~~~
site.time           --  The current time (when you run the jekyll command)
site.pages          --  A list of all Pages
site.posts          --  A reverse chronological list of all Posts
site.related_posts  --  If the page being processed is a Post, this contains a list of up to ten related Posts.
                        By default, these are low quality but fast to compute.
                        For high quality but slow to compute results, run the
                        jekyll command with the --lsi (latent semantic indexing) option.
site.static_files   --  A list of all static files (i.e. files not processed by Jekyll's converters or the Liquid renderer).
                        Each file has three properties:  path, modified_time and extname.
site.html_pages     --  A list of all HTML Pages.
site.collections    --  A list of all the collections.
site.data           --  A list containing the data loaded from the YAML files located in the _data directory.
site.documents      --  A list of all the documents in every collection.

site.categories.CATEGORY   -- The list of all Posts in category CATEGORY.
site.tags.TAG              -- The list of all Posts with tag TAG.
site.[CONFIGURATION_DATA]  -- All the variables set via the command line and your _config.yml
                              are available through the site variable.
                              For example, if you have url: http://mysite.com in your configuration file,
                              then in your Posts and Pages it will be stored in site.url.
                              Jekyll does not parse changes to _config.yml in watch mode,
                              you must restart Jekyll to see changes to variables.
~~~

## Liquid Page Variables

~~~
page.content      --  The content of the Page, rendered or un-rendered depending upon what
                      Liquid is being processedand what page is.
page.title        --  The title of the Page.
page.excerpt      --  The un-rendered excerpt of the Page.
page.url          --  The URL of the Post without the domain, but with a leading slash, e.g. /2008/12/14/my-post.html
page.date         --  The Date assigned to the Post. This can be overridden in a Post’s front matter
                      by specifying a new date/time in the format YYYY-MM-DD HH:MM:SS (assuming UTC),
                      or YYYY-MM-DD HH:MM:SS +/-TTTT
                      (to specify a time zone using an offset from UTC. e.g. 2008-12-14 10:30:00 +0900).
page.id           --  An identifier unique to the Post (useful in RSS feeds). e.g. /2008/12/14/my-post
page.categories   --  The list of categories to which this post belongs.
                      Categories are derived from the directory structure above the _posts directory.
                      For example, a post at /work/code/_posts/2008-12-24-closures.md would have this field
                      set to ['work', 'code']. These can also be specified in the YAML Front Matter.
page.tags         --  The list of tags to which this post belongs. These can be specified in the YAML Front Matter.
page.path         --  The path to the raw post or page. Example usage: Linking back to the page or post’s source on GitHub.
                      This can be overridden in the YAML Front Matter.
page.next         --  The next post relative to the position of the current post in site.posts.
                      Returns nil for the last entry.
page.previous     --  The previous post relative to the position of the current post in site.posts.
                      Returns nil for the first entry.
~~~



## Liquid Template Filters n Tags


### Date, Time Filters

~~~
{{ site.time | date_to_xmlschema }}   2008-11-07T13:07:54-08:00          -- Convert date to XML Schema (ISO 8601) format
{{ site.time | date_to_rfc822 }}      Mon, 07 Nov 2008 13:07:54 -0800    -- Convert date to RFC-822 format
{{ site.time | date_to_string }}      07 Nov 2008                        -- Convert date to short format
{{ site.time | date_to_long_string }} 07 November 2008                   -- Convert date to long format
~~~

### Where, Group By, Sort

~~~
{{ site.members | where:"graduation_year","2014" }}   -- Select all the objects in an array where the key has the given value.
{{ site.members | group_by:"graduation_year" }}       -- Group an array's items by a given property e.g.

  [{"name"=>"2013", "items"=>[...]},
   {"name"=>"2014", "items"=>[...]}]


{{ page.tags | sort }}                    -- Sort an array 
{{ site.posts | sort: 'author' }}         --   Optional arguments for hashes: 1. property name 2. nils order (first or last)
{{ site.pages | sort: 'title', 'last' }}
~~~

### Escape (XML, CGI, URI)

~~~
{{ page.content | xml_escape }}                            -- Escape some text for use in XML
{{ "foo,bar;baz?" | cgi_escape }}   foo%2Cbar%3Bbaz%3F     -- CGI escape a string for use in a URL; replaces any special characters with appropriate %XX replacements
{{ "foo, bar \baz?" | uri_escape }}  foo,%20bar%20%5Cbaz?  -- URI escape a string
~~~


### Convert (markdownify, slugify, sassify, jsonify)

~~~
{{ page.excerpt | markdownify }}        -- Convert a Markdown-formatted string into HTML
{{ some_scss | scssify }}               -- Convert a SCSS-formatted string into CSS
{{ some_sass | sassify }}               -- Convert a Sass-formatted string into CSS
{{ "The _config.yml file" | slugify }}            the-config-yml-file    -- Convert a string into a lowercase URL "slug"
{{ "The _config.yml file" | slugify: 'pretty' }}  the-_config.yml-file   --  option 'pretty': spaces and non-alphanumeric characters except for ._~!$&'()+,;=@
{{ site.data.projects | jsonify }}           -- Convert Hash or Array to JSON
~~~

### Misc

~~~
{{ page.content | number_of_words }}        1337                -- Count the number of words in some text
{{ page.tags | array_to_sentence_string }}  foo, bar, and baz   -- Convert an array into a sentence. Useful for listing tags
~~~

### Include Tag

~~~
{% include footer.html %}                  -- Searches for include file in _includes folder
{% include footer.html param="value" %}    -- You can also pass parameters to an include
{% include_relative somedir/footer.html %} -- Searches for include file relative to the file where the tag is used
~~~

### Code Syntax Highlighting Tag

~~~
{% highlight ruby %}
def main
  puts 'Hello World'
end
{% endhighlight %}
~~~

~~~
{% highlight ruby linenos %}   -- Use line numbers
def main
  puts 'Hello World'
end
{% endhighlight %}
~~~

### Gist Tag

~~~
{% gist parkr/931c1c8d465a04042403 %}
{% gist parkr/931c1c8d465a04042403 jekyll-private-gist.markdown %}  -- You may optionally specify the filename to display
~~~

(Source: see jekyll-gist gem)



## Permalinks

For example, the default date permalink is defined as:

~~~
/:categories/:year/:month/:day/:title.html
~~~

### Template variables

~~~
year        -- Year from the Post’s filename
month       -- Month from the Post’s filename
i_month     -- Month from the Post’s filename without leading zeros.
day         -- Day from the Post’s filename
i_day       -- Day from the Post’s filename without leading zeros.
short_year  -- Year from the Post’s filename without the century.
title       -- Title from the Post’s filename
categories  -- The specified categories for this Post.
               If a post has multiple categories, Jekyll will create a hierarchy
               (e.g. /category1/category2). Also Jekyll automatically parses out double slashes in the URLs,
               so if no categories are present, it will ignore this.
~~~

### Built-in permalink styles

~~~
date      /:categories/:year/:month/:day/:title.html
pretty    /:categories/:year/:month/:day/:title/
none      /:categories/:title.html
~~~


### Permalink style examples

Given a post named: /2009-04-29-slap-chop.md

~~~
None specified (date)             /2009/04/29/slap-chop.html
pretty                            /2009/04/29/slap-chop/index.html
/:month-:day-:year/:title.html    /04-29-2009/slap-chop.html
/blog/:year/:month/:day/:title    /blog/2009/04/29/slap-chop/index.html
~~~


## Templates

### Displaying an index of posts

~~~
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
~~~

### Displaying an index of posts with post excerpts

~~~
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
~~~

### Paginator

~~~
paginator.per_page            --  Number of Posts per page
paginator.posts               --  Posts available for that page
paginator.total_posts         --  Total number of Posts
paginator.total_pages         --  Total number of Pages
paginator.page                --  The number of the current page
paginator.previous_page       --  The number of the previous page
paginator.previous_page_path  --  The path to the previous page
paginator.next_page           --  The number of the next page
paginator.next_page_path      --  The path to the next page
~~~

***Render the paginated Posts***

~~~
{% for post in paginator.posts %}
  <h1><a href="{{ post.url }}">{{ post.title }}</a></h1>
  <p class="author">
    <span class="date">{{ post.date }}</span>
  </p>
  <div class="content">
    {{ post.content }}
  </div>
{% endfor %}

<div class="pagination">
  {% if paginator.previous_page %}
    <a href="{{ paginator.previous_page_path }}" class="previous">Previous</a>
  {% else %}
    <span class="previous">Previous</span>
  {% endif %}
  <span class="page_number ">Page: {{ paginator.page }} of {{ paginator.total_pages }}</span>
  {% if paginator.next_page %}
    <a href="{{ paginator.next_page_path }}" class="next">Next</a>
  {% else %}
    <span class="next ">Next</span>
  {% endif %}
</div>
~~~

