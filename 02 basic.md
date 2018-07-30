# 2.1 變數
* 每個物件(object)都具備身份、型別和值
    * 身份(id) : 如同身分證，不可改。可透過 `id()` 查詢
    * 型別(type) : 物件的資料型態。可透過 `type()` 查詢
    * 值(value) : 物件存放的資料，視情況(\?)決定可變/不可變
* 不同 type 的物件會佔用不同的空間
* Python 採用 `物件參照(Object Reference)`，異於部分語言的變數參照
* Python 採用 `動態型別(Dynamic Typing)`，因此不需手動指定，直譯器會自動判斷

* `age` 變數指向數值 `25`，因此有相同的 ID：
```py
>>> age = 25
>>> id(age)
140479143357400
>>> id(25)
140479143357400
```

### 垃圾回收機制(Garbage Collection, gc)
* 當 b 的值從 10 變為 20 時，值 10 已無任何物件參照，因此成為垃圾回收機制回收的對象
```py
>>> b = 10
>>> b = 20
```

### 置換變數(Swap)
傳統方法（需要使用一個暫存變數）：
```py
>>> x = 5; y = 10
>>> temp = x # 需使用暫存變數
>>> x = y
>>> y = temp
>>> print(x, y)
(10, 5)
```

便捷方法：
```py
>>> x, y = 5, 10
>>> x, y = y, x # 關鍵
>>> print(x, y)
(10, 5)
```

### eval() : 重新運算參數得出的結果
* 參數須為字串型態
```py
>>> x, y = 5, 10
>>> eval("x + y")
15
>>> eval(x+y) # 應使用字串型態
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: eval() arg 1 must be a string or code object
```

# 2.2 內建型別(Built-in Types)
* 物件
	* 類別(class)：物件藍圖
	* 物件(object)：將類別實體化

### 2.2.1 常見的內建型別
1. 數值(Numeric) : Int, float, complex（複數，如 `3+2j` ）
	* 註：Boolean 為 Int 的子類別
2. 序列(Sequence) : str, list, tuple
3. 迭代(Iterator) : 提供容器，使用 for 迴圈做迭代操作
4. 集合(Set) : set, frozenset
5. 映射(Mapping) : dict
```py
>>> a = 15
>>> type(a) # 能透過 type(object) 查看物件的型別
<type 'int'>
```

# 2.3 數值型別
### 2.3.1 int
* 能透過 `bin(int)`, `oct(int)`, `hex(int)` 從十進位轉換成指定的進位（以字串表示）
```py
>>> result = 16
>>> bin(result)
'0b10000'
>>> oct(result)
'0o20'
>>> hex(result)
'0x10'
```

* 透過 `int(s, base)` 指定從 base 進位轉換成十進位
	* s 一定要是字串
	* 參數 base 可以省略（下圖為方便理解而保留）
```py
>>> int('11', base = 16) # 將十六進位的 11 轉換成十進位
17
>>> int('0x11', base = 0) # 若 base 為 0，則按照字面(0x11)轉換成十進位
17
>>> int('11', base = 13) # base 沒有限制要 2, 8 or 16
14
```

#### 布林(bool)
* 註：隸屬數值(Numeric) -> 整數(Int) -> **布林(Boolean)**
* True, False 首字為大寫
```py
>>> ownMoney = False
>>> isPoor = True
```

* 可透過 `bool()` 將數字轉換為布林值
```py
>>> A1 = 0
>>> type(A1)
<type 'int'>
>>> type(bool(A1)) # 將 int 轉換成 bool
<type 'bool'>
```

* 雖也能採用 1, 0 分別代表 True, False，但不建議（易混淆）
* True = 1; False = 0，其他值不屬於 True 或 False
```py
>>> True == 1
True
>>> False == 0
True
>>> True == 3.14
False
>>> False == 3.14
False
```

### 2.3.2 float
* 浮點數除了帶有小數形式，也能使用科學記號，以指數表示：
```py
>>> 8.9e-4
0.00089
```

