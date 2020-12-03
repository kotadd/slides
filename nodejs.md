---
marp: true
theme: default
paginate: true
---
# NodeJS

---
# NodeJSとは何か

JavaScriptが(C++と同様に)ファイル操作などマシンに近い処理を実施することができる、V8(ECMA Script)を利用できるようにしたもの。

<!--
class: main
_footer: 参考：https://www.udemy.com/course/understand-nodejs/
-->

---
# NodeJSの特徴

* Non-blocking I/O
* シングルスレッド

---
# Non-blocking I/Oとは

I/O: システムのディスクやネットワークとのやり取り
blocking： NodeJSプロセス内で実行されたJavaScriptが、JavaScript以外の操作が完了するまで待たなければならない状態のこと

**NodeJSは標準で非同期（Non-blocking）なメソッドを提供している。**

<!--
class: main
_footer: 参考：https://nodejs.org/en/docs/guides/blocking-vs-non-blocking/
-->

---

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
class: main
_footer: 参考：https://nodejs.org/en/docs/guides/blocking-vs-non-blocking/
-->

---
# コラム：apache と nginx

## apache: スレッド

実行スタックをコピーする必要がある。スレッドが増えるほどメモリ使用率が上昇する。

## nginx: イベントループ

シングルスレッドなので、メモリで有意。
ただし、コードのどこかでブロックする処理が発生するとプロセス全体がストップする。

---
# コラム：Non-blocking I/OとNodeJS

Non-blocking I/Oを利用しているものは複数ある。
> Python: Twisted
> Ruby: EventMachine
> Perl: ColoのAnyEvent

だが、どれもNon-BlockingのI/Oを強制していないため、スレッドで書かれた同様の処理をするプログラムよりも遅い場合がある。

**-> NodeJSはNon-Blocking I/O の使用を強制する**

<!--
class: main
_footer: 参考：https://badatmath.hatenablog.com/entry/20101020/1287587240
-->
