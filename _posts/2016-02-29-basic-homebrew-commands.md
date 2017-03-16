---
layout: page
title: Basic Homebrew commands
description: foo
---

If you use a Mac you should definitely have a look at installing Homebrew. It’s a great way to install and manage additional applications in a safe and self-contained way.

Once Homebrew is installed and running it’s a very good idea to keep it up to date. Here’s a list of useful basic commands to do just that.

* ```brew update``` - this updates Homebrew itself, do this before doing anything else with Homebrew.
* ```brew doctor``` - this is homebrew’s self-diagnostics tool. It will tell you if anything is wring with your Homebrew install. Do this after running brew update.
* ```brew list``` - shows all the packages you have installed.
* ```brew outdated``` - shows any packages you have installed that are not the newest version available.
* ```brew upgrade``` - install latest versions of all outdated packages.
* ```brew upgrade <package_name>``` - upgrade a specific out of date package.
* ```brew pin <package_name>``` - prevent a particular package from being upgraded when you run brew upgrade.
* ```brew unpin <package_name>``` - remove pinned package from being protected from brew upgrade.