---
title: Updating a Blog Theme
author: 'Matt Johnson'
date: '2021-06-14'
slug: updating-a-blog-theme
image: "img/DSCN1968_edited-1_20070804_165511_002.jpg"
categories:
  - web
  - R
tags:
  - blogdown
  - hugo
description: 'Updating the Hugo theme on a blogdown site can be intimidating, the trick is to pick a theme with good documentation and an example site.'
draft: true
---



In an effort to resurrect my long neglected `blogdown` site, I decided to switch to a new theme. There is already some excellent documentation around, especially in the [blogdown](https://bookdown.org/yihui/blogdown/other-themes.html#other-themes) book. I will not try to recreate any of that here. This is more a record of what I did and some of the small gotcha's I encountered.


## First find a good theme 

On the [Hugo website](https://themes.gohugo.io/) there are almost 300 themes to choose from. The themes website is well designed so it is easy to filter and sort through to find the theme you are after. Make sure you find one with good documentation and an example website for you to better understand how it all fits together. Not all documentation is created equally so it is worth taking the time at the start to work through it. 

Another thing to remember is that themes can have different requirements for structuring your blogs content. So also check the example website's structure to assess how much effort is required. 

In my work life I have to use a lot of pale corporate themes, and my previous theme was the wonderful [future imperfect](https://themes.gohugo.io/future-imperfect/). This time I wanted to try something darker and had a few other requirements, I wanted a theme that:

1. is responsive and looks good on a phone
2. is good for displaying photos
3. has a good simple search function
4. displays tags nicely

Eventually I decided on the [stack theme](https://themes.gohugo.io/hugo-theme-stack/) by [Jimmy Cai](https://jimmycai.com/). Some extra features that clinched the deal were:

1. ability to toggle between light and dark themes
2. local search
3. [PhotoSwipe](https://photoswipe.com/) integration
4. an archive page template
5. no built in JavaScript or CSS frameworks

This last point, I hope, will lead to less conflicts when adding `htmlwidgets` to posts.


## Import new theme 

To import the theme I just followed the [documentation](https://docs.stack.jimmycai.com/getting-started) imported the theme using git clone and then setup the folder as a sub-module.

```console
git clone https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack

git submodule add https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack
```

These are the usual instructions for adding a theme. But adding the theme as a sub-module is optional. You will need to make some changes to the contents of the theme and you will also want to keep track of these changes in git. Using the code above the sub-module points to the original source and you will not want to push your changes to this repo. After a while I removed the sub-module and added the theme to the sites repo. To do this you need to use the `git deinit` command but you also need to delete cached files from the git repo. I did this based on a [Stack Overflow answer](https://stackoverflow.com/a/26752628/1498485) which is copied below.

```console
mv themes/hugo-theme-stack themes/hugo-theme-stack_tmp
git themes/hugo-theme-stack deinit themes/hugo-theme-stack
git rm --cached themes/hugo-theme-stack
mv themes/hugo-theme-stack_tmp subfolder
git add themes/hugo-theme-stack
```


## Update the Config file

Now it is time to update your sites `config.toml` or `config.yaml` file. Remember we selected a theme that has an example website. So rename your old `config` file and copy across the one from the new theme example. Then you can go through updating the new `config` file based on the old one. With luck this will be enough to get your site running using `blogdown::build_site()` then `blogdown::serve_site()`. 


## Update site structure 

At this stage (hopefully) it becomes pretty obvious what is working and what is not. For me, the new theme had a different structure to deal with pages like `about`. Using the new `config` file and the structure of the example site I was able to adapt to this pretty easily.

The biggest issue I had came when I tried to update the page logo. This is just a `.jpg` file for both the old and new theme. It took a long time to realise that the new theme expected this file to be in the `themes/hugo-theme-stack/assets/img` folder when the old template expected it to be in `static/img`. In both cases you refer to the file using `img/logo.jpg`, so I could not understand what I was doing wrong.


# Exploring the Theme contents

It is worth having a good idea of the structure and the files in the theme. There will be lots of instances where it is best to make changes in the theme as this will cascade through the site. For example, I wanted to use [highlight.js](https://highlightjs.org/) for syntax highlighting. This can be done with 3 lines of code:

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.0.1/styles/a11y-dark.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.0.1/highlight.min.js"></script>
<script>hljs.highlightAll();</script>
```

This could be added easily enough to each post that needs syntax highlighting but if you add it to the theme it becomes available to all posts. In the `themes/hugo-theme-stack/layouts/partials/head` folder, there is a file called `script.html`. In the base theme the file is empty, it is intended to be modified. These partials are used to build the base `html` template for each page. There were also files called:

  * head.html
  * custom.html
  * style.html
  
<style>
.right {
  display: block;
  float: right;
  width: 30%;
}
</style>

<img class = "right" src="../../fav2/favicon.svg"/>

I used the `custom.html` file to include all the links needed to add a `favicon` to my site. The `svg` for the `favicon` was created in `Inkscape` then I used [RealFaviconGenerator](https://realfavicongenerator.net/) to convert to a `favicon`. This is the same service behind pkgdown's [pkgdown::build_favicon()](https://pkgdown.r-lib.org/reference/build_favicons.html) function.




## Widgets






## Add comments



## Content

add some more content


