---
layout: post
title: "New Year - First Post"
description: "First post in the New Year 2014."
category: articles
tags: [first post, images, test]
---

It's still Januray - so it's still OK to do New Year's resolution thing :)  
I finally decided to stop making excuses and start blogging. I wanted to do this for a while but aside from few false starts I never got to it. 



<figure>
	<img src="http://farm1.staticflickr.com/151/339912423_4416699c99_o.jpg">
	<figcaption><a href="http://www.flickr.com/photos/sally_12/339912423/" title="Photo by: Sally Mahoney"></a>Photo by: Sally Mahoney</figcaption>
</figure>

### Getting to it

#### The platform

I was having a hard time deciding on a platform - as there is so much choice and every one has good and bad sides.  
The platforms I was considering were:

* [Blogger](http://blogger.com)
* [Wordpress](http://wordpress.com) (hosted @ wordpress.com)
* [Wordpress](http://wordpress.org) (self hosted)
* [Tumblr](http://tumblr.com)
* [Github Pages](http://pages.github.com)

During my research I also became interested in static websites and I started playing with:

* [Jekyll](http://jekyllrb.com)
* [Octopress](http://octopress.org)
* [Pelican](http://getpelican.com)
* [Brace](http://brace.io)

In the end my platform of choice was Github Pages + Jekyll.  
Time will tell how this works out, but I like the idea of blogging from my Sublime editor and not dealing with the cluettered web interface. Also there is something cool about being able to **git push** your new blog post :)

#### Setup

It's really easy to get started with GithubPages

* Create yourself a [Github](http://github.com) account (if you don't have one already)
* Create a new repository named: **username.github.io**
* Clone that repo
{% highlight bash %}
~$ git clone https://github.com/username/username.github.io
~$ git checkout master
{% endhighlight %}
* Find a theme you like at [JekyllThemes](http://jekyllthemes.org)
* Follow instructions to install your theme - ususally copy all theme files into where you cloned your repo
* Edit _config.yml
* Push it
{% highlight bash %}
~$ git add --all
~$ git commit -m "Initial commit"
~$ git push
{% endhighlight %}

Success!



