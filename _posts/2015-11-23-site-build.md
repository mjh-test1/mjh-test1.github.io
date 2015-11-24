---
layout: post
title: Moving to Jekyll
description: Migrating my wordpress site to Jekyll
tags:
  - Jekyll
  - Lanyon
---
I've hosted Wordpress on my own server for about 8 years now, the content is mainly stuff that i've learnt and at some point will probably come in useful. Wordpress is a powerful platform capable of building sites as complex or simple as you can envisage. It does, however, come at a price:
* constant tlc required to keep it up to date and secure
* lots of bells and whisltes to act as a distraction
* a reasonable resource requirement from apache, PHP and MySQL.

For what I do using a full blown publishing platform like Wordpress is serious overkill and I had been considering making a change when I stumbled across a [blog post by Scott Lowe describing the new platform he was using](http://blog.scottlowe.org/2015/01/06/the-story-behind-the-migration/).

### Migrating to Jekyll and Lanyon

There are a number of reasons why I chose to migrate from a personally hosted Wordpress instance to a static site hosted by Github, to name a few:
* I can use Vi to edit posts. Vi is like Marmite, some people love it others hate it; I love it.
* I can use git to manage the site. I use git and github to manage projects and other code so it makes sense to manage my site with it.
* I'll save hours of my life not having to keep updaing Wordpress and plugins.
* markdown is not distracting when writing content.


### Resources

A quick [Google search](https://www.google.co.uk/q=migrating+from+wordpress+to+jekyll) reveals a number of good articles by people who have done the same thing as me; I wont repeat their advice other than to say [exitwp](https://github.com/thomasf/exitwp) was invaluable. I modified it slightly to dump all images into one directory rather than splitting them into subdirectories but you could just as easily do that with `mv` or `cp`.

{% highlight diff %}
diff --git a/exitwp.py b/exitwp.py
index 0ab028f..9bd13b0 100755
--- a/exitwp.py
+++ b/exitwp.py
@@ -261,7 +261,7 @@ def write_jekyll(data, target_format):
                 file_infix = file_infix + 1
             files[src] = filename = maybe_filename
 
-        target_dir = os.path.normpath(blog_dir + '/' + dir_prefix + '/' + dir)
+        target_dir = os.path.normpath(blog_dir + '/' + dir_prefix)
         target_file = os.path.normpath(target_dir + '/' + filename)
 
         if (not os.path.exists(target_dir)):
{% endhighlight %}

### Changes and additions

I've modified Lanyon a little to add some bits I wanted on the site, most of these changes were made easy by building on the work of others so my thanks go out to those people.

* Tags page - Based on the [example by psteadman](https://github.com/psteadman/psteadman.github.io/blob/master/tags.html)
* Font-awesome - Modified `_includes/head.html` and added the font-awesome css as per their [getting started guide](https://fortawesome.github.io/Font-Awesome/get-started/)
* Twittercards - Using [code from David Ensinger](http://davidensinger.com/2013/04/supporting-twitter-cards-with-jekyll/)
* Google analytics - A simple include file and `_config.yaml` variable to hold the tracking code
* Sharing link on posts - I actually did this bit myself!
* Excerpts - I changed the default index page to show excerpts rather than the full post, code borrowed and adapted from [Scott Lowe's index page](https://github.com/lowescott/lowescott.github.io/blob/master/index.html) and the [Jekyll guide](http://jekyllrb.com/docs/posts/)

