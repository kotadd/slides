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

# Javascript Engine

![bg 80%](https://images.ctfassets.net/aq13lwl6616q/3o7Q3edCrVJG9Zzj6VMZ1K/28136a643636dfa04090f3fb5c5467ff/javascript_engine.png)


<!--
class: main
_footer: 参考：https://zerotomastery.io/cheatsheets/javascript-cheatsheet-the-advanced-concepts/#the-interpreter
-->

---

# 処理の順序

Call Stack: functionなどをstackし、実行箇所を把握できるもの
→ Stack Overflowを引き起こす

Memory Heap: メモリの一時保管領域
→ memory leaksを引き起こす

<!--
class: noclass
-->

---

# このコードを再帰を保ったまま修正するには？

```javascript
const list = new Array(60000).join('1.1').split('.');

function removeItemsFromList() {
    var item = list.pop();

    if (item) {
        removeItemsFromList();
    }
};

removeItemsFromList();
```
[解説の図](https://viewer.diagrams.net/?highlight=0000ff&edit=_blank&layers=1&nav=1&title=callbackqueue.drawio#R3VrLcpswFP0aZtpFO4iXYWk7TpqZZJqOF2mXMqhAC4gRcmzy9RUgzEM4phPbQFZGR9IFHR1dcWQkdRnu7wiMvUfsoEBSZGcvqTeSogBNMdhPhqQFMgNaAbjEd3ijClj7r4iDMke3voOSRkOKcUD9uAnaOIqQTRsYJATvms1%2B46B51xi6SADWNgxE9Nl3qFegpjKr8G%2FId73yzsCwipoQlo35SBIPOnhXg9SVpC4JxrS4CvdLFGTklbwU%2FW6P1B4ejKCI9unw%2FRlYpvZoze%2FmD%2FpmBl61bfKFR3mBwZYPWFqpkqlKi4WkGAELvNgQduVmV%2F2q8rHStCSQ4G3koOwZZNZu5%2FkUrWNoZ7U7JhmGeTQMWAlkYYQxlQ%2BICEX7GsTHeIdwiChJWRNea3K6ud5ASf%2Bumj2gccyrzZwicxByxbiH0BWp7ILz%2Bh8cKwLHS5j3WlNo%2FxUIY%2BOkTVZg4LsRu7YZK4gwIGPDZxqd84rQd5ys%2B4KgxH%2BFmzxURneM%2FYjm49EXkn6TxdpSnBSr7EyEA7nFuCoyPusk%2FEJ8q6Kmhxal1uZoeFVqAkvPaDN%2Fup%2B8HjVFP6lH45p61Menx1aSPMhzODkanUlykydI%2BccWMXTqwjSbutRAB%2BnyNYU5EzgnKMQv6J6iMLklOHzwE%2Frp89jUqvZX64WIM6dJ3KE8GHHWRIkzhiauzBWTY04bnLkOi9MmCUXOPPOKrBThCPUkBTkN6yhSUhuz3jHkEiMogNR%2FaRrOLh74HZ6yvar%2Bbtlg3NBaTCZ4S2zEO9X9YSuOKZ8IRCFxERUC5bNyGPU7Jkr0SWNTs9E%2FgV5MzqK7%2BdBu0rAGdpNANErl8UcSw%2Bjo2Qi7WaNePDIZMMrI7PAY1pXo0j6oH%2B5aUVf1w%2BXZaX0DZlvpmhcxoR52cQSDVYUumhKt2jxgHHOu%2FiBKU36CnNHYnCRGIEl%2FZv2%2F6mXxV73uZs%2BDF6WUl47OQLGvviUp7mmLffOthmbPF4rebwrvWwqiFx88Y7Q2Yqv%2FC%2FnFEobonj%2F6iYU162D9qicWijls6qgnjloeOX%2FqMHumjnJpjiV1TPRkxBzc4CvWoMoG11J2KdjTyjbOrey8K%2FP5MK014Gn0uLueNZUCgC63JrsIeVYvXLI0%2BnXUfpMfwUISDfJEqBv8qEwRre5EqOv%2Fd%2BqlqBPt40SoG%2FzPFEW0G%2BOkrv1lCbjggmXF6sugYlepvq9SV%2F8A)
---


