---
layout: post
title:  "Creating a New Blog on GitHub Pages!"
date:   2025-01-26 23:45:00 -0500
categories: 
  - jekyll 
  - blog
---

First post here is about the setup, since that in itself was a bit of a journey.

First of all, you need a GitHub account. Secondly, you need to setup a repo. 
Read the [Quickstart for GitHub Pages](https://docs.github.com/en/pages/quickstart) for specifics on how to do this.
You will need to create a repo with the name `USERNAME.github.io` replacing `USERNAME` with your GitHub account username.
This will create your pages site at `https://USERNAME.github.io`.

Next, if you want a custom domain name, you can buy one, CNAME to your git, then setup
the CNAME on your site. (They recommend you verify your domain name first.) For more on this, 
read [About custom domains and GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages).

To setup your Jekyll site, you have a couple options. You can either clone someone else's (like [mine](https://github.com/pastanton/pastanton.github.io)), modify it, and 
then push it up to your repo, or you can generate one with ruby then push it up
yourself. I did this on macOS, and the instructions are here: [Jekyll on macOS](https://jekyllrb.com/docs/installation/macos/)

There are a few big changes that you will need to make before this will be fully functional. You will need to modify your `Gemfile` and `_config.yml`.

For `Gemfile`, you will need to add the following line:

```
gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins
```

Additionally, you're limited to the plugins found on the [Dependency versions](https://pages.github.com/versions/) page.

If you want to use the latest minima theme (or really any newer one), 
you'll need to change your `_config.yml` based on the theme. To add the latest 
minima theme, remove the `theme` and add this:

```yaml
remote_theme: jekyll/minima
plugins:
  - jekyll-remote-theme
```

You'll also need to read the docs to see how to setup your `config.yml` file.
The [Minima README.md](https://github.com/jekyll/minima/blob/master/README.md) is
pretty helpful.

And then after some trial and error, I have a free blog now.