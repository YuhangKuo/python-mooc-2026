# Python Programming MOOC 2026 — Part 1 筆記

> 目標：記住 Python 基礎語法與基本程式思考，不追求把所有內容背起來。

---

## 1. `print()` 輸出

最基本的輸出：

```python
print("Hello world!")
```

可以一次輸出多個值：

```python
name = "Alice"
age = 20

print(name, age)
```

輸出：

```text
Alice 20
```

### f-string

需要把變數放進文字時：

```python
name = "Alice"
age = 20

print(f"My name is {name} and I am {age} years old.")
```

常用於格式化輸出。

---

# 2. `input()` 輸入

```python
name = input("What is your name? ")
```

使用者輸入的內容預設是 **字串 `str`**。

因此：

```python
age = input("Age: ")
```

`age` 是字串，不是數字。

如果需要整數：

```python
age = int(input("Age: "))
```

如果需要小數：

```python
price = float(input("Price: "))
```

常見轉換：

```python
int("10")       # 10
float("10.5")   # 10.5
str(10)         # "10"
```

---

# 3. 變數 Variables

建立變數：

```python
name = "Alice"
age = 20
```

`=` 是**賦值（assignment）**。

不是數學上的「等於」。

```python
x = 10
x = x + 5
```

最後：

```text
x = 15
```

---

## 變數名稱

使用有意義的名稱：

```python
hourly_wage
hours_worked
day_of_week
temperature
points
```

不要全部使用：

```python
a
b
c
x
y
z
```

除非這些名稱本身就是問題的一部分，例如數學公式：

```python
a
b
c
```

### 英文不好時的快速方法

不要追求「漂亮英文」。

先問：

> 這個變數代表什麼？

例如：

| 意思 | 可以用 |
|---|---|
| 工資 | `wage` |
| 時薪 | `hourly_wage` |
| 工作時數 | `hours_worked` |
| 星期幾 | `day_of_week` |
| 溫度 | `temperature` |
| 點數 | `points` |
| 原始點數 | `original_points` |
| 倍率 | `factor` |
| 第一個根 | `root1` |
| 第二個根 | `root2` |

**簡單、清楚就夠了。**

---

# 4. 基本運算

```python
+
-
*
/
```

例如：

```python
a = 10
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a / b)
```

---

## 次方

Python 的次方是：

```python
**
```

例如：

```python
2 ** 3
```

結果：

```text
8
```

### 注意

```python
2 ^ 3
```

**不是次方。**

`^` 在 Python 是 XOR 位元運算。

---

# 5. 複合賦值運算子

```python
x += 1
```

等同：

```python
x = x + 1
```

同理：

```python
x -= 1
```

等同：

```python
x = x - 1
```

```python
x *= 2
```

等同：

```python
x = x * 2
```

```python
x /= 2
```

等同：

```python
x = x / 2
```

### 例子

```python
points = 100

points *= 1.1
```

等同：

```python
points = points * 1.1
```

結果：

```text
110.0
```

---

# 6. `if` 條件判斷

基本結構：

```python
if condition:
    # 要執行的程式
```

例如：

```python
temperature = 15

if temperature < 20:
    print("It is cold")
```

### Python 非常重視縮排

正確：

```python
if temperature < 20:
    print("It is cold")
```

錯誤：

```python
if temperature < 20:
print("It is cold")
```

通常使用 **4 個空白**縮排。

---

# 7. 比較運算子

```python
==    等於
!=    不等於
<     小於
>     大於
<=    小於等於
>=    大於等於
```

注意：

```python
=
```

是賦值。

```python
==
```

才是比較「是否相等」。

例如：

```python
age = 20

if age == 20:
    print("You are 20")
```

---

# 8. 多個 `if`

不同的 `if` 可以全部執行。

例如：

```python
temperature = 5

if temperature <= 20:
    print("Wear a jumper")

if temperature <= 10:
    print("Take a jacket")

if temperature <= 5:
    print("Wear a warm coat")
```

`temperature = 5` 時，三個條件都成立，因此三個都會執行。

---

## `if` 與 `elif`

如果條件是互斥的，可以使用：

```python
if points < 100:
    ...
elif points >= 100:
    ...
```

但如果每個條件都可能同時成立，就不能隨便改成 `elif`。

### 例子

天氣：

```python
if temperature <= 20:
    ...

if temperature <= 10:
    ...

if temperature <= 5:
    ...
```

