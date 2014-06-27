# Ruby

###  MacにRubyをインストールして複数バージョンの切り替え対応

* rbenv, ruby-buildのインストール

```sh
brew install rbenv
brew install ruby-build
```
*（気が向けば）# 依存ライブラリのインストール

```sh
brew install readline
brew install openssl
```
* .zshrcに設定を追加

```sh
# eval "$(rbenv init -)"
eval "$(rbenv init - zsh)"
```
* rbenvで利用できるRubyのバージョンを確認

```sh
$ rbenv install -l
Available versions:
1.9.3-p392
1.9.3-p448
1.9.3-preview1
1.9.3-rc1
2.0.0-dev
2.0.0-p0
2.0.0-preview1
2.0.0-preview2
2.0.0-rc1
2.0.0-rc2
2.1.0-dev
jruby-1.5.6
….
```

_ _ _

###### Rubyをインストール

* 1.9.3をインストールします。

```sh
$ rbenv install 1.9.3-p448
$ rbenv rehash
```

* 2.0.0をインストールします。

```sh
$ rbenv install 2.0.0-p0
$ rbenv rehash
```

###### Rubyのバージョンを切り替える

* 1.9.3に設定してみます。

```sh
$ rbenv global 1.9.3-p448
$ ruby -v
```

* 2.0.0に設定してみます。

```sh
$ rbenv global 2.0.0-p0
$ ruby -v
```

###### インストール済みのバージョンを確認

```sh
$ rbenv versions
  system
  1.9.3-p392
  1.9.3-p426
  1.9.3-p448
  2.0.0-p0
* 2.0.0-p195 (set by /Users/asakura/Sites/ruby2/.ruby-version)
  2.0.0-p247
```

###### 古いバージョンをアンインストール

```sh
$ rbenv uninstall 1.9.3-p385
$ rbenv uninstall 2.0.0-p0
```

###### 必須のgemをインストール

```sh
gem install bundler
```


>参考サイト

* [rbenvとruby-buildでRuby環境を最新に保つ](https://gist.github.com/mochiz/4736183)
* [Mac OS X rbenvでRubyのバージョンを切り替える](http://www.happytrap.jp/blogs/2013/04/08/10394/)
* [MacにRubyをインストールする時のメモ](http://qiita.com/heki1224/items/5f74ae1b1cb5dc03cd36)



***
### MacのRubyGemsを最新に更新

```sh
$ sudo gem install rubygems-update
```
###### 一度PCの再起動

```sh
$ sudo update_rubygems
```
###### インストール or アップデートができたら、念のためバージョンを確認。

```sh
$ gem -v
```

> 参考サイト

* [Mac OS 10.8（Mountain Lion）にSASS + Compassをインストールするメモ](http://dounokouno.com/2012/11/14/mountain-ion-sass-compass/)
* [ツイッターBotを作るための準備](http://www.ruby-ruby.info/date/2013/06/14/)

