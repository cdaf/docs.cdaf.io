# docs.cdaf.io

Static Content published via GitHub Pages, based on https://idratherbewriting.com/documentation-theme-jekyll/. For guidance on editing content see the [HDC Wiki](https://wiki.hdc.company/x/QwF3B).

# pre-requisites : Ruby Development Kit

Can only get this to run consistently on Linux

## Linux

In Ubuntu, e.g. WSL

    sudo apt update && sudo apt -y install ruby-full build-essential
    sudo gem install bundler

## Windows

> Could note get this to work

Based on https://docs.cdaf.io/mydoc_install_jekyll_on_windows.html
Download the Ruby+DevKit from http://rubyinstaller.org/downloads/ and run the ridk install with defaults, then, in Administrator console, install Bundler

    gem install bundler

## Install Dependencies and run Locally

> Do not run from WSL windows mount or the auto-detect will not work.

From Git workspace, run the application with live loading (--incremental)

    bundle update
    rm -rf _site && bundle exec jekyll serve --watch --incremental

> Some components, i.e. navbar will not refresh and need to delete the _site directory and rebuild for these