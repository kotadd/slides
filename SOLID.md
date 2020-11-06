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

> モジュールはたった⼀つのアクターに対して責務を負うべきである。

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
// 誤った例
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

一つのIFが過剰に責務を負わないようにする。

**例：UserというIFをECで作って、売り手と買い手に依存させると、売り手しか利用できない情報に買い手もアクセスできてしまう。**

---
# Dependency Inversion Principle(依存関係逆転の原則)

> 上位レベルのモジュールは下位レベルのモジュールに依存すべきではない。両方とも「抽象」に依存すべきである。
「抽象」は詳細に依存してはならない。詳細が「抽象」に依存すべきである。
(XPワークショップより)

具象クラスではなく、抽象クラスに依存することにより、汎用性を持たせる。

---
