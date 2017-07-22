---
layout: post
title:  "Using Bootstrap with Jekyll"
date:   2017-07-22 18:14:13 +0100
categories: jekyll bootstrap bower
---

It all started with wanting some text to move from above a picture to beside it...


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
[cran]: https://cran.r-project.org/
[RStudio]: https://www.rstudio.com/products/rstudio/download/
[so-personal-lib]: https://stackoverflow.com/questions/44861967/r-3-4-1-single-candle-personal-library-path-error-unable-to-create-na
[yt-ubuntu-r]: https://www.youtube.com/watch?v=Nxl7HDUyw0I
[yt-ubuntu-r-rstudio]: https://www.youtube.com/watch?v=kF0-FH-xBiE
[debian-bug]: https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=866768
