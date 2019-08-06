== Vim ==
=== Mode ===
* Command(一般指令)
  * 離開
    * ''':w''': 存檔(write)
    * ''':q''': 離開(quit)
    * ''':wq''':存檔&離開
    * ''':q!''':強制離開(!=force)
  * 進入Insert Mode
    * i: insert
    * a: append
    * o: new line
  * 移動游標
    * h/←: 左
    * j/↓: 下
    * k/↑: 上
    * l/→: 右
    * [num] + [h|j|k|l]: 進行多次移動
      * 如： '''3j'''即等於「往下移動3個字元」
    * ctrl + f: Page Down
    * ctrl + b: Page Up
    * + / -: 游標移動到非空白字元的上一列/下一列
    * n<space>: 按下數字後再按下空白鍵，游標會移動到右移的第n個字元
    * 0 / $: 移到這一列的最前面/最後面字元
    * G / gg(1G): 移動到這個檔案的最後一列/第一列
    * n<Enter>: 游標向下移動n列
    * shift+4: 游標移到該列的最後字元
    * shift+6: 游標移到該列的最前面的字元
    * w/e: 向前移動一個word
    * b: 向後移動一個word
  * 搜尋與取代
    * /word: 游標之下尋找[word]字串
    * ?word: 游標之上尋找[word]字串
    * n: 向下搜尋下一個[word]字串
    * :n1,n2s/word1/word2/g: n1&n2為數字。在n1與n2列之間尋找word1字串並取代為word2
    * :1,$s/word1/word2/g: 從第一列到最後一列之間尋找word1字串並取代為word2
    * :1,$s/word1/word2/gc: 同上，c代表confir，在取代前須給使用者確認是否要取代
    * r: 替換一個字元為我所插入的字元
    * R: 取代字元到按Esc離開為止
    * s: 替換一個字元為我所插入的字串
  * 刪除、複製＆貼上
    * x/X: 刪除一個字元，x相當於[del];X相當於[backspace]
    * nx: n為數字，nx即為向後刪除n個字元
    * dd: 刪除一整列，若前面加數字(n)，則為向下刪除n列
    * dw: 刪除一個字(不適用中文)
    * dG: 刪除到最底
    * yy: 複製游標所在的那一列，若前面加上數字(n)，則為向下複製n列
    * p/P: 將以複製的資料貼上。p為貼在游標的下一列；P為貼在游標的上一列
    * u: 復原前一個動作(undo)
    * ctrl+r: 重做上一個動作(redo)
    * .:複製前一個動作
  * 簡單排列功能
    * >>: 向右移一個shiftwidth
    * <<: 向左移一個shiftwidth
      * :set sw? : 查看目前的設定值
      * :set sw=n : 設定shiftwidth為n個字元
* Insert(編輯)
  * 返回Normal Mode
    * ESC / Ctrl+[