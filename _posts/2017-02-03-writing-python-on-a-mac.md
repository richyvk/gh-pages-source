---
layout: post
title: Writing Python code on the Mac - a basic setup
description: foo
---

A collection of things I’ve learned that set up a stable and easy to use environment for writing Python code on a Mac.

## Basics

1. Install Command Line Tools for X Code (in order to install Homebrew)<br>
[https://developer.apple.com/downloads/](https://developer.apple.com/downloads/)<br>
You’ll need an Apple ID for this.
2. Install Homebrew<br>
[http://brew.sh](http://brew.sh)
3. Install a text editor, I use (and recommend) Sublime Text 3<br>
[http://www.sublimetext.com/3](http://www.sublimetext.com/3)<br>
If you like it, you should buy a licence too :)
4. Setup Sublime Text command line tool<br>
From terminal run:<br>
```ln -s “/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl” /usr/local/bin/subl```<br>
Sublime docs recommend creating the symlink in ```~/bin/``` but I went with ```/usr/local/bin/``` [because this](http://olivierlacan.com/posts/launch-sublime-text-3-from-the-command-line/).
5. Install [Package Control](https://packagecontrol.io/) for Sublime Text<br>
[Install instructions](https://packagecontrol.io/installation). Package Control enables the installation of thousands of useful plugins.
6. Install Git for version controlling your code<br>
```brew install git```<br>
providing your ```$PATH``` looks like mine (```/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin```), this should be all you need to do to get the brewed verison of Git, rather than the default Mac OS version. You might need to restart Terminal to make the brewed version active.
7. Customise Sublime Text for Python<br>
There is a lot you can do — I recommend [Dan Bader’s book](https://dbader.org/products/sublime-python-guide/).

## Python

1. Install Python via Homebrew<br>
brew install python3<br>
providing your ```$PATH``` looks like mine (```/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin```), this should be all you need to do to get the brewed verison of Python, rather than the default Mac OS version.
2. Install virtualenv and virtualenvwrapper for managing Python environments<br>
For a quick guide see: [http://docs.python-guide.org/en/latest/dev/virtualenvs/](http://docs.python-guide.org/en/latest/dev/virtualenvs/)<br>
As the complexity of code grows virtual environments are great for managing dependencies etc. I find virtualenvwrapper much easier to use than the straight virtualenv.
3. Install iPython and Jupyter Notebooks<br>
```pip3 install jupyter```<br>
I haven’t used iPython for much other than in interactive Python shell. It can do lots more, but even the shell is a great improvement on the default Python interactive shell.<br>
[Jupyter notebooks](http://jupyter.org/) allow you to write, run, and even annotate Python code directly in your browser, and do all sorts of nice stuff after — like share your code with others. Installing Jupyter also installs iPython.

And that’s about it. This will get you up and running with writing Python code. Doing this, and then keeping things up to date and maintained, should mean you don’t have too many issues when writing.