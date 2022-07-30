---
marp: true
theme: common
paginate: true
---

# JavaScript の基本文法

<!--
class: title
-->

---

# Array#flat

Array#flat メソッドは必ず新しい配列を作成して返す

```JavaScript
const array = [[["A"], "B"], "C"];
// 引数なしは 1 を指定した場合と同じ
console.log(array.flat()); // => [["A"], "B", "C"]
console.log(array.flat(1)); // => [["A"], "B", "C"]
console.log(array.flat(2)); // => ["A", "B", "C"]
// すべてをフラット化するには Infinity を渡す
console.log(array.flat(Infinity)); // => ["A", "B", "C"]
```

<!--
class: noclass
_footer: https://jsprimer.net/basic/array/
-->

---

# Array#splice

配列から要素を削除する

```JavaScript
const array = ["a", "b", "c"];
// 1番目から1つの要素("b")を削除
array.splice(1, 1);
console.log(array); // => ["a", "c"]
console.log(array.length); // => 2
console.log(array[1]); // => "c"
// すべて削除
array.splice(0, array.length);
console.log(array.length); // => 0

```

<!--
_footer: https://jsprimer.net/basic/array/
-->

---

# Mutable vs Immutable

Mutable

```JavaScript
const myArray = ["A", "B", "C"];
const result = myArray.push("D");
console.log(result); // => 4
console.log(myArray); // => ["A", "B", "C", "D"]
```

Immutable

```JavaScript
const myArray = ["A", "B", "C"];
const newArray = myArray.concat("D");
console.log(myArray); // => ["A", "B", "C"]
console.log(newArray); // => ["A", "B", "C", "D"]
console.log(myArray === newArray); // => false
```

<!--
_footer: https://jsprimer.net/basic/array/
-->

---

# Array#slice

```JavaScript
const myArray = ["A", "B", "C"];
// `slice`は`myArray`のコピーを返す - `myArray.concat()`でも同じ
const copiedArray = myArray.slice();
myArray.push("D");
console.log(myArray); // => ["A", "B", "C", "D"]
console.log(copiedArray); // => ["A", "B", "C"]
console.log(copiedArray === myArray); // => false
```

<!--
_footer: https://jsprimer.net/basic/array/
-->

---

# Array#forEach,map,filter

引数が「要素, インデックス, 配列」

```JavaScript
// 例）
const array = [1, 2, 3];
const newArray = array.filter((currentValue, index, array) => {
    return currentValue % 2 === 1;
});
```

<!--
_footer: https://jsprimer.net/basic/array/
-->

---

# Array#reduce

累積値（アキュムレータ）と配列の要素を順番にコールバック関数へ渡し、1 つの累積値を返す。
引数：累積値, 要素, インデックス, 配列

```JavaScript
const array = [1, 2, 3];
const totalValue = array.reduce((accumulator, currentValue, index, array) => {
    return accumulator + currentValue;
}, 0);
console.log(totalValue); // => 6
```

<!--
_footer: https://jsprimer.net/basic/array/
-->

---

# slice,substring の使いどころ

```JavaScript
const url = "https://example.com?param=1";
const indexOfQuery = url.indexOf("?");
const queryString = url.slice(indexOfQuery);
console.log(queryString); // => "?param=1"
```

<!--
_footer: https://jsprimer.net/basic/string/
-->

---

# 正規表現リテラルと RegExp コンストラクタの違い

##### 正規表現リテラル

- ソースコードをロード（パース）した段階で正規表現のパターンが評価

##### RegExp コンストラクタ

- 実際に RegExp コンストラクタを呼び出すまでパターンは評価されない

```JavaScript
// `[`は対となる`]`を組み合わせる特殊文字であるため、単独で書けない
function main() {
    // リテラル
    // const invalidPattern = /[/; //この時点でエラー

    // RegExp:main関数が呼ばれたときにエラー：-> 正規表現のパターンに変数を利用する場合に使える
    const invalidPattern = new RegExp("[");
}
```

<!--
_footer: https://jsprimer.net/basic/string/
-->

---

# 正規表現による検索

#### String#search

```JavaScript
const str = "ABC123EFG";
const searchPattern = /\d{3}/;
console.log(str.search(searchPattern)); // => 3
```

<!--
_footer: https://jsprimer.net/basic/string/
-->

---

# 正規表現による検索

#### match

```JavaScript
const str = "ABC あいう DE えお";
const alphabetsPattern = /[a-zA-Z]+/g;
const resultsWithG = str.match(alphabetsPattern);
console.log(resultsWithG.length); // => 2
console.log(resultsWithG[0]); // => "ABC"
console.log(resultsWithG[1]); // => "DE"
// indexとinputはgフラグありの場合は追加されない
console.log(resultsWithG.index); // => undefined
console.log(resultsWithG.input); // => undefined
```

