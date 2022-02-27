# 楔子
在練習寫程式的時候，如果有一些規則可以幫助讀 code 或寫 code 就比較容易形成共識。
今天來聊聊數學的感覺 & 怎把那種 coding style 和數學的感覺結合在一起。

# 函數
小時候應該學過什叫函數，就是 y = f(x) 和 f(x) = x + 1 這種的概念，再衍生來看就是，然後把 `y = f(x)` 的 `f(x)= x + 1` 套入 y = f(x)，這個意思就是代表幾個意思
- 函數是可以當做「參數」丟來丟去的:上面的 f(x) 就是一個參數的概念(y = f(x) 的概念)
- 不同變數之間的關係式可以是「函數」和「參數」的組合結果

如果在 javascript 的環境下，可以試試看下面的結果

```
function g(x) {return x}
g // f 代表 g 是一個 function
```

那如果在程式的呈現就有點像

```
let y1 = f => g => x => f(g(x))
let y2 = f => g => f(g)
```

有沒有覺的很像數學的感覺? 再感覺一下，那上面的 y1 和 y2 二個的意思是一致的嗎?

答案是一致的，也很像數學式的消除法 y * X = f * g * X 把最後的 X 消掉的概念

如果要化成白話文的意思是，f(g) 可以是一個函數的組合(f 和 g 都是函數，彼此都可以參數拋來拋去)

但有一個有趣的問題是，那如果函數是 f(x,y) 參睥 x 是一個函數，y 是一個數值，那這樣消來消去會不會有問題?

為了避刷閱讀上的困擾或計算上的單純化，我們都儘量把函使用「一個」參數最好了，大家才不會去想參數的位置對不對(但其實也有 combinator 一些函數來處理這個議題，之後可以再做一集做分享)

# Data = Function ( arguements )

如果了解以上的內容，還記的上次提到的 coding style 嗎?
```
let box1 = x => f => g => f(g(x))
box1(1)(multi3)(add1) // 4
box1(5)(multi3)(add1) // 6

let box2 = f => g => x => f(g(x))
box2(multi3)(add1)(1) // 4
box2(multi3)(add1)(5) // 6
```
上面的 box1 和 box2 的差別在哪? 就差在「數值」放在前面或後面而以，但其實可以想像的是

結果(final) = 函數組合(function) + 數值(value) 

只是值要放一開始或最後面而以。

# 函數式

講了這麼多，來看看有哪些小工具來幫助我們寫程式。

常用的就其實有
- [Ramda](https://ramdajs.com)
- [loadash](https://lodash.com)
- [sanctury-js](https://github.com/sanctuary-js/sanctuary)

Ramda 是把資料放在最後一個，loadash 是把資料當第一個，有興趣的可以去來玩玩。
我們來看一下 Ramda 的一些示範 code。

```
// add 為二個數字的函數
// Number → Number → Number
R.add(2, 3);       //=>  5
R.add(7)(10);      //=> 17

// map 的參數為「函數」+「array」
const double = x => x * 2 // 定義一個函數
R.map(double, [1, 2, 3]) //=> [2, 4, 6]
R.map(double, {x: 1, y: 2, z: 3}) //=> {x: 2, y: 4, z: 6}

// filter 的參數為「函數」+「array」
const isEven = n => n % 2 === 0;
R.filter(isEven, [1, 2, 3, 4]); //=> [2, 4]
R.filter(isEven, {a: 1, b: 2, c: 3, d: 4}); //=> {b: 2, d: 4}

// reduce 的參數為「函數」+「起始值」+「array」
R.reduce(R.subtract, 0, [1, 2, 3, 4])
```