# 排他制御

```sh
#!/bin/sh
 
LOCK_TMP_DIR=/Users/tomo/.lock
LOCK_FILE_NAME=".lock"
TIMESTAMP_FILE_NAME=".ts"
LOCKFILE=timer.lock
 
# -pでなければ作る(標準エラーは出力しない)
mkdir -p $LOCK_TMP_DIR
 
# 数値1 -ne 数値2   数値1と数値2が等しくない場合に真
if [ $? -ne 0 ]; then
    echo "mkdir error"
    exit 1;
fi
 
# 排他制御
lockfile -r 0 $LOCK_TMP_DIR/$LOCKFILE
if [ $? -ne 0 ]; then
    # error終了
    echo "起動済みのため終了"
    exit 1
fi
 
 
unlock() {
    echo "解除"
    rm -f $LOCK_TMP_DIR/$LOCKFILE
}
unset(){
    unset LOCK_TMP_DIR
    unset LOCK_FILE_NAME
    unset TIMESTAMP_FILE_NAME
    unset LOCKFILE
    unset START_TIME
    unset END_TIME
}
 
 
# 終了時にunlock
# Ctrl+Cを押しても実行される
# 複数のコマンドを指定するには「;」で区切り、コマンド全体を""で囲む
trap "unlock;unset" EXIT;
 
# [ls -1]は検索したファイルを1ファイル1行でリスト表示
for var in `ls -1 ${LOCK_TMP_DIR}`
do
    # -n 文字列 文字列の長さが0より大きければ真
    # ! 文字列  文字列の長さが0であれば真
    if [ ! "${var##*${TIMESTAMP_FILE_NAME}}" ]; then
        START_TIME=${var%${TIMESTAMP_FILE_NAME}}
        echo "OK! Get startTime."
    fi
done
 
# 初回起動分
if [ ! ${START_TIME} ]; then
    START_TIME=$(printf '%ld000' $(expr `date -v-1H +%s`))
    echo "Created startTime."
    touch $LOCK_TMP_DIR/${START_TIME}${TIMESTAMP_FILE_NAME}
fi
 
END_TIME=$(printf '%ld000' $(expr `date +%s`))
 
echo "start:"$START_TIME
echo "end:  "$END_TIME
 
 
# Main
sleep 5;
 
# Mainでエラーならロックファイルをそのままにして終了
if [ $? -ne 0 ]; then
    trap EXIT;
    exit 1;
fi
 
rm -f $LOCK_TMP_DIR/${START_TIME}${TIMESTAMP_FILE_NAME}
touch $LOCK_TMP_DIR/${END_TIME}${TIMESTAMP_FILE_NAME}
 
exit 0;
```


↓どこかで見つけたサンプル。。
```sh
#!/bin/sh

LOCKFILE=test.lock

lockfile -r 0 $LOCKFILE

# evaluate return code
if [ $? -ne 0 ]; then
  echo "Command aborted"
  
  # error終了
  exit 1
fi

# do something exclusive command
echo "important command"

# unlock
rm $LOCKFILE

# 正常終了
exit 0
```



消すかどうか聞かれないようにするには、`-f` オプションを付けると、このようなときにユーザに問い合わせることなく消去される。
```sh
override r--r--r--  tomo/staff for test.lock?
```
ファイルがロックされている時error:73が返され、`$?`で取得し判定する。
`file-system error 73 ("file is locked")`


> lockfile -option
>
> ```sh
> if lockfile -10 -r 5 -l 100 $LOCKFILE
> then
>  ・・・・・
> fi
> ```
> -10：ロックファイル (test.lock) が存在すれば10秒待つことを表します。

> -r 5：上記を5回繰り返す。その間にロックファイルが無くなればロックファイルを作成して成功とし、ロックファイルが無くならなければ失敗とする。

> -l 100：存在するロックファイルが作成後100秒以上経過していた場合、ロックファイルを削除して新たにロックファイルを作成して成功とする。


###### MEMO
シェルでミリ秒を表示
```sh
echo $(printf '%ld000' $(expr `date +%s`))
```



> [flock(1)でシェルスクリプトの排他制御（Linux）](http://qiita.com/ma2saka/items/1eab5713097993d7ddf8)
> [プロセスの多重起動をアドバイザリロックで防止する・改](http://qiita.com/ngyuki/items/cc4f6aeaa9b53baa3b68)