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
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
draft: true
---

<link rel="stylesheet" href="../../highlight/a11y-dark.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.0.1/highlight.min.js"></script>
<script>hljs.highlightAll();</script>


In an effort to resurrect my long neglected `blogdown` blog, I decided to switch to a new theme. There is already some excellent documentation around, especially in the [blogdown](https://bookdown.org/yihui/blogdown/other-themes.html#other-themes) book. I will not try to recreate any of that here. This is more a record of what I did and some of the small gotcha's I encountered.

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


## Import new theme as a submodule

To import the theme I just followed the [documentation](https://docs.stack.jimmycai.com/getting-started) imported the theme using git clone and then setup the folder as a submodule.

```console
git clone https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack

git submodule add https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack
```


update the config. file


will be working here

may need to change structure for set pages like "about"

files like "logo" may need to be added to the theme!!

get widgets working...

add some more content


## Add comments