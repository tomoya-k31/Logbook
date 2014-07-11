# Mac Tools

## シェル効率化ツール
### Homebrewインストール

```sh
$ ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```
> 公式：[Homebrew — The missing package manager for OS X](http://brew.sh/)

##### Homebrewで「brew update」をしたらエラーになった時の対処法

* 長いこと更新作業を忘れるとでやすいエラー

```sh
$ brew update
error: The following untracked working tree files would be overwritten by merge:
	Library/Formula/cabocha.rb
Please move or remove them before you can merge.
Aborting
Updating 7d2c1da..bfe50e3
Error: Failed while executing git pull  origin refs/heads/master:refs/remotes/origin/master
```

* 対処の仕方は次のようにするとOK

```sh
$ cd /usr/local
$ git remote add origin git://github.com/mxcl/homebrew.git
fatal: remote origin already exists.
$ git fetch origin
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 2), reused 3 (delta 2)
Unpacking objects: 100% (3/3), done.
From git://github.com/mxcl/homebrew
   4d2d66e..8a968e9  gh-pages   -> origin/gh-pages
$ git reset --hard origin/master
HEAD is now at bfe50e3 shen: another style issue
```

* うまくアップデートできた！

```sh
$ brew update
Already up-to-date.
```


_ _ _

```sh
# tmuxとMacのクリップボードを共有する
$ brew install reattach-to-user-namespace

$ brew install jq
$ brew install curl
$ brew install wget
$ brew install tree
$ brew install jsonpp
$ pip install httpie

## Python3だとエラー
$ pip install logcat-color

$ brew install zsh
$ brew install zsh-completions
$ brew install tmux
$ gem install tmuxinator

## MacでGNUのコマンドを使う
$ brew install xz
$ brew install binutils
$ brew install findutils
$ brew install coreutils
```


_ _ _

##### ログインシェルを変更
```sh
## 現在のシェルを確認する
$ dscl localhost -read Local/Default/Users/$USER UserShell
UserShell: /bin/bash
```
```sh
$ sudo sh -c "echo '/usr/local/bin/zsh' >> /etc/shells"

## 確認
$ cat /etc/shells
$ chsh -s /usr/local/bin/zsh
```
> [Homebrew で zsh を導入する](http://www.d-wood.com/blog/2014/03/14_5816.html)

_ _ _

##### Install Homebrew-cask
```sh
$ brew tap caskroom/cask
$ brew install brew-cask

# バグったら
$ brew update && brew upgrade brew-cask && brew cleanup && brew cask cleanup
```
> [caskroom/homebrew-cask](https://github.com/caskroom/homebrew-cask)


##### Install LaunchRocket
```sh
$ brew cask install launchrocket
```
> [jimbojsb/launchrocket](https://github.com/jimbojsb/launchrocket)

_ _ _

##### Install Tomcat
```sh
$ mkdir -p /usr/local/src; cd /usr/local/src
$ wget http://ftp.meisei-u.ac.jp/mirror/apache/dist/tomcat/tomcat-7/v7.0.54/bin/apache-tomcat-7.0.54.tar.gz
$ tar zxvf apache-tomcat-7.0.54.tar.gz
$ mv apache-tomcat-7.0.54 /usr/local/tomcat7052
```

##### iTerm2設定
```sh
# color
$ cd $HOME/.dotfiles
$ git clone https://github.com/seebi/dircolors-solarized.git
$ ln -s ~/.dotfiles/dircolors-solarized/dircolors.256dark ~/.dircolors

# vim
$ mkdir -p $HOME/.vim/bundle; cd $HOME/.vim/bundle
$ git clone git://github.com/Shougo/neobundle.vim.git
$ vim +":NeoBundleInstall" +:q
```

iterm用のカラーセットをダウンロード、import後設定
[https://github.com/altercation/solarized/tree/master/iterm2-colors-solarized](https://github.com/altercation/solarized/tree/master/iterm2-colors-solarized)
