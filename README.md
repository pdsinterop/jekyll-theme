# PDS Interop Jekyll Theme

[![license](https://img.shields.io/github/license/pdsinterop/jekyll-theme.svg)](LICENSE)
[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

_Jekyll theme for all PDS Interop sites using GitHub Pages_

GitHub use [Jekyll](https://jekyllrb.com/) to generate a static website for any
repositoy that has enabled [the "GitHub Pages" feature](https://docs.github.com/en/github/working-with-github-pages/about-github-pages).

This repository contains a theme that is meant to be used by all PDS Interop
projects that use GitHub Pages to host their contents. The theme used is a
customized version of [Just the Docs](https://pmarsceill.github.io/just-the-docs/)
called [Extend the Docs](https://github.com/Potherca/extend-the-docs).

The easiest way to use this theme is through the [Jekyll remote theme feature](https://github.com/benbalter/jekyll-remote-theme).

## Install

To use this theme:

1. Enable Github Pages
2. Configure Jekyll

## 1. Enable Github Pages

Before a repository can publish a website, the GitHub Pages feature needs to be
enabled. This is done by [configuring a build source](https://docs.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
for the website:

1. Navigate to the site's repository.

2. Under the repository name, click  Settings.
![Repository settings button](https://docs.github.com/assets/images/help/repository/repo-actions-settings.png)

3. Under "GitHub Pages", use the Source drop-down menu and select a publishing source.
![Drop down menu to select a publishing source](https://docs.github.com/assets/images/help/pages/publishing-source-drop-down.png)

GitHub will now publish any Markdown file as HTML using the ["Primer" Jekyll theme](https://github.com/pages-themes/primer)
by default. A different theme can be used by configuring Jekyll.

## 2. Configure Jekyll

For the website hosted by GitHub Pages to use this repository as a theme, Jekyll
must be told to use it. This is done by configuring Jekyll through a
`_config.yml` file.

As soon as the `_config.yml` file is part of the source that has been configured
as the source for GitHub Pages, the repository website will use this theme.

The following settings are recommended:

```yml
---
# Repository specific settings
#
# THESE SHOULD BE CHANGED TO MATCH THE REPOSITORY
#
baseurl: "/repository-name"
description: "Repository description goes here"
repository: "pdsinterop/repository-name"
title: "Repository Title"

# Organisation-wide settings
logo: "https://avatars3.githubusercontent.com/u/65920341"
remote_theme: "pdsinterop/jekyll-theme@theme"
url: "https://pdsinterop.org"

# Extend the Docs settings
nav:
  exclude:
    - "/"
  recurse: true
  cross_repository:
    show_homepage: true
    show_archived: false

# Just the Docs settings
aux_links:
  "PDS Interop on GitHub":
    - "https://github.com/pdsinterop"
search_enabled: true
```

### 3. Commit and push the file

## Usage

The most common use-cases (how to exclude documents from being build as web page
and how to exclude a web page from the navigation) are described below.

For other configuration details, please visit the config documentation of:

- [Extend the Docs](https://pother.ca/extend-the-docs/)
- [Jekyll](https://jekyllrb.com/docs/configuration/)
- [Just the Docs](https://pmarsceill.github.io/just-the-docs/docs/configuration/)

### Excluding documents from the website

Any files that should not appear as document in the website should be set in the
root of the `_config.yml` file:

```
exclude:
- "document/to/exclude.md"
```

### Excluding pages from the navigation

Documents that should be rendered as a web-pages but should not appear in the
navigation menu, should be set in the `nav` section of the `_config.yml` file:

```
nav:
  exclude:
    - "page/to/exclude/"
```

## Implementation details

This repository was created with a separate orphan branch for each element that
is combined into the PDS Interop Jekyll theme.

Each branch is then merged into the `theme` branch which can be used elsewhere.

This, the `master` branch, contains PDS interop specific files, config and docs.

The exact commands that were run are:

```sh
git init && git commit --allow-empty --allow-empty-message -m '' && git tag -sam ''  v0.0.0

git checkout --orphan extend-the-docs
git remote add extend-the-docs https://github.com/Potherca/extend-the-docs.git
git fetch extend-the-docs
git merge --allow-unrelated-histories extend-the-docs/master

git checkout --orphan just-the-docs
git remote add just-the-docs https://github.com/pmarsceill/just-the-docs.git
git fetch just-the-docs
git merge --allow-unrelated-histories just-the-docs/master

git checkout --orphan theme
git merge --allow-unrelated-histories just-the-docs
git merge --allow-unrelated-histories -X theirs extend-the-docs
git merge --allow-unrelated-histories -X theirs master
```

<!--
@TODO:

## Contributing

## License

-->
