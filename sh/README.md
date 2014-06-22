# sh

#### シェル変数

| 表記 | 意味 |
|:-----------:|:------------|
|$NAME | 変数NAMEを表す |
|$1, $2, …, $9 | 各引数を表す。順に1番目、2番目、…、9番目を意味する |
|${10}, ${11}, … | 10番目、11番目、… の引数を意味する |
|$0 | 実行されたシェルスクリプトの実行ファイル名を表す |
|$# | 実行時に与えられた引数の数を表す |
|$@ | 引数をスペース区切りで表す |
|$* | `$@`とほぼ同じ。引数を環境変数IFSで区切って表す。IFSが空の場合、スペース区切りとなる。`IFS=:`を指定すると`a:b:c:d`となる。 |
|$? | 直前に実行された処理の終了コード値を表す。これを使って実行されたコマンドが正しく終了したかどうか判定します。 |
|$$ | 実行中のシェルのプロセスID値を表す |
|$! | 直前に実行された処理のプロセスIDを表す |
|${NAME:-VALUE} | 変数NAMEが空の場合、値VALUEが設定される |
|${NAME:=VALUE} | 「${NAME:-VALUE}」と同じ |
|${NAME:+VALUE} | 変数NAMEが空でなければ、値VALUEが設定される |
|${NAME:?VALUE} | 変数NAMEが空の場合、値VALUEを標準エラーに出力し、スクリプトの実行を終了する |
|${NAME:START} | 変数NAMEのSTART番目以降の値を表す |
|${NAME:START:LENGTH} | 変数NAMEのSTART番目からLENGTH文字分の値を表す |

> [ステップ・バイ・ステップ・シェルスクリプト（5）：シェルの変数に慣れる - ＠IT](http://www.atmarkit.co.jp/ait/articles/0010/19/news003.html)

> [Linuxのシェルスクリプト変数の記号あれこれ - 気まぐれな備忘録(仮)](http://kajitiluna.hatenablog.com/entry/20111023/1319381392)


_ _ _

#### 四則演算
数値の演算を行う際には`expr`を使用。(例)``変数 = `expr 5 + 3` ``
区切りに半角スペースが必要、括弧と掛け算はエスケープが必要。
小数点を扱った計算は`bc`コマンドを使用。

| 演算子 | 意味 |
|:-----------:|:------------|
| \`expr a + b\` | aとbの和 |
| \`expr a - b\` | aとbの差 |
| \`expr a \\* b\` | aとbの積 |
| \`expr a / b\` | aとbの商 |
| \`expr a % b\` | aとbの剰余 |

`$((計算式))`でも可能。半角スペースやエスケープは不要。
```sh
#!/bin/sh
echo $((3+5*8))  #=>43
expr 3 + 5 \* 8  #=>43
```

_ _ _

#### 数値演算子

| 演算子 | 意味 |
|:-----------:|:------------|
| 数値1 -eq 数値2 | 数値1と数値2が等しい場合に真(=) |
| 数値1 -ne 数値2 | 数値1と数値2が等しくない場合に真(!=) |
| 数値1 -gt 数値2 | 数値1が数値2より大きい場合に真(>) |
| 数値1 -lt 数値2 | 数値1が数値2より小さい場合に真(<) |
| 数値1 -ge 数値2 | 数値1が数値2より大きいか等しい場合に真(>=) |
| 数値1 -le 数値2 | 数値1が数値2より小さいか等しい場合に真(<=) |

> [シェルスクリプト入門 [演算・比較]](http://www.k4.dion.ne.jp/~mms/unix/shellscript/shell_calc.html)



_ _ _

#### 文字列判定
| 演算子 | 意味 |
|:-----------:|:------------|
| 文字列 | 文字列の長さが0より大きければ真 |
| -n 文字列 | 文字列の長さが0より大きければ真 |
| ! 文字列 | 文字列の長さが0であれば真 |
| -z 文字列 | 文字列の長さが0であれば真 |
| 文字列1 = 文字列2 | 2つの文字列が等しければ真 |
| 文字列1 != 文字列2 | 2つの文字列が等しくなければ真 |



_ _ _

#### ファイル判定
| 演算子 | 意味 |
|:-----------:|:------------|
| -d ファイル名 | ディレクトリなら真 |
| -f ファイル名 | 通常ファイルなら真 |
| -L ファイル名 | シンボリックリンクなら真 |
| -r ファイル名 | 読み取り可能ファイルなら真 |
| -w ファイル名 | 書き込み可能ファイルなら真 |
| -x ファイル名 | 実行可能ファイルなら真 |
| -s ファイル名 | サイズが0より大きければ真 |
| ファイル1 -nt ファイル2 | ファイル1がファイル2より新しければ真 |
| ファイル1 -ot ファイル2 | ファイル1がファイル2より古ければ真 |



_ _ _

#### パス文字列からファイル名／ディレクトリ名／拡張子を抽出する
```sh
#!/bin/sh

test_path="/usr/local/etc/apache/httpd.conf"

string_filename=${test_path##*/}
string_filename_without_extension=${string_filename%.*}
string_path=${test_path%/*}
string_extension=${test_path##*.}

echo ${string_filename}
echo ${string_filename_without_extension}
echo ${string_path}
echo ${string_extension}
```

```
# 実行結果
httpd.conf
httpd
/usr/local/etc/apache
conf
```
> 「${test_path##*/}」は「*/」で表される文字列の最長一致接頭部分の除去を、「${test_path%/*}」は「/*」で表される最短一致接尾部分の除去をするからです。

> 元の文字列「${test_path}」が「/usr/local/etc/apache/httpd.conf」ですので、「${test_path##*/}」では「*/」にマッチする最長の接頭部分「/usr/local/etc/apache/」が削除され、結果として「httpd.conf」が残ります。
また、「${test_path%/*}」は「/*」にマッチする最短の接尾部分「/httpd.conf」が削除され、結果として「/usr/local/etc/apache」が残ります。

> 引用： [【FreeBSD】シェルスクリプトでパス文字列からファイル名／ディレクトリ名／拡張子を抽出する](http://www.kishiro.com/FreeBSD/get_filename_in_shellscript.html)




_ _ _

#### 処理を一行で実行するときの接続子
```sh
# ; の前後コマンドに何の関連性はなし
$ echo abcd ; echo えーびーしぃでぇ]

# && は、直前に実行された処理の終了コード値が[正常終了:0]なら次のコマンドを実行
$ echo 新規書き込み > a.txt && echo 書き込み成功
bash: a.txt: Permission denied

# || は、上記以外の時に実行
$ echo 新規書き込み > a.txt || echo 書き込み失敗
bash: a.txt: Permission denied
書き込み失敗
```