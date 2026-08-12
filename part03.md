可以。Part 3 建議整理成**「之後真的會回來查」的筆記**，不要把 MOOC 教材整章抄一遍。

# Python MOOC — Part 3 筆記

## 1. 字串與字元

### 字串索引

```python
text = "Python"

print(text[0])   # P
print(text[1])   # y
print(text[-1])  # n
```

索引從 `0` 開始。

### 字串切片

```python
text = "Python"

print(text[0:2])  # Py
print(text[2:])   # thon
print(text[:3])   # Pyt
```

基本形式：

```python
string[start:end]
```

**`end` 不包含在範圍內。**

---

## 2. `len()`

取得字串長度：

```python
text = "abc"

print(len(text))  # 3
```

也可以用在其他序列型資料。

---

## 3. `%` 餘數運算

```python
print(7 % 3)  # 1
```

除了算餘數，還很常用來做**循環索引**。

例如：

```python
characters = "abc"

i = 0
while i < 8:
    print(characters[i % len(characters)])
    i += 1
```

結果：

```text
a
b
c
a
b
c
a
b
```

核心概念：

```text
i:      0 1 2 3 4 5 6 7
i % 3:  0 1 2 0 1 2 0 1
```

> **`%` 可以讓索引到達尾端後重新從頭開始。**

這就是 Part 3 最後 `squared` 題目很重要的技巧。

---

# 4. `while` 迴圈

基本結構：

```python
while condition:
    # 執行
```

例如：

```python
i = 0

while i < 5:
    print(i)
    i += 1
```

結果：

```text
0
1
2
3
4
```

### 常見結構

```python
i = 0

while i < limit:
    # 工作
    i += 1
```

要注意：

> 如果沒有讓條件最終變成 `False`，可能造成無限迴圈。

---

# 5. `break`

立即離開迴圈：

```python
while True:
    command = input("Command: ")

    if command == "quit":
        break
```

`break` 會直接跳出目前的迴圈。

---

# 6. `continue`

跳過這一次迴圈剩餘的程式碼，直接進入下一次迴圈。

```python
i = 0

while i < 10:
    i += 1

    if i % 2 == 0:
        continue

    print(i)
```

這裡只會處理奇數。

---

# 7. 巢狀迴圈

迴圈裡面可以再放迴圈：

```python
i = 0

while i < 3:
    j = 0

    while j < 3:
        print(i, j)
        j += 1

    i += 1
```

可以用來處理：

* 方陣
* 棋盤
* 表格
* 多層資料

---

# 8. `for` 迴圈

Part 3 開始接觸另一種常見迴圈方式：

```python
for item in collection:
    print(item)
```

例如：

```python
for character in "abc":
    print(character)
```

結果：

```text
a
b
c
```

與 `while` 最大的差別：

```text
while
→ 自己管理「現在跑到哪裡」

for
→ Python 幫你依序走過資料
```

例如：

```python
for character in "Python":
    print(character)
```

通常比自己寫索引更自然。

---

# 9. `range()`

產生一連串整數：

```python
for i in range(5):
    print(i)
```

結果：

```text
0
1
2
3
4
```

注意：

```python
range(5)
```

不是 `0 ~ 5`，而是：

```text
0 ~ 4
```

也就是**終點不包含**。

### `range(start, end)`

```python
range(2, 6)
```

得到：

```text
2 3 4 5
```

### `range(start, end, step)`

```python
range(0, 10, 2)
```

得到：

```text
0 2 4 6 8
```

---

# 10. List（串列）

List 可以存放多個值：

```python
numbers = [1, 2, 3, 4]
```

索引：

```python
print(numbers[0])
```

切片：

```python
print(numbers[1:3])
```

---

## 修改 List

```python
numbers = [1, 2, 3]

numbers[0] = 10
```

現在：

```python
[10, 2, 3]
```

與字串不同：

> **字串不能直接修改單一字元；List 可以修改元素。**

---

# 11. `append()`

在 List 尾端加入元素：

```python
numbers = []

numbers.append(5)
numbers.append(10)
```

結果：

```python
[5, 10]
```