* 有三個特殊的浮點數：`nan`, `Infinity`, `-inf`
	* 注意：Infinity 的首字大寫
```py
>>> float('nan') # 非數字，not a number
nan
>>> float('Infinity') # 正無窮大
inf
>>> float('-inf') # 負無窮大
-inf
```

* 檔案 CH0232A.py
	* `isnan()`：判斷是否為 nan
	* `isinf()`：判斷是否為 inf 或 -inf
	* 以上兩個方法皆在 math 模組內，因此需先匯入
```py
import math
a = 1E309
print('a = 1E309, 輸出', a)
print('為NaN?', math.isnan(float(a/a)))
b = -1E309
print('b = -1E309, 輸出', b)
print('為Inf?', math.isinf(float(-1E309)))
```
輸出結果：
```bash
a = 1E309, 輸出 inf
為NaN? True
b = -1E309, 輸出 -inf
為Inf? True
```

#### float 類別提供的方法

方法 | 說明 | 備註
-|-|-
fromhex(s) | 將 16 進位的浮點數轉換為 10 進位 | 類別方法；s代表string
hex() | 回傳 16 進位的浮點數，以字串型別 | 物件方法
is_integer() | 判斷是否為整數（沒有小數*） | 類別方法
```py
>>> num = 71.235
>>> num16 = num.hex() # 以字串回傳 num 的 16 進位
>>> print(num16)
0x1.1cf0a3d70a3d7p+6
>>> type(num16) # num16 為字串
<type 'str'>
>>> float.fromhex(num16) # 以數字回傳 num16 的 10 進位
71.235
>>>
>>> float.is_integer(14.00) # 小數部分皆為 0 也算 Int
True
>>> float.is_integer(11.28)
False
```

#### 函式(function) vs. 方法(method)
* 函式泛稱內建函式(BIF)
* 方法(method)分類別方法、物件方法
	* 類別方法：由類別提供，`className.method()`
	* 物件方法：由物件提供，`objectName.method()`

### 2.3.3 complex
* 由實數(real)和虛數(imaginary)
	* 註：為實數而非整數，因此也能做這樣的宣告
```py
>>> complex('3.25+6j')
(3.25+6j)
```
* 虛數的部分得加上 j 或 J（其它字元不行）
```py
>>> total = 5 + 6j
>>> total.real, total. imag # real, imag 能分別取得實數、虛數部分
(5.0, 6.0)
>>> total.conjugate() # conjugate() "方法"能取得共軛複數
(5-6j) # 註：共軛負數將原本虛數變號
>>> type(total)
<type 'complex'>
```

* 複數以字串型態表示時，中間不能加空白
```py
>>> complex(12-5j, 5+3j) # 註 1
(9+0j)
>>> complex('12+5j')
(12+5j)
>>> complex('12 + 5j') # 中間加空白會發生錯誤
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: complex() arg is a malformed string
```
* 註 1：`complex(12-5j, 5+3j)`
```
complex(12-5j, 5+3j)
= 12-5j + j(5+3j)
= 12-5j + 5j+3jj
= 12-5j+5j + 3jj # jj = -1
= 12+0j + -3
= 9+0j
```

### 2.3.4 decimal
* decimal 型別較 float 更精準
* 註：須先匯入 `decimal` 模組
```py
>>> print(10/3)
3.3333333333333335
>>> print(decimal.Decimal(10/3)) # 尚未匯入 decimal 模組
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'decimal' is not defined
>>> import decimal
>>> print(decimal.Decimal(10/3))
3.333333333333333481363069950020872056484222412109375
```

* decimal 具有「有效位數」
```py
>>> from decimal import *
>>> Decimal(0.23)
Decimal('0.2300000000000000099920072216264088638126850128173828125')
>>> Decimal('0.235') # 以字串表示數字
Decimal('0.235')
>>> numA = Decimal('0.235'); numB = Decimal('3.458')
>>> numA + numB
Decimal('3.693')
>>> numA * numB
Decimal('0.812630')
```

