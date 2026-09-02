
# Python MOOC Part 10 筆記

## 1. Class Hierarchies（類別階層）

Class 可以繼承另一個 Class。

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height


class Square(Rectangle):
    def __init__(self, side):
        super().__init__(side, side)
````

### super()

用來呼叫父類別的方法。

```python
super().__init__(...)
```

---

## 2. Method Overriding（方法覆寫）

子類別可以重新定義父類別的方法。

```python
class Animal:
    def speak(self):
        print("...")


class Dog(Animal):
    def speak(self):
        print("Woof!")
```

呼叫 `Dog.speak()` 時，會使用子類別自己的版本。

---

## 3. Attribute Access

Python 常見的命名方式：

```python
self.name
self._name
self.__name
```

### `_name`

代表「這個屬性主要是內部使用」。

這是 Python 的慣例，不是真正的存取限制。

### `__name`

Python 會進行 name mangling。

主要用途是避免子類別意外覆蓋父類別的內部屬性。

---

# 4. `__str__`

決定物件使用 `print()` 時顯示什麼。

```python
class Person:
    def __str__(self):
        return self.__name
```

例如：

```python
person = Person(...)
print(person)
```

會使用：

```python
person.__str__()
```

### 注意

`__str__` 要：

```python
return "..."
```

而不是：

```python
print("...")
```

---

# 5. Magic Methods

Python 可以透過特殊方法定義運算子的行為。

## 比較

```python
__eq__    # ==
__ne__    # !=
__lt__    # <
__gt__    # >
```

例如：

```python
def __eq__(self, other):
    return self.__value == other.__value
```

---

## 運算

```python
__add__   # +
__sub__   # -
```

例如：

```python
def __add__(self, other):
    return self.__value + other.__value
```

所以：

```python
a + b
```

可能會實際呼叫：

```python
a.__add__(b)
```

---

# 6. `__repr__`

`__repr__` 是物件比較正式的表示方式。

大致可以理解成：

```text
__str__  → 給使用者看的
__repr__ → 給程式設計師 / 除錯看的
```

---

# 7. `@property`

讓 method 可以像 attribute 一樣使用。

```python
@property
def name(self):
    return self.__name
```

使用：

```python
person.name
```

而不是：

```python
person.name()
```

---

# 8. `@classmethod`

Class method 使用：

```python
@classmethod
```

第一個參數通常是：

```python
cls
```

而不是：

```python
self
```

```text
self → instance
cls  → class
```

---

# 9. Dict 管理 Objects

Dict 不只能存數字、字串，也可以存 object。

例如：

```python
self.__courses = {}
```

可以建立：

```text
課程名稱 → Course object
```

例如：

```text
"ItP"  → Course(...)
"ACiP" → Course(...)
```

查詢：

```python
self.__courses["ItP"]
```

得到的是一個 `Course` object。

---

# 10. `.values()`

如果 Dict 裡面存的是 objects：

```python
for course in self.__courses.values():
    print(course)
```

可以直接取得所有 value。

例如：

```python
courses = {
    "ItP": course1,
    "ACiP": course2
}
```

```python
courses.values()
```

會得到：

```text
course1
course2
```

---

# 11. `None` 與查詢

查不到資料時，可以回傳：

```python
None
```

例如：

```python
def get_course(self, name):
    if name not in self.__courses:
        return None

    return self.__courses[name]
```

使用：

```python
course = records.get_course("ItP")

if course is None:
    print("no entry for this course")
else:
    print(course)
```

---

# 12. Separation of Concerns

## 關注點分離

大型程式不要讓一個 Class 負責所有事情。

例如電話簿：

```text
Application
      ↓
PhoneBook
      ↓
FileHandler
```

### Application

負責：

* `input()`
* `print()`
* 選單
* 使用者互動

### PhoneBook

負責：

* 電話簿資料
* 新增資料
* 查詢資料
* 資料邏輯

### FileHandler

負責：

* 讀取檔案
* 寫入檔案

核心概念：

> 一個 Class 負責一類主要工作。

---

# 13. Dependency Injection

## 依賴注入

核心概念：

> Class 需要的物件，由外部傳進來，而不是自己建立。

---

## 不好的耦合方式

```python
class PhoneBookApplication:
    def __init__(self):
        self.__phonebook = PhoneBook()
        self.__storage_service = FileHandler("phonebook.txt")
```

這裡：

```python
PhoneBookApplication
```

自己決定一定要使用：

```python
FileHandler
```

因此兩者耦合較高。

---

## Dependency Injection

改成：

```python
class PhoneBookApplication:
    def __init__(self, storage_service):
        self.__phonebook = PhoneBook()
        self.__storage_service = storage_service
```

外部建立：

```python
storage_service = FileHandler("phonebook.txt")

application = PhoneBookApplication(storage_service)

application.execute()
```

架構：

```text
外部建立 FileHandler
        ↓
傳入 Application
        ↓
Application 使用 storage_service
```

---

## Dependency Injection 的好處

### 1. 降低耦合

Application 不需要知道 storage_service 究竟怎麼實作。

### 2. 容易替換

未來可以換成：

```text
FileHandler
DatabaseHandler
CloudHandler
APIHandler
TestHandler
```

