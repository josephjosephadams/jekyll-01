---
layout: post
title:  "Getting started with R on Ubuntu"
date:   2017-07-04 12:03:13 +0100
categories: r linux
---

Since 2015 I've been using R and Linux separately. This week I took the plunge and set up my R work flow in Ubuntu. 

Coming from the point-and-click world of Windows, it wasn't as easy as I expected. Online resources explained each part of the process reasonably well. But a big picture summary was lacking. Something to give an idea of what would be involved start to finish. Especially for someone's first time.

<div style="text-align: center">
	<img src="/assets/ubuntu-ball.jpg" alt="Ubuntu Ball" style="width: 150px;"/>
	<img src="/assets/plus-sign.jpg" alt="Plus sign" style="width: 200px;"/>
	<img src="/assets/RStudio-Ball.jpg" alt="RStudio Ball" style="width: 150px;"/>
</div>

<!-- ![RStudio Ball](/assets/RStudio-Ball.jpg)
![Ubuntu Ball](/assets/ubuntu-ball.jpg) -->

So here is my version of that big picture summary - in three parts: a check-list with links; a summary of some tricky bits; and lessons learnt from writing this post.

### Check-list
1. Download and install R from [CRAN][cran]
	* Click **Download R for Linux** then choose Ubuntu
	* Follow the instructions
1. Download and install [RStudio][RStudio]

### Tricky bits
The first thing that struck me was how involved the process was. My first thoughts looking at the [CRAN][cran] instructions was *is this really all necessary?* *Why does this involve editing files and running terminal commands?* After following the lengthy instructions I finally had R and RStudio installed. 

But packages weren't downloading:

{% highlight r %}
> install.packages("ggplot2")
Installing package into ‘/usr/local/lib/R/site-library’
(as ‘lib’ is unspecified)
Warning in install.packages :
  'lib = "/usr/local/lib/R/site-library"' is not writable
Would you like to use a personal library instead?  (y/n) y
Would you like to create a personal library
NA
to install packages into?  (y/n) y
Error in install.packages : unable to create ‘NA’
{% endhighlight %}

I found [this solution][so-personal-lib] but it felt a bit hacky. Eventually I realised I'd skipped  the very last step in the [CRAN][cran] instructions:

> Individual users can install R packages into their home directory. The simplest procedure is to create a file ~/.Renviron containing, e.g.,

`R_LIBS_USER="~/lib/R/library"`

> The install.packages() and update.packages() functions will then work in directory ~/lib/R/library.

In human-speak this means:

1. Users (i.e. you) do not yet have write access to a directory to download packages into
1. You must create one and tell R about it

So we have two steps:

1. Create a directory to download packages into. This could be `~/lib/R/library` as suggested, or a version specific directory like `~/R/x86_64-pc-linux-gnu-library/3.4`
1. Create a new file called `.Renviron` in your home directory and paste in something like this:

`R_LIBS_USER="~/lib/R/library"`

You should now have a directory to download packages into:

{% highlight r %}
> .libPaths()
[1] "/home/your_username/R/x86_64-pc-linux-gnu-library/3.4"
[2] "/usr/local/lib/R/site-library"                 
[3] "/usr/lib/R/site-library"                       
[4] "/usr/lib/R/library" 
{% endhighlight %}

<!-- Dirk Eddelbuettel explains [here][debian-bug]. -->

### Lessons Learnt
I wrote this post after installing R and Rstudio - thinking I'd remember everything I'd figured out... Wrong! In future I'll make notes as I go. 

Secondly, the initial idea behind the article was to give an overview of setting up R on Ubuntu. In the end it became mainly about the specific issue covered in "Tricky bits". This is because I only found the solution while writing the article. And since this was freshest in my mind it became the main topic. I'm actually happy with this because, had I not started writing the post, I would likely have put up with this issue not being fixed.

[cran]: https://cran.r-project.org/
[RStudio]: https://www.rstudio.com/products/rstudio/download/
[so-personal-lib]: https://stackoverflow.com/questions/44861967/r-3-4-1-single-candle-personal-library-path-error-unable-to-create-na
[yt-ubuntu-r]: https://www.youtube.com/watch?v=Nxl7HDUyw0I
[yt-ubuntu-r-rstudio]: https://www.youtube.com/watch?v=kF0-FH-xBiE
[debian-bug]: https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=866768
