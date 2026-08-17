可以。Part 5 的筆記建議以**「之後複習能快速找回概念」**為主，不把每一題的完整解法塞進去。下面整理成可直接存成 `.md` 的版本。

````md
# Helsinki Python MOOC — Part 5 筆記

> 主題：Dictionary、Tuple、Function、資料結構與 Problem Solving

---

## 1. Dictionary 字典

Dictionary 用來儲存「鍵（key）→ 值（value）」的對應關係。

```python
students = {
    "Peter": {},
    "Emily": {}
}
````

取得資料：

```python
students["Peter"]
```

新增或修改：

```python
students["Peter"] = {}
students["Peter"]["Introduction to Programming"] = 5
```

---

## 2. 判斷 Key 是否存在

```python
if name in students:
    ...
```

```python
if name not in students:
    ...
```

例如：

```python
if name not in students:
    print(f"{name}: no such person in the database")
```

這是處理 Dictionary 時非常常用的判斷。

---

## 3. Dictionary 的 `.items()`

`.items()` 可以同時取得 key 和 value。

```python
for course, grade in students[name].items():
    print(course, grade)
```

例如：

```python
courses = {
    "Programming": 5,
    "Databases": 4
}

for course, grade in courses.items():
    print(course, grade)
```

輸出：

```text
Programming 5
Databases 4
```

---

## 4. Nested Dictionary 巢狀字典

Dictionary 的 value 也可以是另一個 Dictionary。

例如：

```python
students = {
    "Peter": {
        "Programming": 5,
        "Databases": 4
    },
    "Emily": {
        "Programming": 3
    }
}
```

取得 Peter 的課程：

```python
students["Peter"]
```

取得 Peter 的 Programming 成績：

```python
students["Peter"]["Programming"]
```

這種結構在實際程式中非常常見。

---

## 5. `len()` 計算資料數量

Dictionary：

```python
len(students)
```

代表學生人數。

```python
len(students["Peter"])
```

代表 Peter 已完成的課程數。

---

## 6. Tuple

Tuple 使用小括號：

```python
course = ("Introduction to Programming", 5)
```

可以透過 index 取得資料：

```python
course[0]
course[1]
```

也可以直接解包：

```python
lesson, score = course
```

這樣：

```python
lesson
```

就是課程名稱。

```python
score
```

就是成績。

---

## 7. Tuple 解包

Tuple 可以一次指定給多個變數：

```python
course = ("Programming", 5)

lesson, score = course
```

等同於：

```python
lesson = course[0]
score = course[1]
```

這種寫法在處理函式參數時很方便。

---

## 8. Function 函式

Part 5 開始大量使用函式來拆分程式。

例如：

```python
def add_student(students: dict, name: str):
    students[name] = {}
```

呼叫：

```python
add_student(students, "Peter")
```

函式可以讓一個程式拆成多個獨立功能。

---

## 9. Type Hint

函式參數可以標示型別：

```python
def add_student(students: dict, name: str):
    ...
```

代表：

* `students` 預期是 `dict`
* `name` 預期是 `str`

這主要是幫助閱讀與工具檢查，不會自動阻止錯誤型別。

---

## 10. Dictionary + Function

常見的函式設計方式：

```python
def add_student(students: dict, name: str):
    students[name] = {}
```

資料由外部建立：

```python
students = {}
```

再傳入函式：

```python
add_student(students, "Peter")
```

Python 中 Dictionary 是 mutable，因此函式可以直接修改原本的 Dictionary。

---

# Student Database 重要觀念

## 11. 學生資料結構

Student Database 的核心結構可以理解成：

```text
students
  ├── Peter
  │     ├── Programming → 5
  │     └── Databases → 4
  │
  └── Emily
        └── Programming → 3
```

對應：

```python
students = {
    "Peter": {
        "Programming": 5,
        "Databases": 4
    },
    "Emily": {
        "Programming": 3
    }
}
```

---

## 12. `add_student`

新增學生：

```python
def add_student(students: dict, name: str):
    students[name] = {}
```

新學生一開始沒有完成任何課程：

```python
{
    "Peter": {}
}
```

---

## 13. `print_student` 的基本流程

處理一個學生時，可以先判斷：

```python
if name not in students:
    ...
else:
    ...
```

如果學生存在，再判斷是否有完成課程：

```python
if students[name] == {}:
    ...
else:
    ...
```

這形成兩層條件：

```text
學生不存在
    ↓
顯示不存在

學生存在
    ↓