Application 不一定需要修改。

### 3. 更容易測試

測試時可以傳入假的 storage service。

---

# 14. Course Records

Part 10 最後的 Course Records 是一個很重要的綜合練習。

官方架構：

```text
Application
      ↓
StudyRecords
      ↓
Course
```

---

# 15. Course Class

`Course` 負責「一門課」的資料。

```python
class Course:
    def __init__(self, name, grade, credits):
        self.__name = name
        self.__grade = grade
        self.__credits = credits
```

包含：

```text
name
grade
credits
```

例如：

```text
ItP
grade 5
5 credits
```

---

# 16. StudyRecords Class

`StudyRecords` 負責管理「所有課程」。

可以使用：

```python
self.courses = {}
```

資料結構：

```text
課程名稱 → Course object
```

例如：

```text
"ItP"  → Course(...)
"ACiP" → Course(...)
"FS"   → Course(...)
```

負責：

* 新增課程
* 查詢課程
* 統計課程

---

# 17. Application Class

`Application` 負責使用者介面。

例如：

```python
input()
print()
```

以及：

```text
1 add course
2 get course data
3 statistics
0 exit
```

Application 不應該自己處理所有資料邏輯。

---

# 18. 相同課程只能保留較高成績

如果已經有：

```text
ItP grade 3
```

重新輸入：

```text
ItP grade 2
```

不能降低：

```text
ItP grade 3
```

如果重新輸入：

```text
ItP grade 5
```

則更新成：

```text
ItP grade 5
```

概念：

```text
新成績 > 舊成績 → 更新
新成績 < 舊成績 → 保留舊成績
```

---

# 19. Statistics

## 課程數量

```python
number_of_courses = len(self.courses)
```

---

## 總學分

```python
credits = 0

for course in self.courses.values():
    credits += course.credits()
```

---

## 成績總和

```python
sum_of_grades = 0

for course in self.courses.values():
    sum_of_grades += course.grade()
```

---

## 平均

```python
average = sum_of_grades / number_of_courses
```

輸出一位小數：

```python
f"{average:.1f}"
```

例如：

```text
3.6666 → 3.7
3.2857 → 3.3
```

---

# 20. Grade Distribution

因為成績只有：

```text
1～5
```

可以使用 List 統計。

```python
grades = [0, 0, 0, 0, 0, 0]
```

直接使用 grade 當 index：

```python
grades[course.grade()] += 1
```

例如：

```text
grade 5 → grades[5]
grade 4 → grades[4]
grade 3 → grades[3]
grade 2 → grades[2]
grade 1 → grades[1]
```

---

## 輸出

```python
for i in range(5, 0, -1):
    grade_hits = grades[i]
    row = "x" * grade_hits
    print(f"{i}: {row}")
```

如果：

```text
grade 5 有 3 人
grade 4 有 2 人
grade 3 有 1 人
```

會得到：

```text
5: xxx
4: xx
3: x
2:
1:
```

---

# 21. Part 10 最重要的 Magic Methods

| Method     | 對應                        |
| ---------- | ------------------------- |
| `__str__`  | `print(object)` / `str()` |
| `__repr__` | 物件正式表示                    |
| `__eq__`   | `==`                      |
| `__ne__`   | `!=`                      |
| `__lt__`   | `<`                       |
| `__gt__`   | `>`                       |
| `__add__`  | `+`                       |
| `__sub__`  | `-`                       |

---

# 22. Part 10 最重要的觀念

### ① 繼承

```python
class Child(Parent):
```

Child 可以繼承 Parent。

---

### ② `super()`

```python
super().__init__()
```

呼叫父類別初始化方法。

---

### ③ Method Overriding

子類別可以重新定義父類別的方法。

---

### ④ Private-like attributes

```python
self.__value
```

用於封裝內部資料。

---

### ⑤ Magic Methods

讓自己的 Class 可以支援：

```python
==
<
>
+
-
```

等操作。

---

### ⑥ Separation of Concerns

不同 Class 負責不同事情。

---

### ⑦ Dependency Injection

依賴從外部傳入：

```python
Application(storage_service)
```

而不是：

```python
Application()
```

裡面自己建立所有東西。

---

# 23. Part 10 的整體架構思維

Part 8：

```text
Class
  ↓
Object
```

Part 9：

```text
Class
  ↓
Inheritance
  ↓
Class hierarchy
```

Part 10：

```text
Application
      ↓
Service / Manager
      ↓
Objects
      ↓
Storage / External systems
```

例如：

```text
Application
    ↓
StudyRecords
    ↓
Course
```

或：

```text
PhoneBookApplication
    ↓
PhoneBook
    ↓
FileHandler
    ↓
phonebook.txt
```

---

# 24. Part 10 核心思想

> 不要讓一個 Class 什麼都管。

把程式拆成不同責任：

```text
UI
↓
Logic
↓
Data
↓
Storage
```

這會讓程式：

* 更容易理解
* 更容易修改
* 更容易測試
* 更容易替換元件
* 更容易擴充

---

# PART 10 一句話總結

> Part 10 不只是學更多 Class 語法，而是開始學習如何讓多個 Class 分工合作，並降低 Class 之間不必要的依賴。

---

```
```
