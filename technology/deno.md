---
marp: true
theme: common
paginate: true
---

# Deno

<!--
class: title
-->

---

# Deno とは

Deno は、V8 を使用し、Rust で構築されたシンプルでモダンな JavaScript と TypeScript のためのセキュアなランタイム。

> Deno is a simple, modern and secure runtime for JavaScript and TypeScript that uses V8 and is built in Rust.

<!--
class: noclass
_footer: https://deno.land/
-->

---

# なぜ作られたのか

Node.JS の反省点から

- Node.JS のコアに Promise がないこと
- Security が緩かった。（linter もネットワークリソースにアクセスができてしまう）
- Build System (GYP)
- package.json（local なのか npm の中なのかわからない点やライセンスなども含めてインポートする点）
- .js の拡張子なしで module を読み込ませられるようにしたこと（module loader はユーザーの意図を表現するファイルシステムへのクエリーであるべき）
- index.js が require("./") で読み込めること（同上の理由）

<!--
_footer:https://yosuke-furukawa.hatenablog.com/entry/2018/06/07/080335
-->

---

# 実行環境

## Node.JS の仕組み

![bg 70%](https://miro.medium.com/max/1200/0*wpCPDuttKg1fEL6S.jpg)

<!--
class: main
_footer: 参考：https://medium.com/jspoint/how-JavaScript-works-in-browser-and-node-ab7d0d09ac2f
-->

---

# 主要な特徴

- ホワイトリスト形式でネットワーク, I/O 接続を許可する
- TypeScript built-in
- ただ一つの実行ファイル
- built-in のツールが数多くある(lint, fmt, info)
- 多数の標準ライブラリ

<!--
_footer: https://deno.land/
-->

---

# その他の特徴

- node_modules がない（モジュールの非中央化）
- await がトップレベルで利用できる
- ブラウザ互換 API が利用できる(fetch など)
- 標準のテストランナー

<!--
_footer: https://qiita.com/azukiazusa/items/8238c0c68ed525377883
-->

---

# node_modules がないということ

![bg 50%](https://cdn-ak.f.st-hatena.com/images/fotolife/y/yosuke_furukawa/20180604/20180604215229.png)

<!--
class: main
_footer: https://qiita.com/azukiazusa/items/8238c0c68ed525377883
-->

---

# まとめ

- 標準でまかなえる範囲が多く、ソースコードがスッキリする
- セキュリティが Node.JS よりも厳しくなっている
