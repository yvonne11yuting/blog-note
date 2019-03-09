---
path: "/git"
date: "2018-12-16"
title: "git指令筆記"
tags: ["git"]
---

## git筆記
### git push
* 將commit的內容推上遠端repo
  * -u: 將遠端repo branch設為追蹤目標
  * --delete origin \[branch name\]: 移除遠端branch
  ```bash
  git push [remote] [branch]
  ```

* 遠端repo建立新branch
  ```bash
  git push origin master:[branch name]
  ```
  以上指令等同於
  ```bash
  git checkout -b [branch name]
  git push origin [branch name]
  ```
  ※ 建立完branch別忘了clone

### git clone
複製已存在的remote repo到本地端
```bash
git clone [url]
```

### git pull
把遠端repo修改的內容合併到本地端，等同於fetch + merge
```bash
git pull [remote] [branch]
```
* --rebase: 從遠端repo更新時減少不必要的merge，即：
  1. 把本地repo從上次pull後的變更儲存
  2. 回復至上次pull時的狀態
  3. 套用遠端的變更
  4. 再套用剛剛站存下來的本地變更

### git add (add files to stage)
* \[path\]: 增加檔案或目錄到stage
* -u: 不處理untracked的檔案
* -A / . :不管tracked或是untracked的檔案都加到stage上

### git commit (staged)
提交加到stage的檔案
* -m : 可以直接添加commit message

### git branch
列出目前本地端所有的branch
* -r: 列出remote repo 所有branch
* -d \[branch\]: 移除本地端branch

### git checkout
* \[branch name\]: 切換branch
* \[filename\]: 還原本地端修改的檔案內容

### git merge
合併branch
* --no-ff \[branch name\]: 保留branch合併的記錄，merge後會產生新的commit
  ![image](https://i.stack.imgur.com/FMD5h.png)

> reference: [What is the difference between `git merge` and `git merge --no-ff`?](https://stackoverflow.com/questions/9069061/what-is-the-difference-between-git-merge-and-git-merge-no-ff)

### git rebase
與git merge類似都有合併branch的功能，差異點在於：
* merge: 修改的歷史記錄會維持原狀，但合併後的記錄會變得更複雜
* rebase: 修改內容的歷史記錄會接在要合併的分支後面，合併後的記錄會比較清楚，但會比使用merge更容易發生衝突
  * git rebase -i \[commit hash\]: 精簡commit記錄，commit hash指定要合併的最早節點，合併HEAD到指定的commit節點，接著進入編輯模式
    * pick: 直接使用這個commit，不做任何調整
    * reword: 使用這個commit，只調整commit message
    * squash: 使用這個commit並融入前一個commit中，合併兩個commit message（可以修改)
    * fixup: 使用這個commit並融入前一個commit中，合併兩個commit message（不能修改)
    * drop: 直接移除這個commit

> reference: [\[Git\] Rebase - 使用 Interactive 模式來精簡 commit 紀錄](https://dotblogs.com.tw/wasichris/2016/05/04/re)

### git status
顯示目前修改的檔案清單

### git diff
顯示修改的檔案差異
* --staged/--cached: 已經上stage的檔案列出差異

### git reset
* --mixed: 還原已經add至stage的檔案，仍保存修改 (default)
* --hard: 還原已經add至stage的檔案，並捨棄之前的修改

### git revert
```bash
git revert [commit hash]
```
建立一個新的commit來還原已經commit的修改(尚未執行git push)

### git mv
重新命名或搬移檔案
```bash
git mv [origin file] [rename file/destination]
```

### git log
觀看commit的log記錄
* \[remote/branch\]: 查看特定的branch log
* --oneline: 只顯示hash和log message
* --author="username": 顯示特定開發者的commit log

### tig
需另外安裝，maxOS安裝tig透過brew，指令如下：
```bash
brew install tig
```
可以代替git log, git diff 以及 git blame等指令直接瀏覽commit記錄
* q: 離開
* j/k: 上下移動
* return/enter: 查看commit的詳細內容
* t: 對選中的commit按**t**進入tree view，可以查看當時repo的內容
* C: tig後若有接branch名稱，直接在該commit上按大寫**C**可以cherry-pick回目前的branch

### git stash
暫存修改不commit
* list: 列出暫存的項目
* apply: 使用暫存的修改但不移除stash，可指定stash使用，如：```git stash apply stash@{0}```
* pop: 使用暫存的stash並從stash移除
* drop: 移除stash上的項目，並可指定stash，如：```git stash drop stash@{0}```
* stash show -p stash@{0}: 查看已儲存的stash@{0}和目前本地repo的diff
  * ```git stash show -p stash@{0}``` 等同於 ```git show stash@{0}```

### git apply
使用補丁(patch)。前置作業：
* 產生補丁: 透過```git diff > xxx.patch```產生補丁檔
* 使用補丁: ```git apply xxx.patch```

### git blame
* \[file name\]: 查看每行修改記錄
* -L \[start line\],\[end line\]: 指定行數
  * 範例：```git blame -L 5,10 index.js```

### git cherry-pick
* [commit hash...]: 只選擇特定branch的commit合併，多筆以空格區隔
* --no-commit: 合併過來的commit先不要commit

> reference: [【狀況題】如果你只想要某個分支的某幾個 Commit？](https://gitbook.tw/chapters/faq/cherry-pick.html)

### git reflog
查看自己過去的git操作記錄

### git tag
指向某個commit的指標
* \[tag name\] \[commit hash\]: 建立沒有附註的tag
* \[tag name\] \[commit hash\] -a -m '\[messages\]': 建立有附註的tag<br>
※ 如果沒有特別加commit hash，tag會下在當前的commit上
* -d \[tag name\]: 移除tag
* git show \[tag name\]: 顯示特定tag的commit
<br>
**用途：**
* 可使用git reset --hard \[tag name\] 和 git checkout \[tag name\]結合使用，將專案回復至先前commit的版本
> reference: [Git配合Tag的代码回滚](http://www.cnblogs.com/zqzjs/p/6812214.html)


