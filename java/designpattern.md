### Adapter, Facade, Proxy パターンの違い

`単一責任の原則（SRP）の延長`


> [Adapter, Facade, Proxy パターンの違いメモ](http://futurismo.biz/archives/2813)

### Proxy(構造

直接触る代わりに、中間層を置くのは悪くない手法である。
汎用的過ぎて、デザインパターンと言えるのかは微妙。
例えば、直接Stringを触る代わりにHtmlStringとRawStringにWrapして使おう。というのも中間層を置いていることに変わりはない。
また、マルチスレッドで使われるFutureパターンも同様である。
中間層はあらゆる問題の解決に利用される。


### Facade(構造)

よく使われそうなメソッドだけ、わかりやすいところに出しておく。
これは良い設計であり、デザインパターンにふさわしいだろう。



### Iterator(振る舞い)

多態性が有用であることのサンプルの一つ。
iterator自体は知っておいて損はないだろう。
現在においては言語組み込みとなっていることが多く、改めてデザインパターンで学ぶ必要はないかもしれない。

### Adapter(構造)

インタフェースを変換することにより, インタフェースに互換性がない クラス同士を接続する.
既存のクラスに対して修正を加えることなく, インタフェースを変更することができる.
継承を利用する場合と委譲を利用する場合がある.



- Facade はインタフェースを簡素化する
- Adapter は既存インタフェースを他のインタフェースに変換する
- Proxy はインタフェースを変更せずに機能追加する.

```java
class Target {
    void printInt (int i) {
        System.out.println (i);
    }
 
    void printLong (long l) {
        System.out.println (l);
    }
}
 
class Adapter {
    Target target;
    Adapter (Target target) {
        this.target = target;
    }
 
    void printInt (Integer i) {
        target.printInt (i);
    }
 
    void printLong (Long l) {
        target.printLong (l);
    }
     
}
 
class Facade {
    Target target;
    Facade (Target target) {
        this.target = target;
    }
 
    void print (long l) {
        target.printLong (l);
    }
}
 
class Proxy {
    Target target;
    int intCount = 0;
    int intCache= 0;
    long longCount = 0;
    long longCache = 0; 
     
    Proxy (Target target) {
        this.target = target;
    }
     
    void printInt (Integer i) {
        target.printInt (i);
        intCount++;
        intCache = i;
    }
 
    void printLong (Long l) {
        target.printLong (l);
        longCount++;
        longCache = l;
    }
}
```