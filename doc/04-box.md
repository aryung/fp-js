# 楔子
如果要使用所謂的 chain style 的 coding style，那可能就開始要來設定一些「規則」讓程式的方便使用和好讀，今天就來練習建立這種規則吧。

# Functor(chain style)
如果要使用這種的模式，入口的思考點就是使用一個 Box，而這個 Box 可以有一個指令「方法」，丟入一個「函數」來計算結果，就像 map 一樣，就是把一個「函數」丟入一個「很多值」的資料。

如果用「函數式程式」的說法就是:有一個 Functor 可以 map over。

指的就是一個 Box 可以使用 map 的方式來丟一個函數計算。

那像 array 算不算一個 Box/Functor ?

```
// array 是 box 嗎? yes
let a = [100]
a.map(addOne) // [101]

// 如果是一個 value 是一個 box 嗎?
let b = 10
b.map(addOne) // Error: 10 不是一個有 map 方法

// 如何建位一個 box ? 自製一個有 map 的 box
let box = x => ({map: f => f(x), x})

function addOne(x) {return x + 1}
```

# Compose & Pipe

to be continue

