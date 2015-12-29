# オブジェクト指向設計原則

[参照: オブジェクト指向設計原則 - Strategic Choice](http://d.hatena.ne.jp/asakichy/20090122/1232879842)

## 単一責任の原則（SRP）

`the Single Responsibility Principle`

> クラスに変更が起こる理由は、一つであるべき。
> (A class should have only one reason to change.)

クラスを変更する理由は１つより多く存在してはならない。  
要するに、クラス1つに対する責任は1つにするべきで、複数の異なるメソッドなどを追加しないこと。単一責任のほうがテストがし易い。

#### デザインパターン
- Proxy
- Facade
- Iterator

> - [プログラマが知るべき97のこと - [73] 単一責任原則](http://xn--97-273ae6a4irb6e2hsoiozc2g4b8082p.com/%E3%82%A8%E3%83%83%E3%82%BB%E3%82%A4/%E5%8D%98%E4%B8%80%E8%B2%AC%E4%BB%BB%E5%8E%9F%E5%89%87)
> - [SOLIDの原則: Part1 - 単一責任の原則(Single Responsibility Principle)](http://code.tutsplus.com/ja/tutorials/solid-part-1-the-single-responsibility-principle--net-36074)
> - [アジャイル設計と5つの原則](http://tdak.hateblo.jp/entry/20130703/1372842149)
> - [Hello, Stupid World! - オブジェクト指向設計　単一責任の原則](http://ameblo.jp/trap-z/entry-11906924936.html)

## オープン・クローズドの原則（OCP）
## リスコフの置換原則（LSP）
## インターフェイス分離の原則（ISP）
## 依存関係逆転の原則（DIP）