5 度時，三個建議都應該出現。

---

# 9. `else`

當 `if` 條件不成立時執行：

```python
if temperature < 20:
    print("Cold")
else:
    print("Warm")
```

常見結構：

```python
if condition:
    ...
else:
    ...
```

---

# 10. 字串 String

字串可以用：

```python
"Hello"
```

或：

```python
'Hello'
```

例如：

```python
day_of_week = input("Day of the week: ")

if day_of_week == "Sunday":
    print("Weekend")
```

### 字串比較

```python
rain = input("Will it rain (yes/no): ")

if rain == "yes":
    print("Take an umbrella")
```

---

# 11. `int`、`float`、`str`

常見資料型態：

```text
int     整數
float   浮點數／小數
str     字串
```

例子：

```python
age = 20          # int
price = 19.99     # float
name = "Alice"    # str
```

---

# 12. `math` 模組

使用平方根：

```python
from math import sqrt
```

之後：

```python
sqrt(9)
```

結果：

```text
3.0
```

平方根也可以用次方：

```python
9 ** 0.5
```

---

# 13. 二次公式

二次方程式：

```text
ax² + bx + c = 0
```

二次公式：

```text
x = (-b ± √(b² - 4ac)) / (2a)
```

其中：

```text
discriminant = b² - 4ac
```

中文叫：

> **判別式**

Python：

```python
discriminant = b**2 - 4*a*c
```

---

## 判別式的意義

```text
discriminant > 0
→ 兩個不同的實數根

discriminant == 0
→ 一個實數根（兩根相同）

discriminant < 0
→ 沒有實數根
```

---

## 二次公式 Python 寫法

```python
from math import sqrt

a = int(input("Value of a: "))
b = int(input("Value of b: "))
c = int(input("Value of c: "))

discriminant = b**2 - (4 * a * c)

root1 = (-b + sqrt(discriminant)) / (2 * a)
root2 = (-b - sqrt(discriminant)) / (2 * a)

print(f"The roots are {root1} and {root2}")
```

### 重要單字

```text
root
→ 根／解

root1
→ 第一個根

root2
→ 第二個根

discriminant
→ 判別式

factor
→ 因素／因子；在某些計算情境可理解為倍率
```

---

# 14. `±` 不等於「正根／負根」

二次公式：

```text
-b ± √(...)
```

`+` 和 `-` 會產生兩個解。

但：

```text
+ → 不一定是正根
- → 不一定是負根
```

「正根」是指**數值大於 0 的根**。

因此程式通常使用：

```python
root1
root2
```

而不是：

```python
positive_root
negative_root
```

---

# 15. 變數不要過早修改

這是 Part 1 很值得記住的程式思考。

例如：

```python
points = 99

if points < 100:
    points *= 1.1
```

修改後：

```text
points = 108.9
```

如果後面還要判斷：

```python
if points >= 100:
```

就可能造成問題。

---

## 更好的方法：先決定，再修改

```python
if points < 100:
    factor = 1.1
    print("Your bonus is 10 %")

if points >= 100:
    factor = 1.15
    print("Your bonus is 15 %")

points *= factor
```

這裡：

```python
factor = 1.1
```

代表：

> 先決定要使用 1.1 倍。

最後才真正修改：

```python
points *= factor
```

### 重要觀念

> **不要不必要地太早修改原始資料。**

有時候可以先把「要怎麼處理」存進另一個變數。

---

# 16. 還原運算

如果：

```python
price *= 1.1
```

想用相反運算還原：

```python
price /= 1.1
```

因為：

```text
原值 × 1.1 ÷ 1.1 = 原值
```

但如果程式邏輯本身不需要修改原值，通常更好的方法是：

```python
original_price = price
```

或像前面的例子，**先保存 factor，最後才修改**。

---

# 17. 數學公式翻譯成 Python

不要看到公式就整行硬打。

例如：

```text
x = (-b ± √(b² - 4ac)) / (2a)
```

可以拆成：

```text
1. b² - 4ac
2. sqrt(discriminant)
3. -b + sqrt(...)
4. -b - sqrt(...)
5. 除以 2a
```

Python：

```python
discriminant = b**2 - 4*a*c

root1 = (-b + sqrt(discriminant)) / (2*a)
root2 = (-b - sqrt(discriminant)) / (2*a)
```

### 原則

