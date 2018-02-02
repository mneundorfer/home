---
title: "Static GH Pages with Hugo and TravisCI"
date: 2018-01-18T20:23:22+01:00
draft: false
tags: ["hugo", "travis", "gh-pages"]
---

After a few tries in the last couple of years to establish an own homepage/blog, I learned about [Hugo](https://gohugo.io/) and GitHub pages from a colleague at work. And after playing around a little bit, I really liked the idea of using static pages for that exact purpose. And again, Hugo really is a great tool! Nevertheless, I did not find it that trivial, to get the whole setup of how to really just write some Markdown on your machine, and having some magic happening until your compiled page appears under your custom domain. That's why I took a few notes to that...

# Hugo to the Rescue

Hugo makes it really easy to come up just with some content, and then having someone else care about the visualization. Basically, you just throw some Markdown at it, tell him about one of [multiple themes](https://themes.gohugo.io/) to use, and have it spit out your final page. Since there are plenty of tutorials on how to use it (and also, it really is not that complicated - at least the basic use cases) I leave you with that.

# Use your GitHub

Since people are already using GitHub to [organize their life](https://dev.to/und0ck3d/organizing-your-life-using-github-6an), why not use it for hosting your website? [GitHub Pages](https://pages.github.com/) is the feature you are looking for. It takes your web page and just hosts it. And since we already got that page from Hugo...!

# Let Travis do the Work

Okay, now we've got it all. Just write your content, compile beautiful HTML and CSS with Hugo, and then - take the output, and commit it to your GitHub page. Right? Well, you can do that. But really, there are better ways.