<!--
_footer: https://jsprimer.net/basic/string/
-->

---

# 正規表現による検索

#### matchAll

```JavaScript
const str = "ABC あいう DE えお";
const alphabetsPattern = /[a-zA-Z]+/g;
// matchAllはIteratorを返す
const matchesIterator = str.matchAll(alphabetsPattern);
for (const match of matchesIterator) {
    // マッチした要素ごとの情報を含んでいる
    console.log(`match: "${match[0]}", index: ${match.index}, input: "${match.input}"`);
}
// 次の順番でコンソールに出力される
// match: "ABC", index: 0, input: "ABC あいう DE えお"
// match: "DE", index: 8, input: "ABC あいう DE えお"
```

<!--
_footer: https://jsprimer.net/basic/string/
-->

---

# 正規表現による検索

#### マッチした文字列の一部を取得

```JavaScript
const pattern = /ES(\d+)/g;
const matchesIterator = "ES2015、ES2016、ES2017".matchAll(pattern);
for (const match of matchesIterator) {
    console.log(`
      match: "${match[0]}",
      capture1: ${match[1]},
      index: ${match.index},
      input: "${match.input}"
    `);
}
// 次の順番でコンソールに出力される
// match: "ES2015", capture1: 2015, index: 0, input: "ES2015、ES2016、ES2017"
// match: "ES2016", capture1: 2016, index: 7, input: "ES2015、ES2016、ES2017"
// match: "ES2017", capture1: 2017, index: 14, input: "ES2015、ES2016、ES2017"
```

<!--
_footer: https://jsprimer.net/basic/string/
-->

---

# 正規表現による検索

#### RegExp#exec

```JavaScript
const str = "ABC あいう DE えお";
const alphabetsPattern = /[a-zA-Z]+/g;
console.log(alphabetsPattern.lastIndex); // => 0
const result1 = alphabetsPattern.exec(str);
console.log(result1[0]); // => "ABC"
console.log(alphabetsPattern.lastIndex); // => 3
const result2 = alphabetsPattern.exec(str);
console.log(result2[0]); // => "DE"
console.log(alphabetsPattern.lastIndex); // => 10
const result3 = alphabetsPattern.exec(str);
console.log(result3); // => null
console.log(alphabetsPattern.lastIndex); // => 0
```

<!--
_footer: https://jsprimer.net/basic/string/
-->

---

# 正規表現による検索

#### 真偽値を取得

```JavaScript
const str = "にわにはにわにわとりがいる";
console.log(/^にわ/.test(str)); // => true
console.log(/^いる/.test(str)); // => false

console.log(/にわ$/.test(str)); // => false
console.log(/いる$/.test(str)); // => true

console.log(/にわ/.test(str)); // => true
console.log(/いる/.test(str)); // => true
```

<!--
_footer: https://jsprimer.net/basic/string/
-->

---

# [ES2015] タグつきテンプレート関数

```JavaScript
function tag(strings, ...values) {
    console.log(strings); // => ["template "," literal ",""]
    console.log(values); // => [0, 1]
}
tag`template ${0} literal ${1}`;

```

<!--
_footer: https://jsprimer.net/basic/string/
-->

---

# [ES2015] タグつきテンプレート関数

#### 変数を URL エスケープするタグ関数

```JavaScript
function escapeURL(strings, ...values) {
    return strings.reduce((result, str, i) => {
        return result + encodeURIComponent(values[i - 1]) + str;
    });
}

const input = "A&B";
const escapedURL = escapeURL`https://example.com/search?q=${input}&sort=desc`;
console.log(escapedURL); // => "https://example.com/search?q=A%26B&sort=desc"
```

<!--
_footer: https://jsprimer.net/basic/string/
-->

---

# 文字コード

JavaScript は文字コードとして Unicode を採用し、エンコード方式として UTF-16 を採用しています

<!--
_footer: https://jsprimer.net/basic/string-unicode/
-->

---

# クロージャー

外側のスコープにある変数への参照を保持できる」という関数が持つ性質

```JavaScript
function createCounter() {
    let count = 0;
    function increment() {
        count = count + 1;
        return count;
    }
    return increment;
}
const myCounter = createCounter();
myCounter(); // => 1
myCounter(); // => 2
const newCounter = createCounter();
newCounter(); // => 1
newCounter(); // => 2
```

<!--
_footer: https://jsprimer.net/basic/function-scope/
-->

---

# クロージャー

性質

- 関数に状態を持たせる
- 外から参照できない変数を定義する
- グローバル変数を減らす
- 高階関数の一部

<!--
_footer: https://jsprimer.net/basic/function-scope/
-->

---
