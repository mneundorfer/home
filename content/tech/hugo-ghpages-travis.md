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

Okay, now we've got it all. Just write your content, compile beautiful HTML and CSS with Hugo, and then - take the output, and commit it to your GitHub page. Right? Well, you can do that. But really, there are better ways. For starters, you can leverage [Travis CI](https://travis-ci.org/) - and for open source projects, its free!

## Travis Setup

First of all - if not already done - sign up using your GitHub account.

Then go to the `Profile` view and activate the repository from which you would like to build your page. By default, Travis sees all your public projects, but you have to enable them seperately.

Then, within the settings for the activated repository, create a new environment variable named `GITHUB_TOKEN`. This then will be passed as secret variable to the build container. Now this needs to be filled with an actual token to allow Travis accessing the repository. Generate it [here](https://github.com/settings/tokens/new), the `repo` scope should do it.

## GitHub Repo Setup

Travis is set up and waiting for work to do. Just place a file named `.travis.yml` in the root of your repo: It is the configuration file for Travis and will be picked up automatically.

```
language: go

# This gets the latest Go version from master
go:
  - master

# Install the latest Hugo - you could also just add the binary 
# to your repo, but I like to keep that clean
install:
  - go get github.com/spf13/hugo

# Here's the actual work: Build your static pages
script:
  - hugo

# Here is what finally happens:
# Using the pages provider, just get what has been compiled into public
# (the default Hugo output folder) and push it to the given repo on
# branch master, using the given token
deploy:
  provider: pages
  skip_cleanup: true
  repo: {user}/{user}.github.io
  target_branch: master
  local_dir: public
  github_token: $GITHUB_TOKEN
  on:
    branch: master
```

Also, the `{user}/{user}.github.io` repo has to be created, if not done yet.

Now, when `push`ing to your `master` branch, the CI pipeline (which here does nothing but generate static pages and push them to another repository) will be triggered.