是否有課程？
    ├── 沒有
    └── 有
```

---

## 14. 計算平均成績

可以使用累加：

```python
total = 0

for course, grade in students[name].items():
    total += grade
```

最後：

```python
average = total / len(students[name])
```

基本概念：

```text
平均 = 總和 / 數量
```

---

## 15. `add_course` 的重要邏輯

新增課程時需要處理：

### 成績為 0

不加入資料庫。

```text
0 = 不及格
```

### 同一門課已經存在

如果新成績比較低：

```text
保留原本較高成績
```

如果新成績比較高：

```text
更新成較高成績
```

因此核心邏輯：

```text
新課程
 ├── 成績 0 → 不記錄
 └── 非 0
      ├── 課程不存在 → 新增
      └── 課程已存在
           ├── 新成績較低 → 不更新
           └── 新成績較高 → 更新
```

---

# Problem Solving

## 16. 不要只想「我要寫什麼語法」

Part 5 開始，題目會逐漸要求：

```text
問題
 ↓
拆解
 ↓
找資料結構
 ↓
找規則
 ↓
轉成程式
```

而不是：

```text
看到題目
 ↓
想一個 Python 語法
```

---

## 17. A Square of Letters

這題是一個典型的 Problem Solving 題。

例如：

```text
CCCCC
CBBBC
CBABC
CBBBC
CCCCC
```

核心規律：

```text
中心 = A
距離中心 1 層 = B
距離中心 2 層 = C
```

因此可以把問題轉換成：

```text
座標
 ↓
計算距離中心
 ↓
決定 layer
 ↓
layer → 字母
```

---

## 18. `abs()`

`abs()` 取得絕對值：

```python
abs(-3)
```

結果：

```text
3
```

在座標問題中很常用：

```python
distance = abs(x - center)
```

因為距離不能是負數。

---

## 19. `ord()` 與 `chr()`

可以利用 ASCII / Unicode 編碼在字元與數字之間轉換。

```python
ord("A")
```

得到 `"A"` 的數值。

```python
chr(65)
```

得到：

```text
A
```

因此：

```python
chr(ord("A") + 2)
```

得到：

```text
C
```

可以用來把：

```text
0 → A
1 → B
2 → C
3 → D
```

---

# Part 5 的重要思維

## 20. Dictionary 的核心

要熟悉：

```python
key in dictionary
```

```python
dictionary[key]
```

```python
dictionary[key] = value
```

```python
dictionary.items()
```

```python
len(dictionary)
```

---

## 21. Tuple 的核心

要熟悉：

```python
course = ("Programming", 5)
```

```python
course[0]
course[1]
```

以及：

```python
course_name, grade = course
```

---

## 22. Nested Data

遇到：

```python
students[name]
```

先確認這一層資料是什麼。

不要一看到：

```python
students[name].items()
```

就只背語法。

要理解：

```text
students
 ↓
某個學生
 ↓
該學生的課程 Dictionary
 ↓
課程名稱 + 成績
```

---

## 23. Part 5 學習重點

Part 5 不只是記新語法。

真正重要的是：

1. Dictionary 的操作
2. Nested data structure
3. Tuple 與 unpacking
4. Function 拆分問題
5. 使用迴圈處理資料
6. 條件判斷
7. 累加與平均
8. 從題目找出規律
9. 把問題轉換成資料結構
10. 把 problem solving 轉換成程式

---

## 24. 學習策略

MOOC 是主線。

遇到題目時：

```text
先自己想
    ↓
自己嘗試
    ↓
測試
    ↓
除錯
    ↓
仍卡住 → 接受少量提示
    ↓
完成
    ↓
再理解為什麼
    ↓
繼續下一題
```

不要為了「一定要完全獨立解出每一題」而在單題上耗掉大量時間。

也不要把每一題的解法背起來。

真正需要留下的是：

> **遇到類似問題時，能不能重新想到解法。**

---

# 本 Part 容易忘記的語法

```python
# Dictionary
data[key]

# 判斷 key
if key in data:
    ...

if key not in data:
    ...

# Dictionary items
for key, value in data.items():
    ...

# Tuple
a, b = (1, 2)

# 長度
len(data)

# 絕對值
abs(number)

# 字元 ↔ 數字
ord("A")
chr(65)

# 累加
total += value
```

---

# 一句話總結

> **Part 5 的核心不是背更多 Python 語法，而是開始學會把「資料」與「問題」轉換成程式可以處理的結構。**

```
```
