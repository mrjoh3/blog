---
title: Another blog about a blog
author: Matt Johnsom
date: '2018-07-20'
slug: another-blog-about-a-blog
categories: ['web']
tags:
  - hugo
  - blogdown
  - rstats
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
---

Having decided to write a blog I needed something to write about. The purpose of this blog will be to link up various projects I work on and to share code and ideas. 

Currently I mostly work with `R` and use it for statistics, modelling, GIS and web based reporting. Therefore the choice of `Blogdown` as a platform seemed simple enough. You will find many existing posts about others setting up their blogs in a similar way. Further, [blogdown: Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/) covers everything you need to know about the process. Here, I am only going to discuss the few specific things I needed to worry about to get started.

## Choosing a Theme and Installing

There are many themes available at [Hugo Themes](https://themes.gohugo.io). This one is called [Hugo Future Imperfect](https://github.com/jpescador/hugo-future-imperfect) by [Julio Pescdor](https://github.com/jpescador). Once you have chosen it is time to begin. Themes are loaded directly from their github repositories so you will need the themes github username and repository name.

```r

install.packages("blogdown")
blogdown::install_hugo()

blogdown::new_site(theme = "jpescador/hugo-future-imperfect")

```

Now everything is up an running but it is easier to test everything if you have some content. The `Blogdown` package includes a series of addins that makes this process simple, just select `New Post` from the `Addins` menu.

![new post screenshot](/post/2018-07-20-another-blog-about-a-blog_files/new_post.png)


## Configuring the Site

With some simple content generated use `blogdown:::serve_site()` to preview your site. At this stage it will not look exactly as you expected. Each theme has a `config.toml` that is used to setup each site. Most themes will have detailed instructions or an [example project](https://github.com/jpescador/hugo-future-imperfect/blob/master/exampleSite/config.toml) for your reference. This file is quite readable so you can just copy the settings you need. 

Be sure to read any documentation that comes with the theme as they are all different and may have some simple gotcha's. Here the CSS did not want to load until I found that I had to add the setting `relativeURLs = true`. Also play around with all the settings in the `config.toml` file just so you know what they do.


## Deploying 

`Hugo` generates static sites so there are many deployment options. The simplest is to run `blogdown::build_site()` and then copy the contents of the `public` folder to your hosting service. I won't go thoughthem as the `blogdown` book mentioned above goes into great detail. 

As I am too cheap to pay for a hosting service but and want to make use of my github pages url I am using Github and Travis. Again, refer to the blogdown book for instructions. The only trick was linking the github repo with travis with permissions to write back to the repo. [This post](https://medium.com/zendesk-engineering/how-to-create-a-website-like-freshswift-net-using-hugo-travis-ci-and-github-pages-67be6f480298) contained all the details necesary for setting an environment variable in Travis.

This worked nicely **BUT**... 


## Actually Deploying

When travis builds the site it runs `blogdown::build_site()` just as you would on your computer. Now if you have an `.Rmd` post that uses packages, they are installed on your computer but they are not on Travis. Travis can be configured to install the packages, but you will have to do this each time you add use a new package. And this seems like a lot of effort when you can simply build the site locally and move thje static files.

After several dead-ends and messing around with folder names to appease the Github gods (the were not appeased), I came across instructions on the [GoHugo website](https://gohugo.io/hosting-and-deployment/hosting-on-github/#github-user-or-organization-pages). This involved creating 2 repositories one called `blog` and the other `<USER>.github.io` and then setting up the public folder of `blog` as a git-submodule that commits to `<USER>.github.io`.

The only drawback is that if you use the git GUI in RStudio the sub-module does not commit. But this is likely user error as my knowledge of git is limited. For now I am using the terminal to push changes in the public folder.



```bash

# run once
git submodule add -b master git@github.com:mrjoh3/mrjoh3.github.io.git public

cd public

git pull

# after updates
git add .
git commit -m 'some message'
git push origin master

```