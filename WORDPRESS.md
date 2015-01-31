# WordPress <=> Jekyll - Template (Theming) Cheatsheet



`bloginfo()`

```
<?php bloginfo('name'); ?>         |   {{ site.title }} or {{ site.name }}
<?php bloginfo('description'); ?>  |   {{ site.description }}
<?php bloginfo('url'); ?>          |   {{ site.url }}
<?php bloginfo('admin_email'); ?>  |   {{ site.admin.email }}
<?php bloginfo('version'); ?>      |   {{ site.version }}
```


Define in your `_config.yml`:

```
title:        Dr Jekyll and Mr Hyde    ## or
name:         Dr Jekyll and Mr Hyde
description:  Just another Jekyll site
url:          http://www.example.com
version:      3.0                      ## check if auto-set/builtin ??

admin:
  email:      admin@example.com
```


`wp_title`

```
<?php wp_title();    ?>         |    {{ post.title }} or {{ page.title }}
```


The Loop

```
<?php while( have_posts() ) : the_post();  | {% for post in site.posts %}
        ...                                |   ...
      endhwile; ?>                         | {% endfor %}
```


Includes - `get_header()`, `get_sidebar()`, `get_footer()`

```
<?php get_header(); ?>                   |  {{ include header.html }}
<?php get_sidebar(); ?>                  |  {{ include sidebar.html }}
<?php get_footer(); ?>                   |  {{ include footer.html }}
```
