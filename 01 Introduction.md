# 1.1 關於 Python
* 動態型別
    * 程式碼執行的時候才會檢查
* 強型態
    * 規範較嚴格，如數字加字串並不合法
* 是腳本語言也是程式語言
    * 腳本語言(Script Language)：又稱描述語言 \?
* 是膠水語言
    * 能把相關功能的程式（可能由不同的語言所寫）黏在一起
* 官方的直譯器：CPython
* pip : 管理第三方函式庫的工具

# 1.2 Python IDE
* IDLE : 內建於 CPython 的 IDE
    * 另外推薦由 JetBrains 所開發的 Pycharm

### 說明模式 `help()`
```py
>>> help()

Welcome to Python 2.7!  This is the online help utility.
... # 略

help> if # 查詢關鍵字代表的意義，只要輸入關鍵字名稱即可
help> input # 查詢 BIF 的說明，只需要函式名稱即可，不用加小括號
help> topics # 也能輸入 topics 查看主題式的說明
help> quit # 輸入 quit 或 Ctrl + c/d 來離開說明模式
```
* 註：內建函式(Built-In Function, BIF)

* 在 `>>>` 模式下，也能輸入 `help(BIFName)` 能查詢
```py
>>> help(round) # 查詢 round（四捨五入到指定的位數）
>>> help(str.split) # 因為是字串型別提供的方法，因此前面需加上 str
>>> help(math.pow) # 查詢不到內容，因為沒有匯入模組
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'math' is not defined
>>> import math
>>> help(math.pow) # 匯入後即能查詢
```

# 1.3 Python 撰寫風格
* 原始程式碼(.py) -> 解譯器(interpreter) -> 位元碼(.pyc) -> 執行程式(PVM)
* Python 虛擬機器(Python Virtual Machine, PVM)

### 變更編碼
* 在每個檔案開頭附上：
```py
-*- coding: encoding -*-
# 註：encoding 代表要使用的編碼
```
* 如要更改為 UTF-8：
```py
-*- coding: utf-8 -*-
```

### 1.3.2 註解
```py
# 單行註解
... """ 多行
...     註解 """
```

### 1.3.3 敘述的分行與合併
* 當敘述太長時，能用 `\` 將敘述拆成多行
```py
isLeapYear = (year % 4 == 0 and year % 100 != 0) or \
(year % 400 == 0)
```

* 例外：敘述中有小、中、大括號時，在括號內分行並不會被當作兩行不同的敘述
```py
isLeapYear = (year % 4 == 0 and
year % 100 != 0) or (year % 400 == 0)
```

* 如果單行敘述很短，可使用 `;` 將分行的敘述合併成一行
```py
a = 10; b = 20; c = 30
```

### 1.3.4 程式的輸入與輸出
* 輸入：`input([prompt])`
    * prompt：提示字串
```py
>>> num = input("請輸入一個數字：")
請輸入一個數字：10
>>> print(num)
10
```
* 輸出：`print(value)`