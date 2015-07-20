# Dr. Jekyll's Themes - Add Your Theme!

(Yet Another) Static Site Theme Directory - see it live @ [`drjekyllthemes.github.io`](http://drjekyllthemes.github.io)


## How-To Add Your Theme

* Fork the [themes repo](https://github.com/drjekyllthemes/themes) on GitHub
* Add a new entry in the [`themes.yml`](https://github.com/drjekyllthemes/themes/blob/master/themes.yml) file and fill out all fields.
  Example:

~~~
- title:     Shiori
  homepage:  http://ellekasai.github.io/shiori/
  download:  http://github.com/ellekasai/shiori/
  demo:      http://ellekasai.github.io/shiori/
  author:    Elle Kasai
  thumbnail: shiori.png
  license:   MIT
~~~

* Make a 250 x 200 thumbnail (*) and drop it in the thumbnails folder.
  Note: Do NOT forget to list its filename in the `themes.yml` entry.
* Check that everything is ok, then open up a pull request.
* Thanks!



## Tips & Tricks

Q: How to create a 250 x 200 thumbnail?

A: One way is to create a regular-size screenshoot e.g. 1024 x 768 in step one.
In step two calculate how much to zoom in
(divide the required width, that is, 250 pixel by your current width,
that is, 1024 pixel) e.g.

     250
    ---- * 100 =  24.4 %
    1024

And than readjust the scale to 24.4% and set the width and height to 250 x 200.
That's it.

Another example - let's say the screenshoot size is 500 x 400 than
calculate how much to zoom in e.g.

     250
    ---- * 100 =  50 %
     500



## Meta

**License**

The themes directory is dedicated to the public domain.
Use it as you please with no restrictions whatsoever.

**Questions? Comments?**

Post them to the [jekyll talk forum](https://talk.jekyllrb.com). Thanks!

