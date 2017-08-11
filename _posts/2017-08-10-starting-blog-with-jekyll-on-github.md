---
layout: post
title: "Start blogging with jekyll on github"
date: 2017-08-10
tags: jekyll github blog
---

GitHub docs say that in order to preview my jekyll blog locally by [setting up github pages locally with jekyll]( https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#requirements):

> We recommend using Bundler to install and run Jekyll. Bundler manages Ruby gem dependencies, reduces Jekyll build errors, and prevents environment-related bugs. To install Bundler, you must install Ruby.

I didn't want to install that software at present since I have no immediate plans to study Ruby (my current priority is python and django).

Instead I followed this excellent tutorial by JONATHAN MCGLONE: [Creating and Hosting a Personal Site on GitHub](http://jmcglone.com/guides/github-pages/) and was able to get the blog up using only git and my normal editor on my local system.

One odd note: even though GitHub supports Markdown for repository files (like README.md) they evidently now only support kramdown for _GitHub Pages_. Here is the text of an automatic email I was sent from GitHub support when I first configured my _config.yml to use markdown:

> The page build completed successfully, but returned the following warning for the `master` branch:

> You are currently using the 'markdown' Markdown engine, which is no longer supported by GitHub Pages and may cease working at any time. To ensure your site continues to build, remove the 'markdown' setting in your site's '_config.yml' file and confirm your site renders as expected. For more information, see https://help.github.com/articles/updating-your-markdown-processor-to-kramdown/.
