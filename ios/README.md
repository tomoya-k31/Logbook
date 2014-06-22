# iOS

### Install CocoaPods
```sh
$ sudo gem update --system
$ sudo gem update
$ sudo gem install cocoapods
$ sudo gem cleanup
$ pod setup
$ pod --version
```

> [開発レシピ：Objective-Cのライブラリ管理ツール CocoaPods](http://www.iosjp.com/dev/archives/451)


_ _ _

#### pod setupでerrorになった時の対処法

```sh
$ pod setup
Setting up CocoaPods master repo
[!] An error occurred while performing `git pull` on repo `master`.
[!] /usr/local/bin/git pull --ff-only

From https://github.com/CocoaPods/Specs

 + a076b5a...b27da90 master     -> origin/master  (forced update)

fatal: Not possible to fast-forward, aborting.
```


* 念のためバックアップ

```sh
$ mv ~/.cocoapods ~/cocoapods
$ mv ~/Library/Caches/CocoaPods ~/CocoaPodsCaches
```

* 再度実行

```sh
$ pod setup

# 新しいファイルが生成されていることを確認
$ ls ~/.cocoapods
$ ls ~/Library/Caches/CocoaPods

# バックアップを削除
$ rm -rf ~/cocoapods
$ rm -rf ~/CocoaPodsCaches
```