#### decimal 算術運算環境
```py
>>> getcontext() # 取得算數環境的設定值
Context(prec=28, rounding=ROUND_HALF_EVEN, Emin=-999999, Emax=999999, capitals=1, clamp=0, flags=[FloatOperation], traps=[InvalidOperation, DivisionByZero, Overflow])
>>> getcontext().prec # 取得精確度
28
>>> getcontext().prec = 8 # 重設精確度為 8 位
>>> Decimal(2)/Decimal(3) # 可看到精確度為 8 位
Decimal('0.66666667')
>>> Decimal(16)/Decimal(3) # 精確度包含整數與小數
Decimal('5.3333333')
>>> Decimal(128)/Decimal(3)
Decimal('42.666667')
```

#### 捨入(Rounding)規則
	* `ROUNDING_CEILING`：朝著無窮大的方向
	* `ROUND_DOWN`：無條件捨去
	* `ROUND_FLOOR`：朝著負無窮大的方向
	* 四捨六入
		* `ROUND_HALF_DOWN`：五朝著接近零的方向
		* `ROUND_HALF_EVEN`：五朝著最接近偶數的方向
		* `ROUND_HALF_UP`：五朝著遠離零的方向
	* `ROUND_UP`：無條件進位
	* `ROUND_05UP`：捨去最後位數後，若為 0 或 5 則進位，其他捨位
```py
>>> getcontext().rounding
'ROUND_HALF_EVEN' # 預設的捨入規則
>>> getcontext().prec = 4
>>> Decimal('0.123') + Decimal('1.0005')
Decimal('1.124')
>>> Decimal('0.122') + Decimal('1.0005')
Decimal('1.122')
```

* `ROUND_05UP`：捨去最後位數後，若為 0 或 5 則進位，其他捨位
```py
>>> Decimal('0.125') + Decimal('1.0001') # 1.1251
Decimal('1.126') # 捨去最後位數(1)後，因左邊是 5 而進位
>>> Decimal('0.120') + Decimal('1.0005') # 1.1205
Decimal('1.121') # 捨去最後位數(5)後，因左邊是 0 而進位
>>> Decimal('0.121') + Decimal('1.0005') # 1.1215
Decimal('1.121') # 捨去最後位數(5)後，因左邊是 1 而不進位
```

* 使用浮點數時，還可以用 `round()` BIF 將小數四捨五入
> `round(number[, ndigits])`
```py
>>> round(4578.6447) # 沒設第二個參數，因此以整數輸出
4579
>>> round(4578.6447, 0)
4579.0
>>> round(4578.6447, 1)
4578.6
>>> round(4578.6447, 2) # 保留小數兩位
4578.64
```

### 2.3.5 番外－分數
* 分數並不屬於數值型別
* 要做分數計算時，須先匯入 `fractions` 模組（注意：有s）
* 使用 `Fraction()` 方法會自動約分
* 參數不能浮點數和整數混合使用，否則會產生「Type Error」錯誤
```py
>>> from fractions import Fraction # 只匯入 Fraction 方法
>>> Fraction(12, 18) 
Fraction(2, 3) # 會自動約分
>>> Fraction('1.623')
Fraction(1623, 1000)
>>> Fraction(Fraction(2, 5), Fraction(6, 5)) # Fraction 的參數也能使用 Fraction
Fraction(1, 3)
>>> Fraction(1.3, 4)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/fractions.py", line 174, in __new__
    raise TypeError("both arguments should be "
TypeError: both arguments should be Rational instances
```

* `numerator` 屬性為分子；`denominator` 屬性為分母
```py
>>> from fractions import Fraction
>>> num = Fraction(3, 4)
>>> num.numerator # 分子
3
>>> num.denominator # 分母
4
```

# 2.4 使用運算式
### 2.4.1 算數運算子
運算子|說明|運算|結果
-|-|-|-
`/`|把運算元相除|total = 15 / 7|total = 2.14
`//`|取得整除數|total = 15 // 4|total = 3
`**`|指數運算子|total = 15 ** 2|total = 255

