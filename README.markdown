
# Installing Mac

## What and Why

This is a step by step guide which was written by me for myself mostly, with
the intent to use and update it whenever I install a new mac.

<a name=top></a>
## Backup

- SSH keys
- GPG
- Project configs
- gitconfig.secret
- Wallet
- Github API Key
- Heroku Key

## Contents

* [AppStore](#appstore)
* [3rd party](#3rdparty)
* [Keychains](#keychains)
* [Preview signatures](#preview)
* [Skype history transfer](#skype)
* [Copy Files](#files)
* [Preferences](#preferences)
* [All Descktops Apps](#alldesktopapps)
* [Homebrew](#homebrew)
* [/etc git](#etc)
* [Postfix](#postfix)
* [ZSH](#zsh)
* [Fonts](#fonts)
* [Dot files](#dotfiles)
* [gitconfig](#gitconfig)
* [ssh](#ssh)
* [Dotvim](#dotvim)
* [Rbenv](#rbenv)
* [Heroku](#heroku)
* [Nodejs](#nodejs)

<a name=appstore></a>
## AppStore

Login into the AppStore, go to "Purchases" and download all relevant apps.

In particular make sure to install Xcode.

<a name=3rdparty></a>
## 3rd party

### Useful apps:

- Numi, MacDown, Viettien Dict, Franz, GoTiengViet, BitDefender, Pdf Exert, Dash, The Unarchiver, TogglDesktop, Twist, Tomato One, Viber, Zoom

### Developer Tools
* [Xcode](https://developer.apple.com/download/more/)

### General
* [Dropbox](https://www.dropbox.com)
* [1Password](https://agilebits.com/onepassword)

  > IMPORTANT: Make sure Dropbox finished sync before you open your 1password keychain!

* [Google Chrome](http://www.google.com/chrome/)
* [Google Drive](https://drive.google.com/start)
* [Skype](http://skype.com)
* [iTerm2](http://www.iterm2.com)

  - in Settings/Terminal set 'Unlimited scrollback'
  - Turn on Prompt before closing
  - Map Cmd+S to save in Vim: Preferences > Keys, Add shortcut Cmd + s to 0x117 (F6)
  - Create n1->n4 profile with random tab colors

* [GitX](http://gitx.laullon.com)

  After that go to menu `GitX/Enable Terminal Usage...` to enable terminal `gitx` command.

* [Fork-git](https://git-fork.com/)

  After that go to menu `GitX/Enable Terminal Usage...` to enable terminal `gitx` command.

* [Postgress.app](http://postgresapp.com)

  To create postgres user without a password like in 'regular' postgres installation:

        createuser --no-password -h localhost postgres
        echo /Applications/Postgres.app/Contents/MacOS/bin | sudo tee /etc/paths.d/postgres

* [SequelPro](http://www.sequelpro.com)
* [VLC](http://www.videolan.org/)
* [Wunderlist](https://www.wunderlist.com/)
* [Stanza](http://www.lexcycle.com)

  > Note: site seems to be down. copy from old computer's Applications folder
  > instead

* [Calibre](http://calibre-ebook.com)

  Choose ~/Dropbox/books as the library location

* [Evernote](https://evernote.com/) & [Skitch](https://evernote.com/intl/vi/products/skitch)

[top](#top)<a name=keychains></a>
## Keychains

Copy files from `~/Library/Keychains/`. rename them with some common prefix
like name of the old computer.

[top](#top)<a name=preview></a>
## Preview signatures

 Copy
 `~/Library/Containers/com.apple.Preview/Data/Library/Preferences/com.apple.Preview.signatures.plist`
 from the old computer.

 The keychains from the previous step should let you open it.

[top](#top)<a name=mysql></a>
## MySQL

* Download 64bit Community Server DMG archive from [MySQL](http://mysql.com).
* Mount it
* install 3 components:
  * mysql
  * MySQL.prefpane
  * MySQLStartupItem
* setup paths:

        echo /usr/local/mysql/bin | sudo tee /etc/paths.d/mysql
        echo /usr/local/mysql/man | sudo tee /etc/manpaths.d/mysql

### Library not loaded: libmysqlclient.18.dylib

If you get this error the magic incantation to fix it is this:

    sudo install_name_tool -change libmysqlclient.18.dylib /usr/local/mysql/lib/libmysqlclient.18.dylib /usr/local/rvm/gems/ruby-1.9.3-p286-falcon/gems/mysql2-0.2.13/lib/mysql2/mysql2.bundle

> NOTE: you need to use your real mysql2.bundle path. to find it out do:

    gem which mysql2

[top](#top)<a name=files></a>
## Copy Files

Copy the following files over:

* `~/Documents/`
* `~/Downloads`
* `~/Desktop/`
* `~/bin/`

  add `~/bin` to the path:

        echo ~/bin | sudo tee /etc/paths.d/home-bin

[top](#top)<a name=preferences></a>
## Preferences


Go to system preferences and adjust the following:
* Accessability

  Enable dragging with Drag Lock on "Mouse & Trackpad/Trackpad Options" with three fingers

* Mission Control

  uncheck "Automatically rearrange spaces based on most recent use"

  uncheck "When switching to an application, switch to a space with open windows for the application"

* TimeMachine

  Exclude directories from TimeMachine backup

       sudo tmutil addexclusion -p ~/.dropbox
       sudo tmutil addexclusion -p ~/Dropbox
       sudo tmutil addexclusion -p ~/Google\ Drive/
       sudo tmutil addexclusion -p ~/Downloads/
       sudo tmutil addexclusion -p /usr/local/Cellar
       sudo tmutil addexclusion -p /usr/local/rvm

* Language & Text

  select required input sources

* Security & Privacy

  disable password reset through Apple ID

  turn on "File Vault"

  turn on Firewall

* Keyboard
  * Key speed, Delay until repeat: Max
  * in "Modifier Keys" popup switch "Caps Lock" to "Esc"
  * Text tab:
	   * Uncheck auto capitalize
  * Keyboard Shortcuts:
      * turn off "Show Spotlight Window" in spotlight group and

* Trackpad

  check "Tap to Click"

* Mail, Contacts & Calendars

  Setup GMail account

[top](#top)<a name=homebrew></a>
## Homebrew

* Install Xcode command line tools from Xcode Preferences' Downloads tab.
* Install [Xquartz](http://xquartz.macosforge.org/) of at least version 2.7.2
  > NOTE: VERY important to install Xquartz before Homebrew.
* Install [Homebrew](http://mxcl.github.com/homebrew/).
* brew install macvim git wget imagemagick aria2 dos2unix watch tree pstree neovim
* brew install tmux mtr iftop htop-osx gpg2 ctags
* brew install erlang md5deep ack s3cmd unrar tig the_silver_searcher hub
* brew install clojure clojure-contrib leiningen
* brew cask install diffmerg java
* brew tap heroku/brew && brew install heroku
* brew install the_silver_searche

[top](#top)<a name=etc></a>
## /etc git

    sudo su -
    cd /etc/
    git init
    chmod 700 .git
    git add .
    git commit -m initial

[top](#top)<a name=postfix></a>
## Postfix

> UPDATE: I just installed a new Air laptop and it had the directories in the
> main.cf file pointing to the old location, so there was no need to do any of
> this... To check do `grep data_directory /etc/postfix/main.cf`. IF it points
> to /Library/... then you might need to do the fixes below.

If you upgraded from Lion your Postfix config is most probably broken.
The upgrade changes /etc/postfix/main.cf to point to a new set of postfix
directories but leaves the old directories at their old place.

> Note: I expect ML upgrade process to be soon fixed to handle this so at some
> point in time those steps should become unnecessary

to verify the new directory locations:

    ls /Library/Server/Mail/Data/spool
    ls /Library/Server/Mail/Data/mta

check the old directory locations:

    ls /var/spool/postfix
    ls /var/lib/postfix

Lets move the directories to their new place (if needed):

    sudo mkdir -p /Library/Server/Mail/Data
    sudo mv /var/spool/postfix /Library/Server/Mail/Data/spool
    sudo mv /var/lib/postfix /Library/Server/Mail/Data/mta

Start the Postfix daemon

    sudo postfix set-permissions
    sudo postfix start

`set-permissions` might complain about missing man pages. the problem is that
the new `postfix-files` file has the man pages with `.gz` extension, but they
were not compressed during the upgrade.

To fix:

    d=/usr/share/man;grep manpage_directory /etc/postfix/postfix-files | cut -d/ -f2- | cut -d: -f1 | grep '\.gz$' | while read f; do echo $f;[ ! -e "$d/$f" -a -e "$d/${f%.gz}" ] && sudo gzip -9v "$d/${f%.gz}";done
    sudo postfix set-permissions

Then you also might have the following problem:

> postfix/postfix-script: warning: group or other writable: /Library/Server/Mail/Data/mta

To fix edit /etc/postfix/postfix-files:

    sudo vim /etc/postfix/postfix-files

find the line

    $data_directory:d:$mail_owner:-:770:uc

and change 770 to 750. then set-persmissions again and verify:

    sudo postfix set-permissions
    sudo postfix check

[top](#top)<a name=zsh></a>
## ZSH

    brew install zsh zsh-completions

- https://github.com/sorin-ionescu/prezto

[top](#top)<a name=inconsolata></a>
## [Fonts](#fonts)

- wget http://www.levien.com/type/myfonts/Inconsolata.otf -O /Library/Fonts/Inconsolata.otf
- wget https://gist.github.com/raw/1595572/Inconsolata-dz-Powerline.otf -O /Library/Fonts/Inconsolata-dz-Powerline.otf
- wget https://gist.github.com/raw/1595572/Menlo-Powerline.otf -O /Library/Fonts/Menlo-Powerline.otf
- wget https://gist.github.com/raw/1595572/mensch-Powerline.otf -O /Library/Fonts/mensch-Powerline.otf


[top](#top)<a name=dotfiles></a>
## Dot files

- https://github.com/tamvm/dotfiles

Branch janus_plus, run `./run.sh`

- https://github.com/remitano/janus-plus

[top](#top)<a name=rbenv></a>
## Rbenv

    https://github.com/rbenv/rbenv#homebrew-on-macos

[top](#top)<a name=heroku></a>
## Heroku

Copy `~/.heroku/accounts` from the old machine.

Then:

    gem install heroku
    heroku plugins:install git://github.com/ddollar/heroku-accounts.git

Verify by running

    heroku accounts

[top](#top)<a name=nodejs></a>
## Nodejs

Now we need to install a couple of npm modules:

    npm install -g coffee-script
    npm install -g js2coffee


[top](#top)<a name=backblaze></a>
## Backblaze

Download and install Backblaze from [backblaze.com](http://backblaze.com/).

Start backblaze.

Select Transfer Backup State from the Backblaze Menu Icon and follow the steps.

### Time Machine

Its important to add backblaze directory to timemachine exclusions list

    sudo tmutil addexclusion -p /Library/Backblaze.bzpkg

