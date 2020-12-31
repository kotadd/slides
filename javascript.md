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
   3. Callback Queue
   4. Event Loop
2. スコープ
3. プロトタイプチェーン
4. this Keyword
   1. アロー関数

<!--
class: noclass
-->

---

# JavaScript Engine (V8)

![bg 90%](https://images.ctfassets.net/aq13lwl6616q/3o7Q3edCrVJG9Zzj6VMZ1K/28136a643636dfa04090f3fb5c5467ff/javascript_engine.png)

<!--
class: main
_footer: 参考：https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
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

```JavaScript
// メモリリークの例
var person = {
  first: "kota",
  last: "nishinaka"
};

person = "knishina";
```

<!--
class: noclass
_footer: 参考：https://blog.sessionstack.com/how-does-JavaScript-actually-work-part-1-b0bacc073cf
-->

---

# コラム：hoisting

コンパイル段階ですべての変数や関数の宣言をメモリに入れること

- function は完全に hoisting される
  - コードベースのどこからでも呼び出すことができる
- var 変数は hoisting されて未定義の値に初期化される
  - 初期化される前にコード内で使用された場合は、undefined を返す
    → メモリリークなどの原因になる
- let 変数と const 変数は hoisting されているが値は初期化されない
  - 宣言される前に使用された場合、参照エラーを投げる（推奨）

<!--
_footer: 参考: https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts

-->

---

# Call Stack

- コードを実行する Stack Frame（Call Stack に入るそれぞれのエントリー）
- 発生するリスク：スタックオーバーフロー
- シングルスレッド＝シングルコールスタック

> The Call Stack is a data structure which records basically where in the program we are.
> → Call Stack はプログラムのどこにいるのかを記録するデータ構造である

<!--
class: noclass
_footer: 参考：https://blog.sessionstack.com/how-does-JavaScript-actually-work-part-1-b0bacc073cf
-->

---

# Event Loop and Callback Queue

- ブラウザで JavaScript のコードを実行すると、エンジンがコードの解析を開始し、各行が実行され、コールスタックにポップイン・ポップアウトされる。
- パーサが Web API で実行する処理をブラウザに渡して処理する。メソッドの実行が終了すると、JavaScript が実行する必要のあるものを Callback Queue に入れる。
- Callback Queue は、コールスタックが完全に空になるまで実行できない。そのため、Event Loop は常にコールスタックが空になっているかどうかをチェックし、コールバックキューにあるものをコールスタックに戻す。
- コールスタックに戻ってきたら実行して、スタックからポップアウトする。

<!--
_footer: 参考：https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
-->

---

# コラム：Job Queue

ES6 で Promise などを優先する Job Queue という概念が追加された

```JavaScript
// 1 Callback Queue ~ Task Queue
setTimeout(() => {
  console.log("1", "is the loneliest number");
}, 0);
setTimeout(() => {
  console.log("2", "can be as bad as one");
}, 10);

// 2 Job Queue ~ Microtask Queue
Promise.resolve("hi").then(data => console.log("2", data));

// 3 Call Stack
console.log("3", "is a crowd");
```

<!--
_footer: 参考：https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts

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
_footer: 参考：https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
-->

---

# プロトタイプの例

```JavaScript
Date.prototype.lastYear = function(){
  return this.getFullYear() - 1;
}

const date = new Date('1991-07-12')
date.lastYear()

date.__proto__ === Date.prototype
```

---

# コラム：JS の "==" の動き

https://dorey.github.io/JavaScript-Equality-Table/

様々な type：https://repl.it/@kotadd/typesjs#index.js

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
[時間があればこっちの例も全て見ておく](https://repl.it/@kotadd/scope#index.js)

---

# this Keyword の 4 type

1. new keyword binding - 作成された object が this の対象になる
2. implicit binding - 呼んでいる object が this の対象となる
3. explicit binding - bind を使えば this の対象を変更できる
4. メソッド内での arrow functions - lexically scope になるため、window object が this となる。
   ( this を呼ぶアロー関数を返す HOF を作成すると object が対象となる)

[上記の例](https://repl.it/@kotadd/scope#fourThisPatterns.js)

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
  console.log(this)
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

# コラム：Node.js 以前のモジュール

```JavaScript
var fightModule = (function () {
  function fight(char1, char2) {
    var attack1 = Math.floor(Math.random() * char1.length)
    var attack2 = Math.floor(Math.random() * char2.length)
    return attack1 > attack2 ? `${char1} wins` : `${char2} wins`
  }

  return {
    fight: fight,
  }
})()
```

× global namespace の汚染
× html で script を読み込む順序に依存

---

# call, apply, bind

```JavaScript
const a = {
  name: "a",
  say(str1, str2) {
    return str1 + ' said hello to ' + str2;
  },
  callName() {
    return this.name;
  }
};
const anotherObj = {}

a.say.call(anotherObj, 'a', 'b');
a.say.apply(anotherObj, ['a', 'b']);
const func = a.say.bind(anotherObj, 'a', 'b');
func()
```

bind はメソッド内の this を実行時点のもので固定することも可能。

---

# コラム：効率的な実装

非効率な実装

```JavaScript
function run(idx) {
  const bigArray = new Array(33800000).fill("😄");
  console.log("created!");
  return bigArray[idx];
}

const getEfficient = run()

```

---

# コラム：効率的な実装

効率的な実装（Memoization）

```JavaScript
function run(idx) {
  const bigArray = new Array(33800000).fill("😄");
  console.log("created!");
  return function(idx) {
    return bigArray[idx];
  };
}

const getEfficient = run()

```

---

# コラム：効率的な実装（Memoization）

```JavaScript
functions memoizedAddTo80() {
  let cache = {}
  return function(n) {
    if (n in cache) {
      return cache[n]
    } else {
      console.log('long time...')
      cache[n] = n + 80
      return cache[n]
    }
  }
}
const memoized = memoizedAddTo80()

console.log('1.', memoized(5))
```

<!--
class: noclass
-->

---

# Promise の方法

- parallel
  - 同時実行で全て返す
- race
  - 一番速いものだけ返す
- sequence
  - 順番に実行して全て返す

https://repl.it/@kotadd/async-2#index.js

<!--
_footer: 参考：https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
-->

---

# コラム：V8 Engine

- Chrome に利用されている C++の JavaScript engine
- Node.js の標準 runtime
- JIT compiler を実装している
- 内部的に複数のスレッドを利用している

<!--
_footer: 参考：https://blog.sessionstack.com/how-JavaScript-works-inside-the-v8-engine-5-tips-on-how-to-write-optimized-code-ac089e62b12e
-->

---

# コラム：V8 Engine

- Inlining
  - 呼び出し元の関数のコードを呼び出し先の実装に置き換えること
- Hidden class
  - dynamic properties を同じ順番で初期化した方が効率的になる
  - [動作の図](https://miro.medium.com/max/700/1*spJ8v7GWivxZZzTAzqVPtA.png)
  - Inline caching
- Compilation to machine code
- Garbage collection

<!--
_footer: 参考：https://blog.sessionstack.com/how-JavaScript-works-inside-the-v8-engine-5-tips-on-how-to-write-optimized-code-ac089e62b12e
-->

---

# コラム：V8 Engine

## 効率的な JavaScript の書き方

1. object の初期化は同じ順序で行うこと(Hidden Classes)
2. constructor で全ての property をセットすること
3. 同じメソッドを繰り返し実行するコードの方が異なるメソッドを一度だけ実行するよりも速い(inline caching)
4. key が incremental でない疎な配列を避ける。大きな配列に事前に割り当てることや配列の要素を削除しないようにする。（key が疎になるため）
5. 31bit より大きい数字は V8 が box するため、できる限り 31bit の符号付き数字を使う

<!--
_footer: 参考：https://blog.sessionstack.com/how-JavaScript-works-inside-the-v8-engine-5-tips-on-how-to-write-optimized-code-ac089e62b12e
-->

---

# OOP

○ コードをクリーンにできる
× 継承におけるデメリット

- Tight Coupling: 継承元の Base となっている Class に新しいメソッドを追加すると、子クラス全てに影響する
- Hierarchy: 親クラスの一部しか利用したくない時でも全て継承する

→ 大量の Obj が必要で、操作の変更があまりなく、状態を持っているものに関しては向いている（ゲームキャラクターなど）

---

# OOP

非効率な実装

```JavaScript
const elf1 = {
  name: 'Dobby',
  type: 'house',
  weapon: 'cloth',
  say: function() {
    return `Hi, my name is ${this.name}, I am a ${this.type} elf.`
  }
  attack: function() {
    return `attack with ${this.weapon}`
  }
}

const elf2 = { ... } // ほとんど同じ内容をもう一度書く
```

<!--
_footer: https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
-->

---

# OOP

Factory Functions

```JavaScript
function createElf(name, type, weapon) {
  return {
    name: name,
    type: type,
    weapon: weapon,
    say() {
      return `Hi, my name is ${name}, I am a ${type} elf.`;
    },
    attack() {
      return `${name} attacks with ${weapon}`;
    }
  };
}
const dobby = createElf("Dobby", "house", "cloth");
```

<!--
_footer: https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
-->

---

# OOP

Stores

```JavaScript
const elfMethodsStore = {
  attack() {
    return `attack with ${this.weapon}`;
  },
  say() {
    return `Hi, my name is ${this.name}, I am a ${this.type} elf.`;
  }
};
function createElf(name, type, weapon) {
  return { name, type, weapon };
}
const dobby = createElf("Dobby", "house", "stick");
dobby.attack = elfMethodsStore.attack;
dobby.say = elfMethodsStore.say;
```

<!--
_footer: https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
-->

---

# OOP

Object.create (prototypal inheritance)

```JavaScript
const elfMethodsStore = {
  attack() {
    return `attack with ${this.weapon}`;
  }
};

function createElf(weapon) {
// this creates the __proto__ chain to the store
  let newElf = Object.create(elfMethodsStore);
  newElf.weapon = weapon;
  return newElf;
}

const dobby = createElf("stick");
```

<!--
_footer: https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
-->

---

# OOP

Constructor Functions (new Keyword)

```JavaScript
function Elf(name, type, weapon) {
  this.name = name;
  this.type = type;
  this.weapon = weapon;
}

const dobby = new Elf("Dobby", "house", "cloth");

// cannot be an arrow function
Elf.prototype.attack = function() {
  return `attack with ${this.weapon}`;
};
dobby.attack();
```

<!--
_footer: https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
-->

---

# OOP

Class

```JavaScript
class Character {
  constructor(name, weapon) {
    this.name = name;
    this.weapon = weapon;
  }
  attack() {
    return `attack with ${this.weapon}`;
  }
}
class Ogre extends Character {
  constructor(name, weapon, color) {
    super(name, weapon);
    this.color = color;
  }
}
```

<!--
_footer: https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
-->

---

# FP

○ テスタブルな実装ができる
△ 状態をもったり、API にアクセスする必要のあるものが出てくるため、全てを純粋関数にすることはできない。

---

# FP

```JavaScript
const compose = (fn1, fn2) => data => fn1(fn2(data));
const pipe = (fn1, fn2) => data => fn2(fn1(data));
const multiplyBy3 = num => num * 3;
const makePositive = num => Math.abs(num);

const composeFn = compose(multiplyBy3, makePositive);
const pipeFn = pipe(multiplyBy3, makePositive);

composeFn(-50); // 150
pipeFn(-50); // 150
```

[EC システムの例](https://repl.it/@kotadd/FP-9#index.js)

<!--
_footer: https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
-->

---

# コラム：Immutability は効率的なのか

単純にコピーして要素を再作成するのなら、
メモリや速度の観点から非効率ではないのか？

```JavaScript
const obj1 = { a: 'a', b: 'b' }
// obj1.c = 'c'

// Immutableな実装
const obj2 = Object.assign({}, obj1, {c: 'c'} )
```

<!--
_footer: https://www.youtube.com/watch?v=Wo0qiGPSV-s
-->

---

# コラム：Immutability は効率的なのか

## Structural Sharing を利用しているため、非効率にならない

<!--
_footer: https://ja.wikipedia.org/wiki/%E6%B0%B8%E7%B6%9A%E3%83%87%E3%83%BC%E3%82%BF%E6%A7%8B%E9%80%A0
-->

---

# コラム：Immutability は効率的なのか

![bg 50%](https://hypirion.com/sha/29bd11f8507cddd860f00fc03166fc84e7a0d0c0cf2e684066a7acc3076cd033.png)

<!--
class: main
_footer: https://hypirion.com/musings/understanding-persistent-vector-pt-1
-->

---

# コラム：Immutability は効率的なのか

## メリット

- Predictability
- Performance
- Mutation Tracking

→ 可能な限り Immutable な実装にしていく方が良い

<!--
class: noclass
_footer: https://stackoverflow.com/questions/34385243/why-is-immutability-so-important-or-needed-in-javascript
-->

---

# コラム：Private Fields

```JavaScript
class Rectangle {
  #height = 0;
  #width;
  constructor(height, width) {
    this.#height = height;
    this.#width = width;
  }
  getHeight() { return this.#height }
}
```

<!--
class: noclass
_footer: https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts
-->

---

# EOP

<!--
class: title
-->
