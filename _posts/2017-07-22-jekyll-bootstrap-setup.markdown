---
layout: post
title:  "Using Bootstrap with Jekyll"
date:   2017-09-10 20:53:13 +0100
categories: jekyll bootstrap bower
---

This site was built using Jekyll - so all the posts are written in markdown. Markdown is convenient for writing content - but it's limited when it comes to creating layouts. One option for customising the front end of sites is the popular front-end component library [bootstrap][bootstrap].

This post covers the steps I took to set up Bootstrap with Jekyll. The process involved installing an installer to install the installer that would install Bootstrap. It felt a bit like this:

![alt text](/assets/hal-lightbulb.gif)

# Figuring out where to start
The first installation option on the Bootstrap [getting started](https://getbootstrap.com/docs/3.3/getting-started/) page is [Bower][bower]. I have a habit of going with the first option presented (my dubious rationale being that's where more experienced people will put the 'preferable' option for the benefit of others). Bower requires [Node.js][nodejs] and [npm][npm]. So that is where we start.

# Install npm
npm is the installer to install the installer that will install Bootstrap. This step was quite straightforward:

{% highlight shell %}
joseph@S400CA:~$ sudo apt install npm
joseph@S400CA:~$ npm -v
3.5.2
{% endhighlight %}

# Install bower
Bower is the installer that will install Bootstrap. Install it with npm:

{% highlight shell %}
joseph@S400CA:~$ sudo npm install -g bower
[sudo] password for joseph: 
npm WARN deprecated bower@1.8.0: ..psst! While Bower is maintained, we recommend Yarn and Webpack for *new* front-end projects! Yarn's advantage is security and reliability, and Webpack's is support for both CommonJS and AMD projects. Currently there's no migration path, but please help to create it: https://github.com/bower/bower/issues/2467
/usr/local/bin/bower -> /usr/local/lib/node_modules/bower/bin/bower
/usr/local/lib
└── bower@1.8.0
{% endhighlight %}

{% highlight shell %}
joseph@S400CA:~$ bower -v
1.8.0
{% endhighlight %}

# (Attempt to) Install Bootstrap
Finally we can install Bootstrap:

{% highlight shell %}
joseph@S400CA:~$ bower install bootstrap
/usr/bin/env: ‘node’: No such file or directory
{% endhighlight %}

Oops... Seems I was trying to move too quickly and skipped installing [Node.js][nodejs]. In fact, it turns out npm is [distributed with Node.js](https://www.npmjs.com/get-npm) so installing npm on it's own was redundant. Seems like the slow way is often the fast way.

# Install Node.js - attempt #1

Seems simple enough:

{% highlight shell %}
sudo apt-get install nodejs
joseph@S400CA:~$ nodejs -v
v4.2.6
{% endhighlight %}

Although...

{% highlight shell %}
joseph@S400CA:~/my/project/directory$ bower install bootstrap
/usr/bin/env: ‘node’: No such file or directory
{% endhighlight %}

It seems I didn't have the right thing installed:

{% highlight shell %}
joseph@S400CA:~$ node -v
The program 'node' is currently not installed. You can install it by typing:
sudo apt install nodejs-legacy
{% endhighlight %}

# Install Node.js - attempt #2

After reading animetosho's advice [here][Nyuu-issue] I followed Linux's initial suggestion and installed nodejs-legacy:

{% highlight shell %}
sudo apt-get install nodejs-legacy
joseph@S400CA:~$ node -v
v4.2.6
joseph@S400CA:~$ nodejs -v
v4.2.6
{% endhighlight %}

Promising! I also learnt that installing a library with bower is project dependant (i.e. you should install at the root of your project directory):

{% highlight shell %}
joseph@S400CA:~/my/project/directory$ bower install bootstrap
bower not-cached    https://github.com/twbs/bootstrap.git#*
bower resolve       https://github.com/twbs/bootstrap.git#*
bower download      https://github.com/twbs/bootstrap/archive/v3.3.7.tar.gz
bower extract       bootstrap#* archive.tar.gz
bower resolved      https://github.com/twbs/bootstrap.git#3.3.7
bower not-cached    https://github.com/jquery/jquery-dist.git#1.9.1 - 3
bower resolve       https://github.com/jquery/jquery-dist.git#1.9.1 - 3
bower download      https://github.com/jquery/jquery-dist/archive/3.2.1.tar.gz
bower extract       jquery#1.9.1 - 3 archive.tar.gz
bower resolved      https://github.com/jquery/jquery-dist.git#3.2.1
bower install       bootstrap#3.3.7
bower install       jquery#3.2.1

bootstrap#3.3.7 bower_components/bootstrap
└── jquery#3.2.1

jquery#3.2.1 bower_components/jquery
{% endhighlight %}

Success! Bower handles dependencies - so it installed jQuery too:

{% highlight shell %}
joseph@S400CA:~/my/project/directory$ bower list
bower check-new     Checking for new versions of the project dependencies...
directory /home/joseph/my/project/directory
└─┬ bootstrap#3.3.7 extraneous (latest is 4.0.0-alpha.6)
  └── jquery#3.2.1
{% endhighlight %}

# Tidying up
Installing Bootstrap caused some minor hiccups to resolve.

#### Documentation being mistaken for content
Some .md files in the bootstrap documentation (e.g. READMEs and change logs) were being compiled by Jekyll into pages on the site. This was strange because I assumed site pages had to be at the root directory of Jekyll projects. Excluding the <code>bower_components</code> directory in <code>_config.yml</code> solved the unwanted pages but removed all bootstrap functionality in the process. Being more specific with exclusions solved the problem:

{% highlight yaml %}
exclude:
  - Gemfile
  - Gemfile.lock
  - bower_components/tether/docs/1-Overview
  - bower_components/tether/docs/2-Examples
  - bower_components/tether/docs/3-Advanced
  - bower_components/tether/README.md
  - bower_components/tether/CHANGELOG.md
  - bower_components/bootstrap/README.md
{% endhighlight %}

#### CSS changes
Once set up with a Jekyll site, Bootstrap applies it's own CSS to all the pages in that site (I don't know why this surprised me when I first saw it happen). This means the aesthetics of the site subtly change. Personally I'm happy to accept this for the benefits Bootstrap brings. In future I may tweak the look and feel of some components.

# Testing
The motivating task for all this was simple: I wanted to vertically align text to the right of a picture. [Flexbox][flexbox] is a new layout mode in CSS3 which seemed a good fit for this. It comes with bootstrap 4.0.0 (alpha at the time of writing this) so I needed to stipulate the version number for Bower which was surprisingly easy.

You can see the final result on my [homepage](/).

# Reflections
Originally I had no intention of writing this post. While going through the above process, I felt the need to record the steps I'd taken, to help get past some of the tricky bits. Had I done this from the start, I may have avoided the redundant step of installing npm at the beginning.

[Nyuu-issue]: https://github.com/animetosho/Nyuu/issues/14
[bootstrap]: http://getbootstrap.com/
[npm]: https://www.npmjs.com/
[bower]: https://bower.io/
[nodejs]: https://nodejs.org/en/
[flexbox]: https://www.w3schools.com/css/css3_flexbox.asp
[cran]: https://cran.r-project.org/
[RStudio]: https://www.rstudio.com/products/rstudio/download/
[so-personal-lib]: https://stackoverflow.com/questions/44861967/r-3-4-1-single-candle-personal-library-path-error-unable-to-create-na
[yt-ubuntu-r]: https://www.youtube.com/watch?v=Nxl7HDUyw0I
[yt-ubuntu-r-rstudio]: https://www.youtube.com/watch?v=kF0-FH-xBiE
[debian-bug]: https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=866768
