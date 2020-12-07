---
marp: true
theme: common
paginate: true
---
# NodeJS

<!--
class: title
-->

---
# NodeJSとは何か

JavaScriptが(C++と同様に)ファイル操作などマシンに近い処理を実施することができる、V8(ECMA Script)を利用できるようにしたもの。
**→ 非同期型イベント駆動の JavaScript**

<!--
class: noclass
_footer: 参考：https://www.udemy.com/course/understand-nodejs/ \n 　　　https://nodejs.org/ja/about/
-->

---
# NodeJSの特徴

* **Non-blocking I/O**
  * Event Loop
  * Single Thread

<!--
class: noclass
_footer: 参考：https://nodejs.org/en/docs/guides/
-->

---
# Non-blocking I/Oとは

非同期処理のなかでもI/OなどJS以外の操作も非同期で動作すること

(Non Blocking I/O ⊂ 非同期処理)


> I/O: システムのディスクやネットワークとのやり取り
> blocking： NodeJSプロセス内で実行されたJavaScriptが、JavaScript以外の操作が完了するまで待たなければならない状態のこと

**→ NodeJSは標準で非同期（Non-blocking）なメソッドを提供している。**

<!--
_footer: 参考：https://nodejs.org/en/docs/guides/blocking-vs-non-blocking/
-->

---
# 同期・非同期処理について

同期

```javascript
const fs = require('fs');
const data = fs.readFileSync('/file.md'); // ファイルが読み込まれるまでここでブロック
console.log(data);
moreWork(); // console.log の後に実行されます
```

非同期

```javascript
const fs = require('fs');
fs.readFile('/file.md', (err, data) => {
  if (err) throw err;
  console.log(data);
});
moreWork(); // console.log の前に実行されます
```

<!--
_footer: 参考：https://nodejs.org/en/docs/guides/blocking-vs-non-blocking/
-->

---

# Event Loop

![bg 60%](./nodejs/EventLoop.png)

<!--
class: main
_footer: 参考：https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/
-->

---

# Event Loop

* timers: setTimeout()やsetInterval()でスケジュールされたcallbacksを実行する
* pending callbacks: 次のループに置かれた I/O callbacks を実行する
* idle, prepare: 内部利用
* poll: 新しい I/O イベントの取得。 I/O 関係のcallbackを実行 (close callbacksの例外の大半、timersやsetImmediate()にスケジュールされたもの)。 適切な場合、nodeはここでロックする。
* check: setImmediate() callbacks がここで呼ばれる。
* close callbacks: close callbacksの何かしら。 例） socket.on('close', ...).

<!--
_footer: 参考：https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/
-->

---
# timers

```JavaScript
const fs = require('fs');
function someAsyncOperation(callback) {
  fs.readFile('/path/to/file', callback); // Assume this takes 95ms to complete
}
const timeoutScheduled = Date.now();
setTimeout(() => {
  const delay = Date.now() - timeoutScheduled;
  console.log(`${delay}ms have passed since I was scheduled`);
}, 100);

someAsyncOperation(() => { // do someAsyncOperation which takes 95 ms to complete
  const startCallback = Date.now();
  while (Date.now() - startCallback < 10) { // do something that will take 10ms...
  }
});
```
---
# コラム：apache と nginx

## apache: スレッド

実行スタックをコピーする必要がある。スレッドが増えるほどメモリ使用率が上昇する。

## nginx: イベントループ

シングルスレッドなので、メモリで有意。
ただし、コードのどこかでブロックする処理が発生するとプロセス全体がストップする。

<!--
class: noclass
-->

---
# コラム：Non-blocking I/OとNodeJS

Non-blocking I/Oを利用しているものは複数ある。
> Python: Twisted
> Ruby: EventMachine
> Perl: ColoのAnyEvent

だが、どれもNon-BlockingのI/Oを強制していないため、スレッドで書かれた同様の処理をするプログラムよりも遅い場合がある。

**-> NodeJSはNon-Blocking I/O の使用を強制する**

<!--
_footer: 参考：https://badatmath.hatenablog.com/entry/20101020/1287587240
-->
