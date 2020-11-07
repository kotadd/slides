---
marp: true
theme: default
paginate: true
---
# SOLID原則

---
# SOLID原則とは
下記の5つの原則の接頭辞を並べたもの。
* Single Responsibility Principle(単⼀責任の原則)
* Open-Closed Principle(オープン・クローズドの原則)
* Liskov Substitution Principle(リスコフの置換原則)
* Interface Segregation Principle(インターフェース分離の原則)
* Dependency Inversion Principle(依存関係逆転の原則)

---
# SOLID原則の目的
* 変更に強いこと
* 理解しやすいこと
* コンポーネントの基礎として、多くのソフトウェアシステムで利⽤できること

> Clean Architecture 達人に学ぶソフトウェアの構造と設計より

---
# Single Responsibility Principle(単⼀責任の原則)

> クラス(型)を変更する理由はふたつ以上存在してはならない

**凝集**を拡張したものだといわれている。
手続きや利用シーンが近い機能を一つのモジュールに凝集することは開発のしやすさにつながるが、再利用性が落ちる。逆に、変更可能性のない責務を無意味に切り離すことは「不必要な複雑さ」に結びつく。

---
# Open-Closed Principle(オープン・クローズドの原則)

> ソフトウェアの構成要素は拡張に対しては開いていて、修正に対して閉じていなければならない。
> (アジャイルソフトウェア開発の奥義第2版 より）

ちょっとした機能を追加しようとしたときに、既存のコードへの修正が必要となってくるもの。

---
# Liskov Substitution Principle(リスコフの置換原則)

> S 型のオブジェクト o1 の各々に、対応する T 型のオブジェクト o2 が 1 つ存在し、T を使って定義されたプログラム P に対して o2 の代わりに o1 を使っても P の振る舞いが変わらない場合、S は T の派⽣型であると⾔える。
(アジャイルソフトウェア開発の奥義第2版 より）

```
// 違反例
const o1 = new S() // S: 正方形 extends T: 長方形
const o2 = new T() // T: 長方形

const P = (T, width, height) => {
  arg.width = width;
  arg.height = height;
  return (width * 2 + height * 2) / 面積; // 面積：S.calcArea()
}

P(o2, 2, 5) // 14÷10
P(o1, 2, 5) // width==heightとなるため、同じように計算されない
```

---
# Interface Segregation Principle(インターフェース分離の原則)

* クライアントに、クライアントが利用しないメソッドへの依存を強制してはならない

**例：UserというIFをECで作って、売り手と買い手に依存させると、売り手しか利用できない情報に買い手もアクセスできてしまう。**

---
# Dependency Inversion Principle(依存関係逆転の原則)

> A. 上位レベルのモジュールは下位レベルのモジュールに依存すべきではない。両方とも抽象（abstractions)に依存すべきである。
  B. 抽象は詳細に依存してはならない。詳細が抽象に依存すべきである。
(引用：[依存性逆転の原則](https://ja.wikipedia.org/wiki/%E4%BE%9D%E5%AD%98%E6%80%A7%E9%80%86%E8%BB%A2%E3%81%AE%E5%8E%9F%E5%89%87))

具象クラスではなく、抽象クラスに依存することにより、汎用性を持たせる。

---
