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

## オープン・クローズドの原則（OCP）
## リスコフの置換原則（LSP）
## 依存関係逆転の原則（DIP）
## インターフェイス分離の原則（ISP）