這是非常常用的 List 操作。

---

# 12. `remove()`

移除指定值：

```python
numbers = [1, 2, 3]

numbers.remove(2)
```

結果：

```python
[1, 3]
```

注意：

`remove()` 是按照**值**移除，不是按照索引。

---

# 13. List 與迴圈

很常一起使用：

```python
numbers = [1, 2, 3]

for number in numbers:
    print(number)
```

如果需要索引，可以使用：

```python
for i in range(len(numbers)):
    print(i, numbers[i])
```

---

# 14. List 與字串

字串可以拆成字元：

```python
text = "abc"

for character in text:
    print(character)
```

也可以建立 List：

```python
characters = list("abc")
```

結果：

```python
['a', 'b', 'c']
```

---

# 15. `split()`

把字串按照分隔符切開：

```python
text = "one two three"

parts = text.split()
```

結果：

```python
["one", "two", "three"]
```

也可以指定分隔符：

```python
text = "one,two,three"

parts = text.split(",")
```

---

# 16. `join()`

把多個字串組回一個字串：

```python
parts = ["one", "two", "three"]

text = " ".join(parts)
```

結果：

```text
one two three
```

常見搭配：

```text
split()
→ 把字串拆開

join()
→ 把字串組回去
```

---

# 17. `in`

檢查元素是否存在：

```python
if "a" in "abc":
    print("found")
```

List 也可以：

```python
numbers = [1, 2, 3]

if 2 in numbers:
    print("found")
```

---

# 18. `count()`

計算出現次數：

```python
text = "banana"

print(text.count("a"))
```

結果：

```text
3
```

---

# 19. `index()`

找元素第一次出現的位置：

```python
text = "banana"

print(text.index("n"))
```

---

# 20. 字串方法

Part 3 開始會大量接觸字串操作。

常見：

```python
text.upper()
text.lower()
text.strip()
text.split()
text.count("a")
text.replace("a", "x")
```

記住：

> 方法通常是「對某個物件做事情」。

例如：

```python
text.upper()
```

而不是：

```python
upper(text)
```

---

# 21. List 與資料處理的基本思維

看到：

```python
numbers = [1, 5, 3, 8]
```

可以開始想：

```text
我要逐個處理？
→ for

我要一直做到某條件成立？
→ while

我要新增資料？
→ append()

我要找資料？
→ in / index()

我要刪資料？
→ remove()
```

這種「根據需求選工具」比死背語法重要。

---

# 22. Part 3 很重要的解題思維

### ① 不一定要把所有資料先建立好

這次 `squared` 就是一個很好的例子。

你的方法：

```text
先建立很長的循環字串
        ↓
再切出需要的部分
```

官解：

```text
目前位置 i
    ↓
直接算出這一格該拿哪個字
    ↓
加入 row
```

核心：

```python
characters[i % len(characters)]
```

---

### ② 一個變數可以代表「線性位置」

棋盤：

```text
0 1 2 3 4
5 6 7 8 9
10 11 12 13 14
...
```

可以攤平成：

```text
0 1 2 3 4 5 6 7 8 9 ...
```

再用：

```python
i % size
```

找出每一排的邊界。

這是很值得保留的思維。

---

# Part 3 最值得記住的東西

如果最後只留 **10 個重點**：

```text
1. while
2. break
3. continue
4. for
5. range()
6. List
7. append()
8. split() / join()
9. % 可以做循環索引
10. 可以把二維問題攤平成一維處理
```

其中你今天 `squared` 真正新學到、我最希望你留下的是：

```python
i % len(characters)
```

以及：

```python
i % size
```

**前者控制「字元循環」，後者控制「每排切換」。**

---

### 你現在不用做的事

今天 Part 3 結束，**不要為了筆記再把這些全部重新打一遍**。

把這份當成之後查詢用的 Markdown 筆記就好。

另外，**目前我不建議你為 Part 3 特別去看 BP**。你今天已經完成 Part 3，而且核心概念沒有留下明顯的大洞；等後面真的出現「MOOC 題目會寫，但對某個 Python 概念一直沒有完整理解」的情況，我再提醒你打開 BP。
