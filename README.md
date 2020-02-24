# Overview

Template for github blog hosting.

Use Technology:

1. bootstrap for cascade sheet styling
1. jekyll for static content generation

Has Features:

1. feed support
1. bootstrap theme support
1. post category support
1. github metdata support

# Setup

1. Fork and Clone the repository. More information [here](https://help.github.com/en/github/getting-started-with-github/fork-a-repo).
1. Delete my `gh-pages` branch in local and remote.
   ```bash
   git branch -D gh-pages  # deletes local gh-pages
   git push -d origin gh-pages  # delete remote gh-pages
   ```
1. Create your `gh-pages` branch in local and remote.
   ```bash
   git checkout -b gh-pages  # creates local gh-pages
   git push --set-upstream origin gh-pages  # creates remote gh-pages
   ```
1. Create `_posts` folder and start blogging. Happy blogging.
   ```bash
   mkdir _posts
   ```

# How To Guides

`coming soon`

# Local Deployment

1. Install jekyll (along with ruby). More information [here](https://jekyllrb.com/docs/installation/).
1. Install jekyll feeds plugins.
   ```bash
   gem install jekyll-feed
   ```
1. Serve the contents.
   ```bash
   jekyll serve --config _config.yml,_local.yml
   ```
