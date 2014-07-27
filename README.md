How to setup python environment on Mac OS X Yosemite
=============

On this page I describe how to setup `python` environment on `Mac OS X Yosemite (10.10)`.

HomeBrew
----------

Install [HomeBrew](http://brew.sh) to have ability to install up-to-date software, like `apt-get install` in `Ubuntu`.

My list of `brew` software (use `brew install [package_name]`):
- memcached
- mercurial
- git
- mysql
- postgresql
- mongodb
- rabbitmq
- node
- wget
- --- optional ---
- zookeeper
- boost --with-python
- lynx
- cairo
- jpeg
- jsoncpp
- gettext
- glib
- libpng
- log4cpp


System changes
----------

Edit `nano ~/.profile` file to have this lines:

```
# load all completions
source /usr/local/etc/bash_completion.d/*
# load virtual env wrapper
source virtualenvwrapper.sh
# Set architecture flags
export ARCHFLAGS="-arch x86_64"
# Ensure user-installed binaries take precedence
export PATH=/usr/local/bin:$PATH
# Load .bashrc if it exists
test -f ~/.bashrc && source ~/.bashrc
```

Press `Cmd + O` to save file, `Cmd + X` to exit from nano. Run this command in terminal `source ~/.profile` to load changes.

Edit `~/.hgrc` and insert info about my user:

```
[ui]
username = User Name <user@gmail.com>
```

Python tools
----------

- brew install python
- pip install virtualenv
- pip install virtualenvwrapper


Post-installation
----------

- create virtual environments for projects `mkvirtualenv [env_name]` and run `pip install -r requirements.txt`
- restore MySQL databases
- restore mongodb collections


Software
----------

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
- [TunnelBlick](https://code.google.com/p/tunnelblick/)
- [uTorrent](http://www.utorrent.com) - torrent client
- [Team Viewer](http://www.teamviewer.com/en/index.aspx) - share your screen
- [Google Music Manager](https://support.google.com/googleplay/answer/1229970) - upload music to Google Play
- --- optional ---
- [XMind](http://www.xmind.net) - save your minds in graphical representation
- [Inkspape](http://www.inkscape.org/en/) - free vector graphic tool. Require to install [XQuartz](http://xquartz.macosforge.org/landing/)
- [LVC Video Player](http://www.videolan.org/vlc/download-macosx.html)


Setup OS X integration with web sites
----------

- Login to [google.com](google.com) and auto-setup OS X to work with: mail, calendar, etc
- Login to [facebook](facebook.com), [twitter](twitter.com) and [linkedin](linkedin.com) and allow auto-setup OS X
- Login to [github](github.com) and [bitbucket](bitbucket.org)
