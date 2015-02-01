# Jekyll Quick Reference (Cheat Sheet)

## Table of Contents

- Jekyll Commands (`build`, `serve`, ...)
- Folder Structure (`_posts` Folder, `_drafts` Folder, ...)
- Global Variables
- Site Variables
- Page Variable
- Liquid Template Filters n Tags
- Permalinks
- Template Examples (`feed.xml`, ...)
- GitHub Pages (`site.github`, sitemap, ...)
- Octopress Commands (`new`, `new page`, `deploy`, ...)


## Jekyll Commands

```
$ jekyll help

jekyll 2.5.3 -- Jekyll is a blog-aware, static site generator in Ruby

Usage:

  jekyll <subcommand> [options]

Options:
  -s, --source [DIR]  Source directory (defaults to ./)
  -d, --destination [DIR]  Destination directory (defaults to ./_site)
      --safe         Safe mode (defaults to false)
  -p, --plugins PLUGINS_DIR1[,PLUGINS_DIR2[,...]]  Plugins directory (defaults to ./_plugins)
      --layouts DIR  Layouts directory (defaults to ./_layouts)
  -h, --help         Show this message
  -v, --version      Print the name and version
  -t, --trace        Show the full backtrace when an error occurs

Subcommands:
  serve, server, s      Serve your site locally
  docs                  Launch local server with docs for Jekyll v2.5.3
  build, b              Build your site
  doctor, hyde          Search site and print specific deprecation warnings
  new                   Creates a new Jekyll site scaffold in PATH
  help                  Show the help message, optionally for a given subcommand.
```

### `build` Command

```
$ jekyll help build

jekyll build -- Build your site

Usage:

  jekyll build [options]

Options:
      --config CONFIG_FILE[,CONFIG_FILE2,...]  Custom configuration file
      --future       Publishes posts with a future date
      --limit_posts MAX_POSTS  Limits the number of posts to parse and publish
      --lsi          Use LSI for improved related posts
  -D, --drafts       Render posts in the _drafts folder
      --unpublished  Render posts that were marked as unpublished

  -q, --quiet        Silence output.
  -V, --verbose      Print verbose output.
```

### `serve` Command

```
$ jekyll help serve

  jekyll serve [options]

Options:
  -B, --detach         Run the server in the background (detach)
  -P, --port [PORT]    Port to listen on
  -H, --host [HOST]    Host to bind to
  -b, --baseurl [URL]  Base URL
  
Build Options:
      --skip-initial-build  Skips the initial site build which occurs before the server is 
  -w, --[no-]watch     Watch for changes and rebuild
      --force_polling  Force watch to use polling
  
  plus all build options (see build command)
```


## Jekyll Quickstart

```
  $ jekyll new my-site
     # => New jekyll site installed in ~/my-site
  $ cd my-site
  $ jekyll build
     # => Configuration file: ~/_config.yml
     #                Source: ~/my-site
     #           Destination: ~/my-site/_site
     #          Generating... done.
  $ jekyll serve
     # =>     Server address: http://127.0.0.1:4000/
     #      Server running... press ctrl-c to stop.
```

Browse your site e.g. open the page @ `http://127.0.0.1:4000`


## Folder Structure

Minimial:

```
├── _config.yml                        # site configuration
├── _posts                             # blog posts
|   ├── 2015-01-01-week-1-factbook.md  #   filename format => YEAR-MONTH-DAY-TITLE.MARKUP
|   ├── 2015-01-08-week-2-hoe.md
|   └── 2015-01-15-week-3-slideshow.md
├── _layouts                           
|   ├── default.html                   # master layout template
|   └── post.html                      # blog post template
├── css                               
|   └── styles.css                     # styles for pages
├── feed.xml                           # web feed template (e.g. in rss or atom format)
└── index.html                         # index template
```

will result in (with `permalink: date`):