* 要取得整除的商數，除了可使用 `//` 運算子，也可使用 `int()` 函式做轉換
```py
>>> 17/4
4.25
>>> 17//4 # 方法 1 : // 運算子
4
>>> int(17/4) # 方法 2 : int() 函式
4
```

* 除了指數運算子，也可使用 math 模組內的 `pow(x, y)` 方法
* 餘數也可改用 math 模組內的 `fmod(x, y)` 方法
```py
>>> from math import *
>>> pow(15, 2) # 求指數
225.0
>>> fmod(17, 4) # 求餘數
1.0
```

* 透過 BIF 的 `divmod()` ，回傳商數和餘數的 Tuple
```py
>>> divmod(17, 4)
(4, 1) # 第一個為商數，第二個為餘數
```

#### math 模組的常用屬性、方法
* 使用前須先匯入 math 模組
* 平方根除了採用 `sqrt` 方法外，也能改採 0.5(1/2) 次方的方式
* 進位、捨去部分可把數字想像成樓層，-8.9 層的地板為 -9
```py
from math import *
sqrt(144) # 12.0
144 ** 0.5 # 12.0

pow(3, 3) # 27.0
pow(27, 1.0/3) # 3.0
pow(4, 4) # 256.0
pow(256, 1.0/4) # 4.0

# 進位、捨去
ceil(4.2) # 5
ceil(-4.2) # -4
floor(9.7) # 9
floor(-8.9) # -9
hypot(3, 9) # 等同於 sqrt(3^2 + 9^2)
```

### 2.4.2 指派運算子
* 可把運算後的結果指派給變數
* 假設 total = 10

運算子|運算|指派運算|結果
-|-|-|-
`//`|total = total // 3 |total //= 3|total = 3
`**`|total = total ** 2 |total **= 2|total = 100

* 使用指派運算子時，須先賦予變數的值
```py
>>> a += 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'a' is not defined
>>> a = 5
>>> a += 5
>>> a
10
```

### 2.4.3 比較運算子
* 與 JS 用法類似，但沒有 `===`（嚴格相等）用法
### 2.4.4 邏輯運算子
* 與 JS 用法類似，但符號改為文字
	* `&&` -> `and`
	* `||` -> `or`
	* `!` -> `not`
* `and`, `or` 運算子在做邏輯運算子會採用 `快捷(Short-circuit)運算`
	* 當運算值不是布林值時，會直接回傳運算元
	* `and` 運算子：若第一個運算回傳 True，才會繼續第二個運算的判斷；第一個運算元回傳 False 就不會再繼續
	* `or` 運算子：若第一個運算回傳 False，才會繼續第二個運算的判斷；第一個運算元回傳 True 就不會再繼續
```py
>>> three = 3; eight = 8
>>> three and eight
8
>>> eight and three
3
>>> three or eight
3
>>> eight or three
8
```

### 2.4.5 位元運算子
* 位元(Bitwise)運算以二進位為運算式
	* Xor 的符號為 `^`
	* Not 的符號為 `~`（並非`!`）
* Xor 為兩個參數相等時輸出 False(0)
* Not 的結果採 2 的補數［註：從右邊數過來的第一個 1 不變，其餘左邊的數都相反(0->1;1->0)］
```py
x = 6; y = 13
bin(x); bin(y) # 將 x, y 轉為二進位
# bin(x) = 0b0110
# bin(y) = 0b1101
print(x & y) # 運算結果為 0b0100，會輸出十進位的 4
print(x | y) # 0b1111，15
print(x ^ y) # 0b1011，11
print(~x) # 0b1001，採 2 的補數，得 -7，即 -(x+1)
```

* `~6` 並不等於 -6，而是`-(6+1) = -7`
```py
>>> ~6
-7 # -(6+1)
>>> ~0
-1 # -(0+1)
```

* Python3 也有左移`<<`和右移`>>`運算子
* 左移相當於乘二，右移相當於除二
```py
>>> 2<<1
4
>>> 2>>1
1
```