How to setup python environment on macOS
=============


On this page I describe how to setup `python` environment on **macOS Catalina (10.13)**.


## Known problems

When I upgrade to a next major version of **macOS** it's almost always some problems appear - some tools stop working, eapecially if you use your system for software development.

- [Virtual env stopped work when I upgraded python via homebrew](#virtual-env-stopped-work-when-i-upgraded-python-via-homebrew-and-)
- [Bad file permissions](#bad-file-permissions)
- [Homebrew doesn't work](#homebrew-doesnt-work)
- [Python doesn't work](#python-doesnt-work)
- [Ruby gems can't be installed](#ruby-gems-cant-be-installed)
- [How to clean unused homebrew dependencies](#how-to-clean-unused-homebrew-dependencies)


## How to setup macOS

- [Install HomeBrew](#homebrew)
- [Do system changes](#system-changes)
- [If you use mercurial](#if-you-use-mercurial)
- [Python setup](#python-setup)
  - [Python virtualenv](#python-virtualenv)
  - [Python 3 support](#python-3-support)
  - [Django completion](#django-completion)
- [Post-installation](#post-installation)
- [Useful software](#useful-software)
- [Setup OS X integration with web sites](#setup-os-x-integration-with-web-sites)
- [Read more](#read-more)

----

## Known problems

### Virtual env stopped work when I upgraded python via homebrew

How to fix a broken virtual env after python version upgrade?

I've created an alias that is easy to use every time when you upgrade the python version via homebrew, and your virtusl env becomes not working. Use it like this `fix_virtualenv <env_name>` and it will auto-fix your python version by replacing a broken links to an actual version of python.

Find the snippet in my [gist](https://gist.github.com/1st/4d8f2bd920cd047ccf1e). Find it by the name `fix_virtualenv`

### Bad file permissions

[Repair disk permissions with Disk Utility](https://support.apple.com/en-us/HT201560). It happens that permissions on some files and directories broken after upgrade to **newer version of macOS**.

Then run next command to make this directory writable:

```shell
sudo chown -R $(whoami) $(brew --prefix)/*
```

Previously it was possible to do like this `sudo chown -R $(whoami):admin /usr/local` but no anymore.

### Homebrew doesn't work

Fix issue with these commands:

```shell
xcode-select --install
cd /usr/local/Library
git pull origin master
```

You can try to find some problems by running:

```shell
brew doctor
```

### Python doesn't work

```shell
brew reinstall python
brew reinstall python@2
```

See also [list of known bugs in HomeBrew](https://github.com/Homebrew/homebrew/blob/master/share/doc/homebrew/El_Capitan_and_Homebrew.md).

### Ruby gems can't be installed

To install ruby gems, use this command:

```shell
sudo gem install -n /usr/local/bin [package]
```

where `[package]` is what you need to install (compass, bundler, etc).

### How to clean unused homebrew dependencies

Command `brew bundle dump` generates a `Brewfile` with all the packages installed by user. Dependent packages are not listed here. It allows to use this file for the next time to install all listed software wiith one command `brew bundle --force cleanup`.

```
brew bundle dump
brew bundle --force cleanup
```

----

## How to setup macOS

### HomeBrew

Before you start, open `Terminal` application and install **Xcode command-line tool**. It's required to install a lot of software on your Mac.

```shell
xcode-select --install
```

Install [HomeBrew](http://brew.sh) to have ability to install up-to-date software, like `apt-get install` in `Ubuntu`.

My list of `brew` software (use `brew install [package_name]`):
- **required**: `memcached`, `git`, `mysql`, `postgresql`, `node`, `wget`
- **optional**: `mercurial`, `mongodb`, `rabbitmq`, `zookeeper --with-python`, `boost --with-python`, `jpeg`, `libpng`


### System changes

Edit `nano ~/.profile` file and insert [this content](https://gist.github.com/1st/4d8f2bd920cd047ccf1e).

Press `Cmd + O` to save file, `Cmd + X` to exit from nano. Run in terminal `source ~/.profile` to load changes.


### If you use mercurial

Edit `~/.hgrc` and insert info about my user:

```
[ui]
username = User Name <user@gmail.com>
```


### Python setup

- `brew install python` installs `python` and `pip`
- `pip install virtualenv virtualenvwrapper`


#### Python virtualenv

If your virtual environments are broken, then you need to recreate links to the newer version of Python.

Do these two commands *for each* of your project:
```shell
# delete all broken links
find ~/.virtualenvs/my_project_name/ -type l -delete
# create new links to python
virtualenv ~/.virtualenvs/my_project_name/
```


#### Python 3 support

- `brew install python3` installs `python3` and `pip3`
- `pip3 install virtualenv virtualenvwrapper`

To create virtual environment with `python3` support you need to specify path to specific version of python.

```shell
mkvirtualenv --python=$(which python3) project_name
# you can also use my shortcut from ~/.profile (see link to file above)
mkvirtualenv3 project_name
```


#### Django completion

Add autocompletion in terminal when we type `manage.py` or `django-admin.py` and press `<tab>` button two times.

- `cd /usr/local/etc/bash_completion.d/`
- `wget https://raw.github.com/django/django/master/extras/django_bash_completion`
- `source ~/.profile` to affect changes


## Post-installation

- create virtual environments for projects `mkvirtualenv [env_name]` and run `pip install -r requirements.txt`
- restore MySQL/Postgres/MongoDB databases
  - mongodb: `mongodump --out backup/` -> `mongorestore backup/`


## Useful software

This is my list of sofrware that I use:

- From App Store: Pages, Numbers, Keynote, Pixelmator, iDraw, 1Password, The Unarchiver, Pocket
- [DropBox](https://www.dropbox.com)
- [Skype](http://www.skype.com)
- [Google Chrome](http://www.google.com/chrome)
- [SourceTree](http://www.sourcetreeapp.com)
- [MySQL Workbench](http://dev.mysql.com/downloads/workbench/)
- [Sublime Text 3](http://www.sublimetext.com/3)
- [Atom](https://atom.io)
- [VirtualBox](https://www.virtualbox.org)
- --- optional ---
- [TunnelBlick](https://code.google.com/p/tunnelblick/) - graphical OpenVPN for Mac
- [uTorrent](http://www.utorrent.com) - torrent client
- [Team Viewer](http://www.teamviewer.com/en/index.aspx) - share your screen
- [Google Music Manager](https://support.google.com/googleplay/answer/1229970) - upload music to Google Play
- [XMind](http://www.xmind.net) - save your minds in graphical representation
- [Inkspape](http://www.inkscape.org/en/) - free vector graphic tool. Require to install [XQuartz](http://xquartz.macosforge.org/landing/)
- [VLC Video Player](http://www.videolan.org/vlc/download-macosx.html)


## Setup OS X integration with web sites

- Login to [google.com](http://google.com) and auto-setup OS X to work with: mail, calendar, etc
- Login to [facebook](http://facebook.com), [twitter](http://twitter.com) and [linkedin](http://linkedin.com) and allow auto-setup OS X


## Read more

- [How to configure Atom editor on El Capitan](https://github.com/1st/python-on-osx/blob/master/ATOM.md)
- [How To Setup Ubuntu Web Server](https://github.com/1st/setup-web-server)
