# WordPress <=> Jekyll - Template (Theming) Cheat Sheet



`bloginfo()`

```
<?php bloginfo('name'); ?>         |   {{ site.title }} or {{ site.name }}
<?php bloginfo('description'); ?>  |   {{ site.description }}
<?php bloginfo('url'); ?>          |   {{ site.url }}
<?php bloginfo('admin_email'); ?>  |   {{ site.admin.email }}
```

```
<?php bloginfo('version'); ?>      |   {{ jekyll.version }}   # predefined
```


Define in your `_config.yml`:

```
title:        Dr Jekyll and Mr Hyde    ## or
name:         Dr Jekyll and Mr Hyde
description:  Just another Jekyll site
url:          http://www.example.com

admin:
  email:      admin@example.com
```


`wp_title`

```
<?php wp_title();    ?>         |    {{ post.title }} or {{ page.title }}
```


The Loop

```
<?php while( have_posts() ) : the_post(); ?>  | {% for post in site.posts %}
   <?php the_title(); ?>                      |   {{ post.title }}
   <?php the_content(); ?>                    |   {{ post.content }}
   ...                                        |   ...
<?php endwhile; ?>                            | {% endfor %}
```


Includes - `get_header()`, `get_sidebar()`, `get_footer()`

```
<?php get_header(); ?>                   |  {% include header.html  %}
<?php get_sidebar(); ?>                  |  {% include sidebar.html %}
<?php get_footer(); ?>                   |  {% include footer.html  %}
```

