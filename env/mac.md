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
$ brew install jsonpp
$ pip install httpie

$ brew install zsh
$ brew install zsh-completions
$ brew install tmux
$ gem install tmuxinator
```