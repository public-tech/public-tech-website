# Template Website [![CircleCI](https://circleci.com/gh/public-tech/public-website.svg?style=svg)](https://circleci.com/gh/public-tech/public-website)

This repo contains your public website.

As well as the website code, you have a fully working Continuous Integration (CI) pipeline (we use CircleCI).

## Pre-requisites

You need a Mac.

You need to [install](https://brew.sh/) `homebrew` on your Mac.

You need to have `git` installed (`brew install git`).

## Getting started

### Dependencies used by this repo

We use `hugo` to template the website.

We have our own hugo theme which you need to install (see below).

We use netlify to build and host the site.

### Steps to run locally

You will need clone this repo to your local machine. Currently, running on OSX (Mac) is the only supported platform.

You can clone the repo by copying the `git:` clone link on the top right of this page and then in a terminal, navigate to where you keep code on your laptop, then:

```shell
git clone <clone url>` where `clone url` is the contents of your copied clone link.
```

Then you should navigate into the repo with:

```shell
cd public-website`
```

Firstly, you need to make all the script files in this repo executable, so go to a terminal and run:

```shell
find . -name "*.sh" -maxdepth 1 -exec chmod +x {} \;
```

#### Install dependencies on OSX (available as `osx_install.sh`)

In a terminal, run:

```shell
./osx_install.sh
```

This will install all the dependencies that you need so you can develop locally.

You need to fetch our website theme. To do this, open a terminal and run (in the root repo dir):

```shell
./fetch_theme.sh 0.0.1
```

This will install our theme into `website/themes/fylo`.

If a new version of the theme is released, then you can fetch it locally by running this script with the new version number.

If you want to update the version of the theme that is used in your stage or production website, then you will need to change the `THEME_VERSION` environment variable on your build.

#### Editing your website

- You should only need to edit `config.toml` and files in `static` or `layouts`.

- *DO NOT* edit any files in `themes/fylo`. Any changes you make to the theme will be lost if you install an update to the theme.

- We have added `layouts/partials/hero.html` and `static/js/main.js` as examples of files that override their equivalents in the `themes/fylo` directories. If you need to, you can add any further override files into the top level folders of your website.

- You can decide which sections are shown in the website by editing `config.toml`.

- You can decide how things should look by adding override files.

#### Developing on your local machine

You need to navigate into this repo `website` directory (assuming you are in `place/where/you/keep/code/public-website`):

```shell
cd website
```

From here you can start a local webserver:

```shell
hugo server -D
```

 This will start a webserver locally ( go [here](http://localhost:1313) ) and will watch for any changes to your files.

When you have made the changes you want, you can then commit the changes using `git` and push to your repo.

## CI

The CI pipeline is already configured:

- If you push changes to a `staging` branch, then your changes (if successful) will be automatically deployed to your `staging` environment. This is found [here](https://staging--public-tech.netlify.com).

- If you push changes to the `master` branch, then your changes (if successful) will be automatically pushed to your `production` environment.  This is found [here](https://public-tech.co).

- In all other cases, your changes will be built and tested, but not deployed.

### website

This directory contains your website code.

### fetch_theme.sh

Run this script to fetch the theme for the website.
You must pass it the version of the theme that you want to install:

```shell
./fetch_theme.sh 0.0.1
```

### osx_install.sh

This file can be used if you are developing on OSX (Mac). Running this script will install all the things that you need to maintain your website.

To run the script, go to a terminal, navigate to this folder and then run:

```shell
./osx_install.sh
```

### test.sh

This file contains a simple smoke test to make sure your deployment works. You can run this locally, but it is also run on CI.
