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

- V8 を使用し、**Rust** で構築されたシンプルでモダンな JavaScript と **TypeScript** のための**セキュア**な実行環境

  - 参考：NodeJS は V8 を使用し、C++で構築された JavaScript で動作する実行環境

- Ryan Dahl 氏によって開発された

<!--
class: noclass
_footer: https://deno.land/
-->

---

# 余談

- 当初 Deno は Go で実装されていたが、高速化のために Rust で再実装されている。
- Rust は 2016-2020 年にわたって、最も愛された言語でトップ。

<!--
_footer: https://insights.stackoverflow.com/survey/2020#technology-most-loved-dreaded-and-wanted-languages-loved

-->

---

# NodeJS について

- NodeJS は「イベントドリブンな HTTP Server を作れるようにすること」を目的に開発された。
- Ryan Dahl 氏が 2018 年に利用した際に、いくつかの反省点が見つかった。

<!--
_footer: https://youtu.be/M3BM9TB-8yA \n https://yosuke-furukawa.hatenablog.com/entry/2018/06/07/080335
-->

---

# Deno は NodeJS の反省点から生まれた 1

- NodeJS のコアに Promise がないこと
- Security が甘いこと
  - linter もネットワークリソースにアクセスができてしまう
- Build System (GYP) が複雑なこと

<!--
_footer: 参考：https://yosuke-furukawa.hatenablog.com/entry/2018/06/07/080335 \n 　　　https://news.mynavi.jp/article/programinglanguageoftheworld-34/
-->

---

# Deno は NodeJS の反省点から生まれた 2

- package.json を利用した中央集権リポジトリ
  - local なのか npm の DB の中なのかわからない
  - ライセンスなども含めてインポートする
- module loader はユーザーの意図を表現するファイルシステムへのクエリーであるべき
  - .js の拡張子なしで module を読み込ませられる
  - index.js が require("./") で読み込める

<!--
_footer: 参考：https://yosuke-furukawa.hatenablog.com/entry/2018/06/07/080335 \n 　　　https://news.mynavi.jp/article/programinglanguageoftheworld-34/
-->

---

# 主要な特徴

- ホワイトリスト形式でネットワーク, I/O 接続を許可する
- TypeScript がデフォルトで利用できる
- 単一の実行ファイル
- built-in のツールが数多くある(lint, fmt, info)
- 多数の標準ライブラリ（標準ブラウザとの互換性向上）

<!--
_footer: https://deno.land/
-->

---

# その他の特徴

- node_modules がない（モジュールの非中央化）
- await がトップレベルで利用できる
- ブラウザ互換 API が利用できる(fetch など)
- 標準のテストランナー（jest 不要）

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
- セキュリティが NodeJS よりも厳格になっている

---

# 参考になりそうなサイト

https://zenn.dev/uki00a/books/effective-deno/viewer/cheatsheet
