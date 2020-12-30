---
marp: true
theme: common
paginate: true
---

# Javascript

<!--
class: title
-->

---

# JavaScript とは

> プロトタイプベースで、シングルスレッドで、動的型付けを持ち、そしてオブジェクト指向、命令形、宣言的 (例えば関数プログラミング) といったスタイルをサポートするマルチパラダイムのスクリプト言語

https://developer.mozilla.org/ja/docs/Web/JavaScript

---

# トピック

1. JavaScript Engine
   1. Memory Heap
   2. Call Stack
2. スコープ
3. プロトタイプ
4. this
   1. アロー関数

<!--
class: noclass
-->

---

# JavaScript Engine

![bg 60%](https://miro.medium.com/max/700/1*4lHHyfEhVB0LnQ3HlhSs8g.png)

<!--
class: main
_footer: 参考：https://blog.sessionstack.com/how-does-JavaScript-actually-work-part-1-b0bacc073cf
-->

---

# Memory Heap

メモリの割り当てを行う場所

発生するリスク：メモリリーク

<!--
class: noclass
_footer: 参考：https://blog.sessionstack.com/how-does-JavaScript-actually-work-part-1-b0bacc073cf
-->

---

# Call Stack

- コードを実行する Stack Frame（Call Stack に入るそれぞれのエントリー）
- 発生するリスク：スタックオーバーフロー
- シングルスレッド＝シングルコールスタック

> The Call Stack is a data structure which records basically where in the program we are.
> → 　 Call Stack はプログラムのどこにいるのかを記録するデータ構造である

<!--
class: noclass
_footer: 参考：https://blog.sessionstack.com/how-does-JavaScript-actually-work-part-1-b0bacc073cf
-->

---

# このコードを実行するとどうなる？

```JavaScript
const list = new Array(20000).fill('x')

function removeItemsFromList() {
  var item = list.pop()

  if (item) {
    removeItemsFromList()
  }
}

removeItemsFromList()
```

---

# 再帰性を保ったまま修正する

```JavaScript
const list = new Array(20000).fill('x')

function removeItemsFromList() {
  var item = list.pop()

  if (item) {
    setTimeout(removeItemsFromList, 0)
  }
}

removeItemsFromList()
```

[解説の図](https://viewer.diagrams.net/?highlight=0000ff&edit=_blank&layers=1&nav=1&title=callbackqueue.drawio#R3VrLcpswFP0aZtpFO4iXYWk7TpqZZJqOF2mXMqhAC4gRcmzy9RUgzEM4phPbQFZGR9IFHR1dcWQkdRnu7wiMvUfsoEBSZGcvqTeSogBNMdhPhqQFMgNaAbjEd3ijClj7r4iDMke3voOSRkOKcUD9uAnaOIqQTRsYJATvms1%2B46B51xi6SADWNgxE9Nl3qFegpjKr8G%2FId73yzsCwipoQlo35SBIPOnhXg9SVpC4JxrS4CvdLFGTklbwU%2FW6P1B4ejKCI9unw%2FRlYpvZoze%2FmD%2FpmBl61bfKFR3mBwZYPWFqpkqlKi4WkGAELvNgQduVmV%2F2q8rHStCSQ4G3koOwZZNZu5%2FkUrWNoZ7U7JhmGeTQMWAlkYYQxlQ%2BICEX7GsTHeIdwiChJWRNea3K6ud5ASf%2Bumj2gccyrzZwicxByxbiH0BWp7ILz%2Bh8cKwLHS5j3WlNo%2FxUIY%2BOkTVZg4LsRu7YZK4gwIGPDZxqd84rQd5ys%2B4KgxH%2BFmzxURneM%2FYjm49EXkn6TxdpSnBSr7EyEA7nFuCoyPusk%2FEJ8q6Kmhxal1uZoeFVqAkvPaDN%2Fup%2B8HjVFP6lH45p61Menx1aSPMhzODkanUlykydI%2BccWMXTqwjSbutRAB%2BnyNYU5EzgnKMQv6J6iMLklOHzwE%2Frp89jUqvZX64WIM6dJ3KE8GHHWRIkzhiauzBWTY04bnLkOi9MmCUXOPPOKrBThCPUkBTkN6yhSUhuz3jHkEiMogNR%2FaRrOLh74HZ6yvar%2Bbtlg3NBaTCZ4S2zEO9X9YSuOKZ8IRCFxERUC5bNyGPU7Jkr0SWNTs9E%2FgV5MzqK7%2BdBu0rAGdpNANErl8UcSw%2Bjo2Qi7WaNePDIZMMrI7PAY1pXo0j6oH%2B5aUVf1w%2BXZaX0DZlvpmhcxoR52cQSDVYUumhKt2jxgHHOu%2FiBKU36CnNHYnCRGIEl%2FZv2%2F6mXxV73uZs%2BDF6WUl47OQLGvviUp7mmLffOthmbPF4rebwrvWwqiFx88Y7Q2Yqv%2FC%2FnFEobonj%2F6iYU162D9qicWijls6qgnjloeOX%2FqMHumjnJpjiV1TPRkxBzc4CvWoMoG11J2KdjTyjbOrey8K%2FP5MK014Gn0uLueNZUCgC63JrsIeVYvXLI0%2BnXUfpMfwUISDfJEqBv8qEwRre5EqOv%2Fd%2BqlqBPt40SoG%2FzPFEW0G%2BOkrv1lCbjggmXF6sugYlepvq9SV%2F8A)

---

# コラム：ES6 以前に JavaScript にクラスがなかった理由

> “If I had done classes in JavaScript back in May 1995, I would have been told that it was too much like Java or that JavaScript was competing with Java … I was under marketing orders to make it look like Java but not make it too big for its britches … [it] needed to be a silly little brother language.”
> Brendan Eich

-> 1995 年 3 月にクラスを JS に持たせていたら、Java に似過ぎている or Java と競っていると言われただろう。マーケティングとして、Java に寄せつつも寄せ過ぎないようにする必要があった。

https://hackernoon.com/changemakers-in-programming-brendan-eich-e43f2cc7d269

---

# 下記の結果はどうなるでしょう？

```JavaScript
const array = [1, 2, 3, 4]
for (var i = 0; i < array.length; i++) {
  setTimeout(function () {
    console.log('I am at index  ' + i)
  }, 3000)
}
```

[回答](https://repl.it/@kotadd/closures-exercise-7#index.js)

---

# Scope の考え方

Function Scope

```JavaScript
if (5 > 4) {
  var secret = '12345'
}

secret // '12345'
```

Block Scope （大体のプログラミング言語はこっち）

```JavaScript
if (5 > 4) {
  let secret = '12345' //constもOK
}

secret // undefined
```

---

# プロトタイプチェーン

![bg 70%](https://images.ctfassets.net/aq13lwl6616q/4U7Xxx4CIyG6bHmpOp6ujj/00720fdac4cb138ed97e80da74730cd2/prototype_chain.png)

<!--
class: main
-->

---

# プロトタイプの例

```JavaScript
Date.prototype.lastYear = function(){
  return this.getFullYear() - 1;
}

const date = new Date('1900-10-10')
date.lastYear()

date.__proto__ === Date.prototype
```

---

# コラム：JS の "==" の動き

https://dorey.github.io/JavaScript-Equality-Table/

<!--
class: noclass
-->

---

# this Keyword

## 下記の結果はどうなるでしょう？

```JavaScript
Array.prototype.map2 = function () {
  arr = []
  console.log('this', this)
  for (let i = 0; i < this.length; i++) {
    arr.push(this[i] + ' by map2')
  }
  return arr
}

// [1, 2, 3].map2()
```

→ ダイナミックスコープ

<!--
class: notitle
-->

---

# this Keyword

## 下記の結果はどうなるでしょう？

```JavaScript
Array.prototype.map3 = () => {
  arr = []
  // console.log('this', this)
  for (let i = 0; i < this.length; i++) {
    arr.push(this[i] + ' by map3')
  }
  return arr
}

// [1, 2, 3].map3()
```

→ レキシカルスコープ

---

# アロー関数

> - 2 つの理由から、アロー関数が導入されました。1 つ目の理由は関数を短く書きたいということで、2 つ目の理由は this を束縛したくない、ということです。

> - アロー関数自身は this を持ちません。レキシカルスコープの this 値を使います。つまり、アロー関数内の this 値は通常の変数検索ルールに従います。このためスコープに this 値がない場合、その一つ外側のスコープで this 値を探します。

<!--
_footer: 参考：https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Functions/Arrow_functions
-->

---

# おまけ問題

```JavaScript
function Human(name, age) {
  this.name = name
  this.age = age
}

Human.prototype.build = function () {
  function building() {
    return 'built by ' + this.name
  }
  return building()
}

const Kail = new Human('Kail', 17)
Kail.build()
```

[その他の例](https://repl.it/@kotadd/dynamic-scope#index.js)

---

# EOP

<!--
class: title
-->