> **先把問題拆小，再把每一部分翻成 Python。**

---

# 18. 常見錯誤整理

## `=` 和 `==` 搞混

錯：

```python
if age = 20:
```

對：

```python
if age == 20:
```

---

## `^` 當成次方

錯：

```python
b ^ 2
```

對：

```python
b ** 2
```

---

## 忘記 `input()` 預設是字串

錯：

```python
age = input("Age: ")
if age > 18:
    ...
```

對：

```python
age = int(input("Age: "))
```

---

## 忘記縮排

錯：

```python
if age >= 18:
print("Adult")
```

對：

```python
if age >= 18:
    print("Adult")
```

---

## 不必要地使用 `elif`

如果多個條件可以同時成立：

```python
if temperature <= 20:
    ...

if temperature <= 10:
    ...

if temperature <= 5:
    ...
```

不要因為看到多個條件就自動改成 `elif`。

---

# 19. Part 1 的核心思考

Part 1 不只是記語法。

真正要開始建立的是：

### ① 變數代表什麼？

```python
temperature
points
factor
root1
```

---

### ② 什麼時候修改變數？

問自己：

> 「現在真的需要改它嗎？」

---

### ③ 條件判斷的是什麼？

例如：

```python
if points < 100:
```

要確認這個判斷使用的是：

> **原始 points 還是修改後 points？**

---

### ④ 不同條件是否可以同時成立？

如果可以：

```python
if
if
if
```

如果只能選其中一條：

```python
if
elif
else
```

---

### ⑤ 官解不是唯一寫法

自己的程式和官解不同：

> **不代表自己的程式錯。**

先確認：

1. 結果是否正確
2. 邏輯是否正確
3. 是否容易理解
4. 是否符合題目要求

---

# 20. Part 1 最重要的英文

| English | 中文 |
|---|---|
| variable | 變數 |
| value | 值 |
| input | 輸入 |
| output | 輸出 |
| condition | 條件 |
| statement | 陳述式／敘述 |
| assignment | 賦值 |
| comparison | 比較 |
| integer | 整數 |
| float | 浮點數 |
| string | 字串 |
| factor | 因子／因素／倍率 |
| root | 根／解 |
| discriminant | 判別式 |
| square root | 平方根 |
| temperature | 溫度 |
| points | 點數 |
| factor | 倍率 |
| original | 原始的 |
| result | 結果 |

---

# Part 1 Cheat Sheet

```python
# 輸出
print("Hello")

# 輸入
name = input("Name: ")

# 整數
number = int(input("Number: "))

# 小數
price = float(input("Price: "))

# 條件
if number > 10:
    print("Large")

# 多條件
if number > 10:
    ...
elif number > 5:
    ...
else:
    ...

# 比較
==  !=  <  >  <=  >=

# 運算
+  -  *  /  **

# 複合賦值
+=  -=  *=  /=

# f-string
print(f"Value: {number}")

# 平方根
from math import sqrt
sqrt(9)

# 次方
9 ** 2

# 布林值
True
False
```

---

## Part 1 學習檢查

如果下面這些你能大致理解，就可以往 Part 2 前進：

- [ ] 能使用 `input()` / `print()`
- [ ] 知道 `input()` 得到的是 `str`
- [ ] 知道什麼時候需要 `int()` / `float()`
- [ ] 能建立與修改變數
- [ ] 能使用 `if / elif / else`
- [ ] 理解縮排
- [ ] 能使用 `==`, `!=`, `<`, `>`, `<=`, `>=`
- [ ] 知道 `=` 和 `==` 的差別
- [ ] 知道 `**` 是次方
- [ ] 知道 `^` 不是 Python 的次方
- [ ] 能使用 f-string
- [ ] 能把簡單數學公式拆成 Python
- [ ] 知道 `factor` 可以表示倍率
- [ ] 知道 `discriminant` 是判別式
- [ ] 能理解為什麼有時候要先決定 `factor`，最後才修改 `points`
- [ ] 做題時會先自己思考，而不是看到題目就找答案

---

## 最後記住

Part 1 最重要的不是背完所有語法，而是開始養成：

> **看問題 → 拆成小步驟 → 決定資料要怎麼流動 → 再寫 Python。**

遇到不會的英文或數學，不需要停下來把整個英文／數學重新學完。

**需要什麼，就補什麼。**

這樣繼續往 Part 2 前進即可。
