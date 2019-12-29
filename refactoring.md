---
path: "/refactoring"
date: "2019-09-29"
title: "閱讀筆記-Refactoring"
tags: ["refactoring", "javascript", "js"]
---

# Bad smells in code
* Mysterious Name(神秘的名稱)
* Duplicated Code(重複的程式碼)
* Long Function(冗長的函式)
* Long Parameter List(冗長的參數列)
* Global Data(全域資料)
* Mutable Data(可變資料) - 減少變數作用域
* Divergent Change(發散式修改) - 違反 Single Responsibility Principle ，導致非常檔案容易被修改，例如更改金融處理邏輯和更改資料庫系統都要動到同一個類別的函式。
* Shotgun Surgery(霰彈式修改) - 每次修改時，都要在許多不同的類別進行小規模的編輯
* Feature Envy(依戀情節) - “永遠將一起變化的東西放在一起”
* Data Clumps(資料泥團) - 將成群結隊出現的資料泥團轉換成物件處理
* Primitive Obsession(基本型態偏執) - 使用有意義的型態，而非基本資料型態
* Repeated Switches(重複的切換邏輯) - 重複的邏輯判斷應該使用多型(Polymorphism)
* Loop(迴圈) - Replace Loop with Pipeline (use pipeline operation)
* Lazy Element(冗員元素) - 名字看起來跟內文程式碼一樣的類別或函式
* Speculative Generality(畫大餅) -
* Temporary Field(暫時欄位) -
* Message Chains(過度耦合的訊息鏈)
* Middle Man(中間人) -
* Insider Trading(內幕交易) -
* Large Class(龐大的類別) -
* Alternative Classes with Difference Interfaces(異曲同工的類別) -
* Data Class(呆板的資料類別)-
* Refused Bequest(被拒絕的遺產) -
* Comments(過多的註解) -

# Building Tests
## 自檢程式的價值
 - debug的痛

> 確保所有的測試都是完全自動化的，而且它們會自己檢查結果。
> 測試程式是強大的bug偵測器，減少debug的時間
> 想一下可能出錯的邊界條件，並且集中測試那裡

* 最有效的測試編寫時機之一，就是在開始編程的時候。當需要加入新功能時，就會先編寫測試，即Test-Driven Development(TDD, 測試驅動開發)
* 把測試焦點放在最擔心出錯的領域，不要寫無用的測試

用chai選擇使用 `assert` or `expect` => 我也比較喜歡assert

# 第一組重構
### Extract Function
動機：
* 如果必須費心查看一段程式碼才能了解它究竟在做什麼，就該把函示提取出來，並以目的為函式命名
* 長度超過六行的函式就會發散異味
* 小函式必須有好名字才能發揮效果！命名命的好，就是份參考

作法：
* 根據函式的目的為它命名
