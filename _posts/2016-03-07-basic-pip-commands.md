---
layout: post
title: Basic PIP commands
description: foo
---

[Pip](https://pip.pypa.io/en/stable/) is a great tool for managing Python packages. If you are a Mac user and have installed Python via Homebrew (which you definitely should) then PIP will automatically be install for you. Here’s a list of useful basic PIP commands.

* ```pip install -U pip``` - this updates pip itself to the latest version. Note that it is safe to do this if you installed Python with Homebrew, upgrading your Python version with Homebrew won’t necessarily update pip.
* ```pip list``` - show all packages installed, with version.
* ```pip list -o``` - show installed packages that are not the newest version available.
* ```pip install <package_name>``` - install the latest version of a particular package.
* ```pip install <package_name>==version _number``` - install a specific version of a package.
* ```pip freeze > requirements.txt``` - standard way of preserving a list of required packages with versions for a project. It save the list of packages with versions to a requirements.txt file.
* ```pip install -r requirements.txt``` - install all packages in your requirements.txt file.
* ```pip install -U <package_name>``` - update an installed package to the latest version.
* ```pip search <keyword>``` - search for packages by keyword - sadly searching in pip seems pretty limited, e.g. no capacity to restrict search to package name.
