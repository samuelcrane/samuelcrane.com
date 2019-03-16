---
title: New Year, New Website
author: ''
date: '2019-02-23'
slug: new-year-new-website
categories: []
tags: []
Categories:
  - R
  - Data Science
Description: ''
Tags:
  - R
  - datascience
type: post
---

<img src="/post/2019-02-17-new-year-new-website_files/sarah-dorweiler-357715-unsplash.jpg" alt="image of a single green leaf on a hite background" width="100%"/>


<p class="lead">
I haven't been keeping my website up to date with my career as a data scientist and I'd love to start sharing more about the projects my team and I have been working on. I used to be on Squarespace and the thought of trying to write up R code in Squarespace's CMS was enough to keep me from just never sharing. 
</p>

No more! I've migrated over to blogdown and am hosting on Netlify. What follows is a short write up of the process and some of the custom configurations I've made. 

## What's Needed

Other than wanting to use blogdown, I didn't have a firm grasp of what tools I needed at the outset. Here were my four requirements for the project that led me to my current solution:

<ul class="fa-ul">
  <li><span class="fa-li"><i class='fab fa-r-project' style='font-size:24px'></i></span> Be able to easily post code and output. Rmarkdown is a natural fit for this, and the blogdown package makes it possible</li>
  <li><span class="fa-li"><i class='fab fa-github-alt' style='font-size:24px'></i></span> Version control through GitHub.</li>
  <li><span class="fa-li"><i class='fas fa-magic' style='font-size:24px'></i></span> Apply a theme and not worry too much about design (this was always a benefit of Squarespace). </li>
  <li><span class="fa-li"><i class='far fa-credit-card' style='font-size:24px'></i></span> Keep costs low. I'm willing to pay a small fee for hosting, but probably no more than what I was paying Squarespace. </li>
</ul>


With those requirements in mind, here's the tech stack I've ended using:

- [RStudio](https://www.rstudio.com/) for editing all content and theme files. 
- [blogdown](https://github.com/rstudio/blogdown) for integration with Hugo and R. 
- [Hugo](https://gohugo.io/), the engine that generates the static site files. 
- [GitHub](https://github.com/samuelcrane/samuelcrane.com) for hosting the website project files. 
- [Netlify](https://www.netlify.com/) for continuous deployment and hosting the website. I'm using the free tier. 
- [Hyde](http://hyde.getpoole.com/) a Jekyll theme ported to Hugo. 
- [Typora](https://typora.io/) for drafting (because I'm a monster and still start drafting outside of RStudio).
- [Google Fonts](https://fonts.google.com/) because apparently nothing is ever good enough for me and I love to fuss with fonts.
- [Font Awesome Icons](https://www.w3schools.com/icons/fontawesome_icons_brand.asp) I love these little guys.



## Process

I won't belabor a step-by-step here because there are [already](https://tclavelle.github.io/blog/blogdown_github/) [good](http://jonthegeek.com/2018/02/27/blogging-in-ten-minutes/) [blog](https://www.kencochrane.net/2016/11/20/i-rebuilt-my-blog-with-hugo-and-moved-to-netlify/) [posts](https://www.carlboettiger.info/2017/04/19/migrating-to-hugo-and-blogdown/) on the topic, and no better resource than the [blogdown book](https://bookdown.org/yihui/blogdown/) itself. Still, my process looked roughly something like this:

1. Install blogdown & Hugo 
2. Pick Hugo theme (hard!!)
3. Create a new R project for the site
4. Initialize a repo on GitHub
5. Add `public/` to gitignore
6. Connect Netlify to the GitHub repo
7. Customize and add content

That's it. It took me only the better part of one weekend afternoon to read up on it all, make a few false starts, and then get something up and running on the web. Here are some more details on the process. 

### Read the manual

Before really getting going, the very first thing I did was skim through the blogdown book. At a minimum, I'd recommend you read all of chapters 1, 2, 3, and 4. Much of it will no doubt make no sense at first (`layouts/partials/` what?) but I felt better prepared having gone through it and knew which sections to revisit once the process was underway. 

### Pick a Hugo theme

As recommended in the blogdown book, you should spend some time first picking the Hugo theme you'll use, before building the site. I took the advice to heart and spent a considerable amount of time looking through the different options and exploring the demos before settling on Hyde. This was a bit of making a decision in a vacuum, having not built a Hugo site before, but I liked the simplicity and type-forwardness of the Hyde theme. Seeing how a static-site generator like Hugo seperates content and design, I'm also confident that it will be straightforward to change themes down the road if I change my mind. 

### A note on deployment

There seems to be some consensus out there now on deploying through Netlify. I originally planned on hosting on GitHub using GitHub Pages for deployment, but it turns out that they rely on Jekyll, an alternative to Hugo. While it's possible to build a blogdown site through Jekyll (see [section 5.1](https://bookdown.org/yihui/blogdown/jekyll.html) of the blogdown site), or to trick Github Pages into serving just the blogdown/Hugo rendered pages in `public` ([section 3.3](https://bookdown.org/yihui/blogdown/github-pages.html)), I didn't want play with any of that business. If using Netlify, just be sure to put `public/` in your .gitignore, then push to your heart's content. 

I loved that I could put the website project under version control, point Netlify to the repo, and let it take care of rendering and serving the site automatically. Honestly, it's the best. 

💡 Another thing to watch out for with Netlify: You have to update the `baseURL` field in the config.toml file to match the URL of your site (the default is "www.example.com"), otherwise none of your precious Hugo theme will apply. Unless you are rolling with a custom domain right out of the gate, the way Netflify works is that it assigns you some random url, which you won't know until after your first deploy. So, you'll have to go back and update your config file once you know your URL. Like I did here in commit [b80b984](https://github.com/samuelcrane/samuelcrane.com/commit/b80b9843ac4e9e3c7b19765ab8f3066bb77a13bc).

### Customize the theme

As good as the Hyde theme is, I wanted to modify certain aspects. Here's some of the changes I made. 

- Imported additional Google Fonts in `themes/hyde/layouts/partials/head_fonts.html`
- Made various changes to the CSS. I made most CSS changes in a new `themes/hyde/static/css/custom.css` file. I'm not expecting to pull in a ton of updates to the Hyde theme, but not making many modifications to the provided theme files ought to help with maintainance. 
- Created new page type templates in `themes/hyde/layouts/`. Specifically, I wanted the "About Me" and "Talks" pages to behave differently than a blog post (i.e., not display the date of the post and supress the title given in the config). To do this, I needed to make new layouts. I went down a rabbit hole here, learning about how Hugo themes work and about Hugo's order of execution for rendering pages. The most helpful resource was this blog post, [Hugo's Directory Structure Explained](https://www.jakewiesler.com/blog/hugo-directory-structure/), where I learned more about the page type templates. You should explicitly define the templates for each content type on your site. 

## Resources

Here are some of the resources I found helpful. 

- [blogdown: Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/)

- [Hugo’s Directory Structure Explained | Jake Wiesler](https://www.jakewiesler.com/blog/hugo-directory-structure/)

- [Complete List | Hugo Themes](https://themes.gohugo.io/)

*— Samuel*
<hr>


<span style="display:inline-block;padding:2px 3px"><svg xmlns="http://www.w3.org/2000/svg" style="height:10px;width:auto;position:relative;vertical-align:middle;top:2px;fill:black" viewBox="0 0 32 32"><path d="M10 9V0h12v9H10zm12 5h10v18H0V14h10v9h12v-9z"></path></svg></span><span class="figcaption">Lead photo by [Sarah Dorweiler](https://unsplash.com/@sarahdorweiler) on Unsplash</span>  







