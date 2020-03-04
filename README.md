# Overview

Template for github blog hosting.

Use Technology:

1. bootstrap for cascade sheet styling
1. jekyll for static content generation

Has Features:

1. feed support
1. bootstrap theme support
1. poster support
1. post category support
1. github metadata support
1. github comments to post integration

# Setup

1. Fork and Clone the repository. More information [here](https://help.github.com/en/github/getting-started-with-github/fork-a-repo). To host the repo at root url, the repository name must be `<your username>.github.io`.
1. Delete my `master` branch in local and remote.
   ```bash
   git branch -D master  # deletes local master
   git push -d origin master  # delete remote master
   ```
1. Create your `master` branch in local and remote.
   ```bash
   git checkout -b master  # creates local master
   git push --set-upstream origin master  # creates remote master
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

# Todo list

Todo list is [here](TODO.md).
