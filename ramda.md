---
path: "/ramda"
date: "2019-12-29"
title: "Ramda"
tags: ["ramda", "functional programming", "javascript", "js"]
---

# Ramda
## Ramda vs. Lodash and Underscore
* lodash 和 underscore 歸類於實用函式庫，內含許多ES6的函式方便開發者使用，不過隨著ES6普及，lodash和underscore的優勢不如以往強大，很多函式可以直接用原生javascript method取代，如: map、filter、reduce

* Ramda vs. (Lodash & Underscore)
    | Ramda | Lodash/Underscroe |
    | --- | --- |
    |函式柯里化並且將data放置於最後，讓構成更簡單 | 沒有柯里化或把data放置於最後，除了lodash/FP

## FP (Functional Programming) 的概念
1. 強調純函式(pure function)
2. 每件事都是可以柯里化(curried)的
3. 包含並鼓勵 pipe和compose
4. 函式將data放在最後一個參數位置

### Pure Function概念
1. Simple input, Simple output - 使程式碼容易預測與測試
    比較以下兩個函式。可以看出上面的函式收編了x和y，而函式內做的工作就是簡單地把x和y相加；下方的也是加總，但其中ｘ為shared state，是由取得函式外部的變數，每次相加後x的值都會變化，導致這個函式成為不可預測的函式。
    ```javascript
        const add = (x, y) => x + y;

        add(2 + 4);
    ```
    ```javascript
        let x = 2
        const add = (y) => {
            x += y;
        };

        add(4);
    ```
2. No Side-Effects - 沒有副作用
    三個方式避免side-effects
    * 讓input獨立
    * 不要call HTTP 或寫入硬碟
    * 含義清楚的 - 函式本身容易被替代並且不影響整體功能行為

    測試check-list：
    1. 變異input
    2. console.log
    3. HTTP calls (像是ajax或fetch)
    4. 改變filesystem
    5. 取得 the DOM

    範例程式碼：
    ```javascript
    const impureAssoc = (key, value, object) => {
        object[key] = value;
    };

    const person = { name: 'Bobo' };
    const result = impureAssoc('shoeSize', 400, person);

    console.log({ person, result });
    ```
    我們可以發現person照理來說是不可變得，但因為經由impureAssoc的洗禮，把object傳入function內，每執行一次函式就更動一次person內容。
    調整方式如下：
    ```javascript
    const pureAssoc = (key, value, object) => ({
        ...object,
        [key]: value
    });

    const person = { name: 'Bobo' };
    const result = pureAssoc('shoeSize', 400, person);

    console.log({ person, result });
    ```

小結：
* pure function免於side-effects
* side-effects包含： 改變input、http calls、writing to disk和printing to screen
* 我們可以透過複製inputs來避免資料變異，大方向就是保留原始資料
* spreads是最簡單的方式複製array或object

## High-Order Functions
在javascript函式是第一類公民，即函式可以當作參數傳入，也可以當作變數儲存，而這個特性也讓function可以運作於High-order functions