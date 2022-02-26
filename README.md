# docs.cdaf.io

Static Content published via GitHub Pages, based on https://idratherbewriting.com/documentation-theme-jekyll/

# pre-requisites : Ruby Development Kit

Based on https://docs.cdaf.io/mydoc_install_jekyll_on_windows.html

## Windows

Download the Ruby+DevKit from http://rubyinstaller.org/downloads/ and run the ridk install with defaults, then, in Administrator console, install Bundler

    gem install bundler

## Linux

In Linux, e.g. WSL

    sudo apt-get install ruby-full build-essential
    sudo gem install bundler

## Install Dependencies and run Locally

From Git workspace, run the application with live loading (--incremental)

    bundle update
    bundle exec jekyll serve --incremental

> Some components, i.e. navbar will not refresh and need to delete the _site directory and rebuild for these