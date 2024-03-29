---
marp: true
theme: common
paginate: true
math: mathjax
---

# マイナス同士をかけるとなぜプラスになるのか

<!--
class: title
-->

---

# 前置き

代数学（数式）的に考えると $「-1×-1 = 1」$ になるのは当然だと教えられてきましたが、そもそもマイナスのものとマイナスのものを掛けるとプラスになるというのは、自然数しか存在しない現実では経験的にわかりません。
ただ、幾何学的に考えると、なんとなくわかってきます。

<!--
  class: noclass
-->

---

# 数学の前提知識

■ 虚数$i$
二乗にすると$-1$ となる、数学上でできなかった計算をするために作られたもの

$$
\begin{align}
1*i = i \tag{1} \\
i*i = -1 \tag{2} \\
1*i = -i \tag{3} \\
-i*i = 1 \tag{4} \\
\end{align}
$$

---

# 公式を読み解く

- 1 と-1 は反対の関係にありますが、上記から i と-i の関係も反対向きの関係と考えられます。
- x 軸のみを考えると、1 は右に 1 つ、-1 は左に一つ進みます
- 同様に y 軸のみを考えると、i は上に 1 つ、-i は下に一つ進むと考えることができます
- このことを踏まえると、原点を中心にした単位円（半径が 1）において次の関係性があります。

---

# 図形で考える

## （適当にとってきた画像なので、オイラーの公式という部分は無視してください）

![bg 40%](./img.png)

<!--
class: main
-->

---

# 図形を読み解く

図のとおり、$x$軸が$1$と$-1$, $y$軸が$i$と$-i$なので、下記のようになります

$$
\begin{align}
1: 0度 \tag{1} \\
i:90度 \tag{2} \\
-1:180度 \tag{3} \\
-i:270度 \tag{4} \\
\end{align}
$$

<!--
class: noclass
-->

---

# 公式の解釈

$$
\begin{align}
1*i = i \tag{1} \\
i*i = -1 \tag{2} \\
1*i = -i \tag{3} \\
-i*i = 1 \tag{4} \\
\end{align}
$$

先ほどの公式と見比べてみると、
**ある数値に i を掛けることは 90 度「回転」させることと同義である**と考えられます

---

# マイナス同士をかけるとなぜプラスになるのか

$-1$は先ほどの公式から、**180 度回転させること** と考えられるので、
$-1×-1$は 180 度の回転を $2$ 回行うことと考えられます。

結果的に一周回って右(0 度 or 360 度) に戻ってくるというお話です。

---

# 解釈する力が身につく気がする

1 と-1 が反対という考えだけでは同じ方向のものをかけて逆向きになる意味がわかりませんが、回転ととらえると理解できる。
幾何学の面白さに自分が初めて触れた内容でした。
