---
layout: post
title:  "Using Bootstrap with Jekyll"
date:   2017-07-22 18:14:13 +0100
categories: jekyll bootstrap bower
---

This site was built using Jekyll - so all the posts are written in markdown. Markdown is convenient for writing content - but it's limited when it comes to creating layouts. One option for customising the front end of sites is the popular front-end component library [bootstrap][bootstrap].

This post covers the steps I took to set up Bootstrap with Jekyll. The process involved installing an installer to install the installer that would install Bootstrap. This gif sums up the process:

![alt text](/assets/hal-lightbulb.gif)

# Install npm
[npm][npm] is the installer to install the installer that will install Bootstrap. This step was quite straightforward:

{% highlight shell %}
joseph@S400CA:~$ sudo apt install npm
joseph@S400CA:~$ npm -v
3.5.2
{% endhighlight %}

# Install bower
[Bower][bower] is the installer that will install Bootstrap. Install it with npm:

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
sudo apt-get update
sudo apt-get install nodejs
joseph@S400CA:~$ nodejs -v
v4.2.6
{% endhighlight %}

Although...

{% highlight shell %}
joseph@S400CA:~/Dropbox/jekyll-01$ bower install bootstrap
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

This is promising. I also learnt that installing a library with bower is project dependant (i.e. you need to install from the location of the project you want the library for):

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

Success! Bower handles dependencies; so it installed jQuery too:

{% highlight shell %}
joseph@S400CA:~/my/project/directory$ bower list
bower check-new     Checking for new versions of the project dependencies...
directory /home/joseph/my/project/directory
└─┬ bootstrap#3.3.7 extraneous (latest is 4.0.0-alpha.6)
  └── jquery#3.2.1
{% endhighlight %}

# Tidying up
Installing Bootstrap had some unexpected minor consequences to tidy up.

#### Documentation being mistaken for content
Some .md files in the bootstrap documentation (e.g. READMEs and change logs) were being compiled by Jekyll into pages on the site. This was strange because I assumed site pages had to be at the root directory of Jekyll projects. Excluding the bower_components directory in _config.yml solved the unwanted pages. But also removed all bootstrap functionality. Being more specific with exclusions solved the problem:

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
Perhaps unsurprisingly - once set up with a Jekyll site - Bootstrap applies it's own CSS to all the pages in that site. This means the aesthetics of the site subtly change. Personally I'm happy to accept this for the benefits Bootstrap brings. In future I may tweak the look and feel of some components.

# Testing
The motivating task for all this was simple: I wanted to vertically align text to the right of a picture. [Flexbox][flexbox] is a new layout mode in CSS3 which seemed a good fit for this. It comes with bootstrap 4.0.0 (alpha at the time of writing this) so I needed to explicitly specify the version number for Bower which was surprisingly easy.

You can see the final result on my [homepage](/).



########################################################

1. install npm
1. install bower
1. install node.js
1. install bootstrap
1. add css style sheet to head include

### npm
sudo apt install npm

### bower
Don't forget sudo...
sudo npm install -g bower

joseph@S400CA:~$ sudo npm install -g bower
[sudo] password for joseph: 
npm WARN deprecated bower@1.8.0: ..psst! While Bower is maintained, we recommend Yarn and Webpack for *new* front-end projects! Yarn's advantage is security and reliability, and Webpack's is support for both CommonJS and AMD projects. Currently there's no migration path, but please help to create it: https://github.com/bower/bower/issues/2467
/usr/local/bin/bower -> /usr/local/lib/node_modules/bower/bin/bower
/usr/local/lib
└── bower@1.8.0 

joseph@S400CA:~$ bower install bootstrap
/usr/bin/env: ‘node’: No such file or directory

### node.js
(npm comes with node - ah well...)
sudo apt-get update
sudo apt-get install nodejs

seemed to work:
joseph@S400CA:~$ nodejs -v
v4.2.6

but i ignored the warning sign:
joseph@S400CA:~$ node -v
The program 'node' is currently not installed. You can install it by typing:
sudo apt install nodejs-legacy

and it didn't work in the end:
joseph@S400CA:~/Dropbox/jekyll-01$ bower install bootstrap
/usr/bin/env: ‘node’: No such file or directory

I followed the advice [here][Nyuu-issue]:
sudo apt-get install nodejs-legacy

Some good noises:
joseph@S400CA:~$ node -v
v4.2.6
joseph@S400CA:~$ nodejs -v
v4.2.6

Success!
joseph@S400CA:~/Dropbox/jekyll-01$ bower install bootstrap
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

It also installed bootstraps dependency, jquery:
joseph@S400CA:~/Dropbox/jekyll-01$ bower list
bower check-new     Checking for new versions of the project dependencies...
jekyll-01 /home/joseph/Dropbox/jekyll-01
└─┬ bootstrap#3.3.7 extraneous (latest is 4.0.0-alpha.6)
  └── jquery#3.2.1

### Extra pages??
The readmes for jquery and bootstrap appear as items in the menu. Bit odd as I thought site pages had to be at the root of the jekyll project directory. I deleted them.

### CSS
```html
<link rel="stylesheet" type="text/css" href="bower_components/bootstrap/dist/css/bootstrap.css">
```
Slightly different feel. But willing to tweak look and feel for the benefit of easy responsive layouts.

### Testing bootstrap grid template

Works well. Wanted to vertically align text to the right of picture. Best practice seems to be to use flexbox which comes with bootstrap 4.0.0. Download bootstrap 4.0.0 which is surprisingly easy with bower. Not sure why it didn't install 4.0.0 automatically. Perhaps because it's in alpha (not even beta).

The one problem is that lots of .md files in the bootstrap documentation are being compiled by jekyll into pages for my website.

Excluding the bower_components directory in config file does get rid of the unwanted pages. But it also stops any bootstrap functionality from working! Being more specific with exclusions solves the problem.


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