```
└── _site                                  # output build folder; site gets generated here
    ├── css                               
    |   └── styles.css                     # styles for pages (copied 1:1 as is)
    ├── 2015
    |   └── 01
    |       ├── 01
    |       |   └── week-1-factbook.html   # blog post page
    |       ├── 08
    |       |   └── week-2-hoe.html        # another blog post page
    |       └── 15
    |           └── week-3-slideshow.html  # another blog post page
    ├── feed.xml                           # web feed (e.g. in rss or atom format)
    └── index.html                         # index page
```

or result in (with `permalink: /:title.html`):

```
└── _site                           # output build folder; site gets generated here
    ├── css                               
    |   └── styles.css                     # styles for pages (copied 1:1 as is)
    ├── week-1-factbook.html        # blog post page
    ├── week-2-hoe.html             # another blog post page
    ├── week-3-slideshow.html       # another blog post page
    ├── feed.xml                    # web feed (e.g. in rss or atom format)
    └── index.html                  # index page
```

Note: See the `jekyll-minimal-theme` starter kit for an example
[source repo](https://github.com/feedreader/jekyll-minimal-theme) and
[live demo](http://feedreader.github.io/jekyll-minimal-theme).



With post drafts, page collections, data stores and shared building blocks:

```
├── _config.yml                        # site configuration
├── _posts                             # blog posts
|   ├── 2015-01-01-week-1-factbook.md  #  filename format => YEAR-MONTH-DAY-TITLE.MARKUP
|   ├── 2015-01-08-week-2-hoe.md
|   └── 2015-01-15-week-3-slideshow.md
├── _drafts                            # upcoming posts; not yet published 
|   ├── week-4-kramdown.md             # note: no date required 
|   └── week-5-feedparser.md
├── _layouts                           
|   ├── default.html                   # master layout templates
|   ├── book.html                      # book listing template
|   └── post.html                      # blog post template
├── _includes                          # shared building blocks
|   ├── footer.html
|   └── header.html
├── _data                              # data store (formats available .yml, .json, .csv)
|   └── members.csv
├── _books                             # page collection (for books)
|   ├── ruby-under-a-microscope.md
|   └── learn-ruby-the-hard-way.md
├── books                               
|   └── index.html                     # book listing index template
├── members.html                       # member listing template
├── feed.xml                           # web feed template (e.g. in rss or atom format)
└── index.html                         # site index template
```

Note: The `_post`, `_drafts`, `_layouts`, `_includes`, `_data`, `_books`, `_site` folders must start
with an underscore (`_`).


## `_posts` Folder

The post file name must follow the format: _YEAR-MONTH-DAY-TITLE.MARKUP_
(e.g. `2015-01-15-week-3-slideshow.md`).
The permalinks can be customized for each post,
but the date and markup language are determined by the file name.

```
├── _posts             
|   ├── 2015-01-01-week-1-factbook.md    # e.g. date=2015-01-01, markup=md
|   ├── 2015-01-08-week-2-hoe.md         #      date=2015-01-08, markup=md
|   └── 2015-01-15-week-3-slideshow.md   #      date=2015-01-15, markup=md
```

### Front Matter

```
---
layout: post
title:  "Week #3 - slideshow gem - a free web alternative to PowerPoint and Keynote in Ruby"
---
```

**Excerpt**

```
---
excerpt_separator: <!--more-->
---

Excerpt
<!--more-->
Out-of-excerpt
```

### Tips & Tricks

**Including images and resources**

```
![Ruby under a Microscope Book Cover]({{site.url}}/i/book-ruby-under-a-microscope.png)

[Hoe PDF Booklet](http://docs.seattlerb.org/hoe/Hoe.pdf); 6 Pages
```


## `_draft` Folder

Drafts are unpublished posts without a date.

```
├── _drafts
|   ├── week-4-kramdown.md
|   └── week-5-feedparser.md
```

## `_layouts` Folder

TBD

## `_includes` Folder

TBD

## `_data` Folder

TBD

## `_COLLECTION` Folder (e.g `_books`, `_albums`, etc.)

TBD


## Global Variables

```
site             -- Sitewide information plus configuration settings from  _config.yml.
page             -- Page specific information plus the front matter.
                    Custom variables set via the front matter will be available here.
content          -- In layout files, the rendered content of the Post or Page being wrapped. 
                    Not defined in Post or Page files.
paginator        -- When the paginate configuration option is set variable becomes available.
```


## Site Variables

**Built-in**

```
site.time           --  The current time (when you run the jekyll command)
site.pages          --  A list of all Pages
site.posts          --  A reverse chronological list of all Posts
site.related_posts  --  If the page processed is a Post, this contains a list of up to ten related Posts.
                        By default, these are low quality but fast to compute.
                        For high quality but slow to compute results, run the
                        jekyll command with the --lsi (latent semantic indexing) option.
site.static_files   --  A list of all static files (i.e. files not processed by Jekyll's converter
                        or Liquid's renderer - getting passed-through/copied over to the_site
                        folder as-is). Each file has three properties: path, modified_time and extname
site.html_pages     --  A list of all HTML Pages.
site.collections    --  A list of all the collections.
site.data           --  A list containing the data loaded from the files located in the _data folder.
site.documents      --  A list of all the documents in every collection.

site.categories.CATEGORY   -- The list of all Posts in category CATEGORY.
site.tags.TAG              -- The list of all Posts with tag TAG.
```

**Your Own (Custom)**

All variables set via the command line and 
in your `_config.yml`  site configuration are available through the `site` variable.
For example, if you have `url: http://openfootball.github.io` in your configuration file,
then in your Posts and Pages it will be stored in `site.url`.

If you add in your `_config.yml` site configuration, for example:

```
url:   'http://openfootball.github.io'
title: 'football.db - Open Football Data'
```

than you can use the variables in your posts, pages and templates:

```
site.url     -- your site's url
site.title   -- your site's title
```

Note: Jekyll does not parse changes to `_config.yml` in watch mode,
you must restart Jekyll to see changes to variables.


## Page Variables

```
page.content      --  The content of the Page, rendered or un-rendered depending upon what
                      Liquid is being processedand what page is.
page.title        --  The title of the Page.
page.excerpt      --  The un-rendered excerpt of the Page.
page.url          --  The URL of the Post without the domain, but with a leading slash, 
                      e.g. /2015/01/15/week-3-slideshow.html
page.date         --  The Date assigned to the Post. This can be overridden in a Post's front matter
                      by specifying a new date/time in the format YYYY-MM-DD HH:MM:SS (assuming UTC),
                      or YYYY-MM-DD HH:MM:SS +/-TTTT
                      (to specify a time zone using an offset from UTC. e.g. 2015-01-15 11:11:00 +0900).
page.id           --  An identifier unique to the Post (useful in feeds). 
                      e.g. /2015/01/15/week-3-slideshow
page.categories   --  The list of categories to which this post belongs.
                      Categories are derived from the directory structure above the _posts directory.
                      For example, a post at /ruby/gems/_posts/2015-01-15-week-3-slideshow.md would have
                      this field set to ['ruby', 'gem']. These can also be specified in the front matter.
page.tags         --  The list of tags to which this post belongs. These can be specified in the front matter.
page.path         --  The path to the raw post or page. Example usage: Linking back to the page or
                      post's source on GitHub. This can be overridden in the front matter.
page.next         --  The next post relative to the position of the current post in site.posts.
                      Returns nil for the last entry.
page.previous     --  The previous post relative to the position of the current post in site.posts.
                      Returns nil for the first entry.
```



## Liquid Template Filters n Tags

### Standard Filters

**String Filters**

```
{{ | capitalize }}      -- capitalize words in the input sentence
{{ | downcase }}        -- convert an input string to lowercase
{{ | upcase }}          -- convert an input string to uppercase
{{ | strip_html }}      -- strip html from string
{{ | strip_newlines }}  -- strip all newlines (\n) from string
{{ | newline_to_br }}   -- replace each newline (\n) with html break
{{ 'foofoo' | replace:'foo','bar' }}   -- replace each occurrence
 # => 'barbar'
{{ 'barbar' | replace_first:'bar','foo' }} -- replace the first occurrence
 # => 'foobar'
{{ 'foobarfoobar' | remove:'foo' }}  -- remove each occurrence
 # => 'barbar'
{{ 'barbar' | remove_first:'bar' }}  -- remove the first occurrence
  # => 'bar'
{{ 'foobarfoobar' | truncate: 5, '.' }}  -- truncate a string down to x characters. 
  # => 'foob.'                              It also accepts a second parameter that will append to the string
{{ | truncatewords }}               -- truncate a string down to x words
{{ 'bar' | prepend:'foo' }}         -- prepend a string
  # => 'foobar'
{{ 'foo' | append:'bar' }}          -- append a string
  # => 'foobar'
{{ "a~b" | split:"~" }}             -- split a string on a matching pattern
  # => ['a','b']
{{ "hello" | slice: -3, 3 }}        -- slice a string. Takes an offset and length
  # => llo
```

**Date Filters**

```
{{ | date }}     -- reformat a date 
```

**Array Filters**

```
{{ | first }}   -- get the first element of the passed in array
{{ | last  }}   -- get the last element of the passed in array
{{ | join  }}   -- join elements of the array with certain character between them
{{ | sort  }}   -- sort elements of the array
{{ | map   }}   -- map/collect an array on a given property
{{ | size  }}   -- return the size of an array or string
```

**Numbers, Math Filters**

```
{{ 4  | minus:2 }}       #=> 2    -- subtraction
{{ 1  | plus:1 }}        #=> 2    -- addition
{{ 5  | times:4  }}      #=> 20   -- multiplication
{{ 10 | divided_by:2 }}  #=> 5    -- division
{{ 3  | modulo:2 }}      #=> 1    -- remainder

{{ '1' | plus:'1' }}     #=>'11'  -- note: make sure to use numbers not strings
```

**Escape Filters**

```
{{ | escape }}       -- escape a string
{{ | escape_once }}  -- returns an escaped version of html without affecting existing escaped entities
```


### Jekyll Filters

**Date, Time Filters**

```
{{ site.time | date_to_rfc822 }}       -- Convert date to RFC-822 format 
 # => Mon, 07 Nov 2008 13:07:54 -0800     (e.g. used in rss feeds)
{{ site.time | date_to_xmlschema }}    -- Convert date to XML Schema (ISO 8601) format 
 # => 2008-11-07T13:07:54-08:00           (e.g. used in atom feeds)
 
{{ site.time | date_to_string }}       -- Convert date to short format
 # => 07 Nov 2008
{{ site.time | date_to_long_string }}  -- Convert date to long format
 # => 07 November 2008
```

**Where, Group By, Sort Filters** 

```
{{ site.members | where:"graduation_year","2014" }}   -- Select all the objects in an array where the key
                                                         has the given value.
{{ site.members | group_by:"graduation_year" }}       -- Group an array's items by a given property e.g.
                                                           [{"name"=>"2013", "items"=>[...]},
                                                            {"name"=>"2014", "items"=>[...]}]
{{ page.tags | sort }}                                -- Sort an array 
{{ site.posts | sort: 'author' }}                     -- Optional args for hashes:
{{ site.pages | sort: 'title', 'last' }}                  1. property name
                                                          2. nils order (first or last)
```

**Escape (XML, CGI, URI) Filters**

```
{{ page.content | xml_escape }}      -- Escape some text for use in XML
{{ "foo,bar;baz?" | cgi_escape }}    -- CGI escape a string for use in a URL;
 # => foo%2Cbar%3Bbaz%3F                replaces any special characters with appropriate %XX replacements
{{ "foo, bar \baz?" | uri_escape }}  -- URI escape a string
 # => foo,%20bar%20%5Cbaz?
```


**Convert (`markdownify`, `slugify`, `sassify`, `jsonify`) Filters**

```
{{ page.excerpt | markdownify }}        -- Convert a Markdown-formatted string into HTML
{{ site.data.projects | jsonify }}      -- Convert Hash or Array to JSON
{{ some_scss | scssify }}               -- Convert a SCSS-formatted string into CSS
{{ some_sass | sassify }}               -- Convert a Sass-formatted string into CSS

{{ "The _config.yml file" | slugify }}            -- Convert a string into a lowercase URL "slug";
 # => the-config-yml-file                            with option 'pretty': spaces and non-alphanumeric chars
{{ "The _config.yml file" | slugify: 'pretty' }}     except for ._~!$&'()+,;=@
 # => the-_config.yml-file                           
```

**Misc Filters**

```
{{ page.content | number_of_words }}         -- Count the number of words in some text
 # => 1337
{{ page.tags | array_to_sentence_string }}   -- Convert an array into a sentence. Useful for listing tags
 # => foo, bar, and baz
```

### Jekyll Tags

**Include Tag**

```
{% include footer.html %}                  -- Searches for include file in _includes folder
{% include footer.html param="value" %}       You can also pass parameters to an include

{% include_relative somedir/footer.html %} -- Searches for include file relative to the file where used
```

**Code Syntax Highlighting Tag**

```
{% highlight ruby %}
def main
  puts 'Hello World'
end
{% endhighlight %}
```

```
{% highlight ruby linenos %}         -- Use line numbers
def main
  puts 'Hello World'
end
{% endhighlight %}
```

**Gist Tag**

```
{% gist hyde/931c1c8d465a04042403 %}
{% gist hyde/931c1c8d465a04042403 hello_world.rb %}  -- You may specify the filename to display
```

(Source: see jekyll-gist gem)



## Permalinks

The default `date` permalink is defined as:

```
/:categories/:year/:month/:day/:title.html
```

### Permalink Variables

```
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
```

### Permalink Styles

**Built-in**

```
date     /:categories/:year/:month/:day/:title.html
pretty   /:categories/:year/:month/:day/:title/
none     /:categories/:title.html
```

**Examples**

Given a post named: /2015-01-15-week-3-slideshow.md

```
None specified (date)             /2015/01/15/week-3-slideshow.html
pretty                            /2015/01/15/week-3-slideshow/index.html
/:month-:day-:year/:title.html    /01-15-2015/week-3-slideshow.html
/blog/:year/:month/:day/:title    /blog/2015/01/15/week-3-slideshow/index.html
```


## CSS Preprocessor Example


```
├── _config.yml            # site configuration (add sass settings)
└── css 
    ├── _settings.scss     # include / partial settings
    └── style.scss         # main styles 
```

will result in:

```
└── _site
    └── css
        └── style.css      # all-in-one styles (converted from scss to css)
```

Example - `_config.yml`:

```
sass:
  sass_dir: css    # gets used for partial lookup (default is _sass)
```

Example - `_settings.scss`:

```
$font-family:    Helvetica, Arial, sans-serif;

$color-primary:  #8b0000;    // dark red (ruby)
...
```

Exampe - `style.scss`:

```
---
---

@import 'settings';           // include partial (will use sass_dir for lookup)

body {
  font-family:  $font-family; // use variables, nested rules, and more
}
...
```
Note: Front matter (minimal) 

```
---
---
```

or with comments

```
---
# ensure Jekyll converts scss to css
---
```

required; ensures Jekyll converts `style.scss` to `style.css`; 
include all partials (e.g. `_settings.scss`, and so on) with `@import` directives.


(Source: [jekyll-sass-converter gem](https://github.com/jekyll/jekyll-sass-converter))


## Template Examples

### Displaying an index of posts

```html
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
```

### Displaying an index of posts with excerpts

```html
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
```

### Generate web feed e.g. `feed.xml` for last ten posts (in Atom format)

```xml
---
layout: null
---
<?xml version="1.0" encoding="utf-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
  <title>{{ site.title }}</title>
  <link href="{{ site.url }}/feed.xml" rel="self"/>
  <link href="{{ site.url }}/"/>
  <updated>{{ site.time | date_to_xmlschema }}</updated>
  <id>{{ site.url }}/</id>
  <author>
    <name>{{ site.author }}</name>
  </author>
  <generator>Jekyll v{{ jekyll.version }}</generator>

  {% for post in site.posts limit: 10 %}
  <entry>
    <title>{{ post.title | xml_escape }}</title>
    <link href="{{ site.url }}{{ post.url }}"/>
    <updated>{{ post.date | date_to_xmlschema }}</updated>
    <id>{{ site.url }}{{ post.id }}</id>
    <content type="html">{{ post.content | xml_escape }}</content>
  </entry>
  {% endfor %}
</feed>
```

Tip: Add feed auto-discovery to your master layout template in the header. Example:

```html
<link rel="alternate" type="application/atom+xml" href="{{ site.url }}/feed.xml" title="News Feeds">
```

Note: You can add more than one feed, for example:

```html
<link rel="alternate" type="..." href="{{ site.url }}/feed.xml"       title="Blog News Feeds">
<link rel="alternate" type="..." href="{{ site.url }}/books/feed.xml" title="Books News Feed">
<link rel="alternate" type="..." href="{{ site.url }}/links/feed.xml" title="Links News Feed">
```



## Paginator

### Paginator Variables

```
paginator.per_page            --  Number of Posts per page
paginator.posts               --  Posts available for that page
paginator.total_posts         --  Total number of Posts
paginator.total_pages         --  Total number of Pages
paginator.page                --  The number of the current page
paginator.previous_page       --  The number of the previous page
paginator.previous_page_path  --  The path to the previous page
paginator.next_page           --  The number of the next page
paginator.next_page_path      --  The path to the next page
```

(Source: see jekyll-paginator gem)


***Render the paginated Posts***

```html
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
```

## GitHub Pages

- [`pages.github.com`](https://pages.github.com/)

What Jekyll version and plugins get used?

- [`pages.github.com/versions`](https://pages.github.com/versions), for example (update Jan/2015):

Library               | Version
--------------------- | -----------
jekyll                | 2.4.0
jekyll-coffeescript   | 1.0.1
jekyll-sass-converter | 1.2.0
kramdown              | 1.5.0
liquid                | 2.6.1
pygments.rb           | 0.6.0
jemoji                | 0.4.0
jekyll-mentions       | 0.2.1
jekyll-redirect-from  | 0.6.2
jekyll-sitemap        | 0.6.3
github-pages          | 32
ruby                  | 2.1.1


### `site.github` Variables

```
site.github.contributors    -- A list of your project's contributors (*)
site.github.public_repositories    -- A list of your public repositories (*)
site.github.organization_members   -- A list of your organization's public members (*)
...
```
(*) as returned through the contributors/repositories list/organization members API

Each of these new variables let you use the complete user/repository objects in Jekyll, thus,
you no longer need any client-side JavaScript API calls when showcasing
your projects on GitHub. For more information on displaying metadata
within your Jekyll site, see [Repository metadata on GitHub Pages](https://help.github.com/articles/repository-metadata-on-github-pages/).

(Source: [`jekyll-github-metadata` gem](https://github.com/jekyll/github-metadata))


### Sitemap Plugin

By simply adding the plugin to your site's configuration (`_config.yml`) e.g.

```
gems:
- jekyll-sitemap
```

Jekyll will automatically generate a `sitemaps.org`-compliant sitemap,
making it easier for search engines to index your site's content.

Note: The sitemap plugin is already added (and white-listed) on GitHub Pages.

(Source: [`jekyll-sitemap` gem](https://github.com/jekyll/jekyll-sitemap))

### How-To: Use Single `gh-pages` Branch; Delete `master` Branch

Step 1a) Already has `gh-pages` branch:

```
git checkout gh-pages   
git merge master
git push
```

Step 1b) Create `gh-pages` branch:

````
git checkout -b gh-pages
git merge master
git push origin gh-pages
````

Step 2) Make `gh-pages` branch default branch on GitHub via settings tab

Step 3)  Delete `master` branch on GitHub

```
git push origin :master     # will delete master branch on remote (that is, github)
    
git branch -d master        # will delete master branch in local remote
```

Step 4) Delete local git repo and get a fresh clone from GitHub

```
rm -rf <repo>
git clone <repo-remote-url>
```

That's it.

**Bonus: Check if remote is setup with `git remote show <repo-remote-shorthand>`**

```
$ git remote show origin
# => * remote origin
       Fetch URL: https://github.com/openbeer/book.git
       Push  URL: https://github.com/openbeer/book.git
       HEAD branch: gh-pages
       Remote branch:
          gh-pages tracked
       Local branch configured for 'git pull':
          gh-pages merges with remote gh-pages
       Local ref configured for 'git push':
          gh-pages pushes to gh-pages (up to date)
```

## Octopress Commands

```
$ octopress --help

octopress 3.0.0 -- Octopress is an obsessively designed toolkit for Jekyll blogging.

Usage:

  octopress <subcommand> [options]

Options:
  -h, --help         Show this message
  -v, --version      Print the name and version
  -t, --trace        Show the full backtrace when an error occurs

Subcommands:
  new         Creates a new site with Jekyll and Octopress scaffolding at the specified path.
  docs        Launch local server with docs for Octopress v3.0.0.rc.31 and Octopress plugins.
  init        Add Octopress's default scaffolding to your site.
  publish     Convert a draft to a normal published post.
  unpublish   Convert a post to a draft. Command accepts path to post or search string.
  isolate     Move all posts not matching selected post to _posts/_exile. Command accepts path to post or search string.
  integrate   Reintegrate posts from _posts/_exile.
  deploy      Deploy your Octopress site.
```

## `new` Command

```
$ octopress new --help

octopress new -- Creates a new site with Jekyll and Octopress scaffolding at the specified path.

Usage:

  octopress new <PATH>

Options:
  -f, --force        Force creation even if path already exists.
  -b, --blank        Creates scaffolding but with empty files.
  -h, --help         Show this message

Subcommands:
  page    Add a new page to your Jekyll site.
  post    Add a new post to your Jekyll site.
  draft   Add a new draft post to your Jekyll site.
```

## `new post` Command

```
$ octopress new post --help

octopress new post -- Add a new post to your Jekyll site.

Usage:

  octopress new post <TITLE> [options]

Options:
  -d,  --date DATE    Use 'now' or a String that is parseable by Time#parse.
  -tm, --template PATH  New post from a template.
  -l,  --lang LANGUAGE  Set a post language (e.g. en, it) for multi-language sites.
  -f,  --force        Overwrite file if it already exists
  -s,  --slug SLUG    Use this slug in filename instead of sluggified post title.
  -d,  --dir DIR      Create post at _posts/DIR/.
  -c,  --config <CONFIG_FILE>[,CONFIG_FILE2,...]  Custom Jekyll configuration file
  -h,  --help         Show this message
```

## `deploy` Command

```
$ octopress deploy --help

octopress deploy 1.0.4 -- Deploy your Octopress site.

Usage:

  octopress deploy [options]

Options:
      --config FILE  The path to your config file (default: _deploy.yml)
  -h, --help         Show this message

Subcommands:
  pull         Pull down the published copy of your site into DIR
  init         Create a configuration file for a deployment method (git, rsync, s3).
  add-bucket   Add a new S3 bucket and configure it for static websites. Name defaults to bucket_name in config file
```


## Octopress Quickstart

```
  $ octopress new my-site
     # => New jekyll site installed in ~/my-site 
     #    Added Octopress scaffold:
     #     + _templates/
     #     +   draft
     #     +   page
     #     +   post
  $ cd my-site
  $ jekyll build
     # => Configuration file: ~/_config.yml
     #                Source: ~/my-site
     #           Destination: ~/my-site/_site
     #          Generating... done.
  $ jekyll serve
     # =>     Server address: http://127.0.0.1:4000/
     #      Server running... press ctrl-c to stop.   
```
