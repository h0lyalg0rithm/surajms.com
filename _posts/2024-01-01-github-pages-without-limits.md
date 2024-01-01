---
layout: post
title: Github pages without limits
date: 2024-01-01 23:22 +0100
---
I decided to upgrade my jekyll theme for the blog to the latest version of the theme.The new version is based on the new version of jekyll wwhich is not supported by github pages, even though I would try to use the newer versions of the theme.Github pages would replace it with their an older version of the theme resulting in a broken links throughout the website.

To get around this I decided to fork the github [action](https://github.com/actions/jekyll-build-pages).
It took me a while to understand how actions are released and deployed to the github marketplace.Luckily the repository already contained  auatomated workflows to build and release new versions of the github action.

The github action is configured to download the github-pages ruby gem which contains the restrictions like allows themes and plugins which can be used with the github pages platform, since these restrictions were just validations added before the action of building the jekyll static html pages, all I had to do was get rid of those restrictions.

I have updated the action which can be just like the original github action.All you have to do is replace the github workflow name from `actions/jekyll-build-pages@v1` to `h0lyalg0rithm/jekyll-build-pages@v1`

As you can see this website now supports dark mode :rocket: .
