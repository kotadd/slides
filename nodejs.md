---
marp: true
theme: common
paginate: true
---

# Node.js

<!--
class: title
-->

---

# Node.js とは

ファイル操作などマシンに近い処理を行う、V8(ECMA Script)を利用できるようにした**JavaScript の実行環境**

<!--
class: noclass
_footer: 参考：https://www.udemy.com/course/understand-Node.js/ \n 　　　https://Node.js.org/ja/about/
-->

---

# トピック

1. Node.js Runtime
2.

---

# Node.js Runtime

![bg 80%](https://miro.medium.com/max/1200/0*wpCPDuttKg1fEL6S.jpg)

<!--
class: main
_footer: 参考：https://medium.com/jspoint/how-JavaScript-works-in-browser-and-node-ab7d0d09ac2f
-->

---

# 言語の抽象度

↑ JavaScript（ブラウザ）
↑ C/C++, PHP, Python (PC) <- Node.JS
↑ Assembly Language
↑ Macine Language

JavaScript はブラウザで実行することを目的としていたため、C++などのようにファイル操作など OS に近い部分の処理を行うことができなかった。

<!--
class: noclass
-->

---

# LIBUV

---

# Node.js の特徴

- **Non-blocking I/O**
  - Event Loop
  - Single Thread

**→ 大量の同時接続をさばけるネットワークアプリケーションの構築がしたい**

<!--
class: noclass
_footer: 参考：https://Node.js.org/en/docs/guides/
-->

---

# コラム：C10K 問題

apache-> nginx の時代から騒がれていた問題。

> ハードウェアの性能上は問題がなくても、クライアント数があまりにも多くなるとサーバがパンクする問題のこと。
> C は「Client（クライアント）」の頭文字、10K は「1 万台」を意味する。
> 「クライアント 1 万台問題」ともいわれる。

<!--
_footer: 参考：https://d.hatena.ne.jp/keyword/C10K%20%E5%95%8F%E9%A1%8C
-->

---

# コラム：apache と nginx

## apache: マルチスレッド・マルチプロセス

リクエストに応じてスレッド/プロセスを立ち上げる仕組み。
スレッド/プロセスが増えるほどメモリ使用率が上昇するため、**コンテキストスイッチ**が多く発生し、**C10K 問題**が発生する。

## nginx: イベント駆動

イベントが発生するまで待機し、発生したイベントの種類に応じて実行される。

<!--
class: noclass
_footer: 参考：https://qiita.com/i-tanaka730/items/79e8e2c3ceb2bde51436 \n　　　https://blog.mosuke.tech/entry/2016/06/04/180122/
-->

---

# コラム：コンテキストスイッチ

> コンテキストスイッチとは、コンピュータの処理装置（CPU）が現在実行している処理の流れ（プロセス、スレッド）を一時停止し、別のものに切り替えて実行を再開すること。

http://e-words.jp/w/%E3%82%B3%E3%83%B3%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88%E3%82%B9%E3%82%A4%E3%83%83%E3%83%81.html

---

# Non-blocking I/O とは

非同期処理のなかでも I/O など JS 以外の操作も非同期で動作すること

(Non Blocking I/O ⊂ 非同期処理)

> I/O: システムのディスクやネットワークとのやり取り
> blocking： Node.js プロセス内で実行された JavaScript が、JavaScript 以外の操作が完了するまで待たなければならない状態のこと

**→ Node.js は標準で非同期（Non-blocking）なメソッドを提供している。**

<!--
_footer: 参考：https://Node.js.org/en/docs/guides/blocking-vs-non-blocking/
-->

---

# 同期・非同期処理について

同期

```JavaScript
const fs = require('fs')
const data = fs.readFileSync('/file.md') // ファイルが読み込まれるまでここでブロック
console.log(data)
moreWork() // console.log の後に実行されます
```

非同期

```JavaScript
const fs = require('fs')
fs.readFile('/file.md', (err, data) => {
  if (err) throw err
  console.log(data)
})
moreWork() // console.log の前に実行されます
```

<!--
_footer: 参考：https://Node.js.org/en/docs/guides/blocking-vs-non-blocking/
-->

---

# コラム：Non-blocking I/O と Node.js

Non-blocking I/O を利用しているものは複数ある。

> Python: Twisted
> Ruby: EventMachine
> Perl: Colo の AnyEvent

だが、どれも Non-Blocking の I/O を強制していないため、スレッドで書かれた同様の処理をするプログラムよりも遅い場合がある。

**-> Node.js は Non-Blocking I/O の使用を強制する**

<!--
_footer: 参考：https://badatmath.hatenablog.com/entry/20101020/1287587240
-->

---

# Node.js はクライアントサイドでは利用されないのか

Node.js の**コアの機能**はサーバーサイドで利用される。だが、あくまで Node.js は Javascript をブラウザ上だけでなく OS のシステムに関与可能にするための**実行環境**を指しているため、クライアントサイドでも Node.js 自体は利用される。

例：Node.js を利用しているもの

1. Babel: ES6 以降のコードを ES5 に変換する際に利用される
2. Jest: テストツール
3. ESLint: コード検証ツール
4. Gatsby: 静的サイトのビルド

<!--
_footer: 参考：https://qiita.com/non_cal/items/a8fee0b7ad96e67713eb
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

1. object の初期化は同じ順序で行うこと
2. constructor で全ての property をセットすること
3. (inline caching により) 同じメソッドを繰り返し実行するコードの方が異なるメソッドを一度だけ実行するよりも速い
4. key が incremental でない疎な配列を避ける。大きな配列に事前に割り当てることや配列の要素を削除しないようにする。（key が疎になるため）
5. 31bit より大きい数字は V8 が box するため、できる限り 31bit の符号付き数字を使う

<!--
_footer: 参考：https://blog.sessionstack.com/how-JavaScript-works-inside-the-v8-engine-5-tips-on-how-to-write-optimized-code-ac089e62b12e
-->

---

# EOP

<!--
class: title
-->
