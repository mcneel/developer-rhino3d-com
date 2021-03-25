# developer.rhino3d.com

[![Build Status](https://travis-ci.com/mcneel/developer-rhino3d-com.svg?branch=master)](https://travis-ci.com/mcneel/developer-rhino3d-com)

This repo contains the contents of https://developer.rhino3d.com.
The site is built by [Travis CI](https://travis-ci.com/mcneel/developer-rhino3d-com) using [Jekyll](http://jekyllrb.com/) (a static site generator) and hosted on [GitHub Pages](https://pages.github.com/).

Pull requests are welcome! :tada: Please read our guide on [Contributing](https://github.com/mcneel/developer-rhino3d-com/blob/6/CONTRIBUTING.md). If you want to build the site yourself, to test your changes before opening a pull request, then please check out the [Getting Started](#getting-started) guide below.

## Getting started

These instructions cover running this project locally on both macOS and Windows so that you can preview changes.

First, navigate somewhere safe and clone the repository.

```bash
git clone https://github.com/mcneel/developer-rhino3d-com.git
```

If you are not comfortable using git on the command-line, then check out the [git cheat sheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf) or try [GitHub Desktop](https://desktop.github.com).

### Branches

:warning: _**DO NOT PUSH TO THE `gh-pages` BRANCH!** The site is branch-aware and automatically deployed by [Travis CI](https://travis-ci.com/mcneel/developer-rhino3d-com)._

The current (_stable_) version of Rhino is defined in the `stable:` field in the `_config.yml` file.  The `n` branch that corresponds to the stable release is built and deployed to http://developer.rhino3d.com.  

The `master` branch represents the WIP version of the site.  Changes to the `master` branch will be built by Travis and deployed to http://developer.rhino3d.com/wip.  

Branches are defined in `_config.yml` (under `version_branches`) and will be built and deployed into a subpath with the same name; for example: the `5` branch is built and deployed to http://developer.rhino3d.com/5.

### Installing Ruby

See [Jekyll's official guides](https://jekyllrb.com/docs/installation/) for [macOS](https://jekyllrb.com/docs/installation/macos/) and [Windows](https://jekyllrb.com/docs/installation/windows/).

### Installing Jekyll and plug-ins

```bash
cd developer-rhino3d-com

gem install bundler

# script for macOS
./script/bootstrap

# manual method for Windows
bundle install
```

### Running the server locally

You can now serve your local copy of this site by running the `server` script.

```bash
./script/server
```

_**Note**: The `api/*` subdirectories are excluded when previewing the site locally which speeds things up a bit!_

## What next?

Once you have cloned or forked this repository and are able to build it locally, please read the following guides:

- [How This Site Works](http://developer.rhino3d.com/guides/general/how-this-site-works/)
- [Developer Docs Style Guide](http://developer.rhino3d.com/guides/general/developer-docs-style-guide/)
