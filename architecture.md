---
marp: true
theme: common
paginate: true
---

<!--
class: title
-->

# Architectures

---

# Flux

---

<!--
class: noclass
_footer: 参考：https://facebook.github.io/flux/
-->

# Flux

Flux は MVC への批判から生まれた
「MVC は機能を追加しようとするたびに肥大化して壊れやすくなる」
→ Model と View の間でデータフローが入り乱れていると考えられた

---

<!--
class: main
_footer: 参考：https://github.com/facebook/flux/tree/master/examples/flux-concepts
-->

# Flux

![bg 100%](https://github.com/facebook/flux/blob/master/examples/flux-concepts/flux-simple-f8-diagram-with-client-action-1300w.png?raw=true)

---

# Flux

- メリット
  - どこに何を書けば良いのかが明確
  - データの流れがわかりやすいので、デバッグしやすい
  - View から状態管理を消すこともできる
  - スケーラビリティが高い
- デメリット
  - 記述が冗長になりがち
  - 規模の大きなアプリケーションだと、Action が肥大化する

---

<!--
class: title
-->

# Redux

---

<!--
class: noclass
_footer: 参考：https://redux.js.org/understanding/history-and-design/prior-art
-->

# Redux とは

- Flux と Elm(関数型言語)の影響を強く受けたアーキテクチャ。
- 変化と非同期性を解決するために提唱された。

→ 更新がどのタイミングで起きるのかを明確にし、整合性の取れた状態管理を実現する

---

<!--
class: main
_footer: https://app.diagrams.net/#G1HIdCatMpOyTdhuQAyEpp_Ltx4wdcPIMb
-->

# Redux

![bg 80%](./architecture/redux/redux.svg)

---

# Redux のコンセプト

- Single source of truth
  - アプリ全体を単一の State で管理する
- State is read-only
  - Reducer が新しい State を生成するまで、現在の State は変更されない
- Changes are made with pure functions
  - Reducer が純粋関数である

---

# Redux

- メリット
  - （Flux と同じく、）双方向のデータフローと比較してシンプル
  - View と Redux のレイヤーがそれぞれ独立して存在している（互いに関知しない）
- デメリット
  - 関数の再利用性の低下

---

<!--
class: title
-->

# React Hooks

---

<!--
class: noclass
-->

# React Hooks とは

関数コンポーネントに React の機能（ローカルステート、ライフサイクルメソッドなど）を利用可能にしたもの。

---

<!--
_footer: 参考：https://ja.reactjs.org/docs/hooks-intro.html
-->

# React Hooks の特徴

- Class を利用せずに State Full なロジックを記述できる
  - 責務（関心）を分離することができるようになった
  - 純粋関数は View(UI)
  - Hooks は状態、ロジック、ライフサイクル（※副作用)

→ 結果的にテストがしやすくなった

※副作用：引数から戻り値を求めること以外の仕事（変数の変更や外部入出力）

---

<!--
class: noclass
-->

# React Hooks で何を実現したいのか

- 凝集度をあげたい
  - 機能的に関係のあるもので関数をまとめたい
- UI コンポーネントを純粋関数にしたい

---

# EOP

<!--
class: title
-->
