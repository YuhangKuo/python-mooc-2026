# Helsinki Python MOOC — Part 4 筆記

## 1. Functions 函式

### 基本結構

```python
def function_name(parameter):
    # function body
    return value
```

* `def`：定義函式
* `parameter`：參數
* `return`：回傳值
* 函式可以把重複的邏輯封裝起來。

### `return` 與 `print`

```python
def square(x):
    return x * x
```

`return` 是把結果交回呼叫端，不等於直接印出結果。

```python
result = square(5)
print(result)
```

---

## 2. `main` 函式

可以把程式主要流程放進：

```python
def main():
    # program logic


if __name__ == "__main__":
    main()
```

### 觀念

* `main()`：程式主要執行流程
* `if __name__ == "__main__":`：只有直接執行此檔案時才執行 `main()`
* 有助於把**函式定義**與**程式執行流程**分開。

---

## 3. List 串列

### 建立

```python
numbers = [1, 2, 3, 4]
```

### 索引

```python
numbers[0]
numbers[1]
```

Python 索引從 `0` 開始。

### 負索引

```python
numbers[-1]
```

代表最後一個元素。

---

## 4. Nested List 巢狀串列

List 可以包含其他 List：

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```

取得元素：

```python
matrix[0][1]
```

先取得第一個 list，再取得其中索引 `1` 的元素。

---

## 5. `input().split()`

可以把一行輸入依空白切割：

```python
words = input().split()
```

例如：

```text
hello world python
```

會得到：

```python
["hello", "world", "python"]
```

如果需要數字，要自行轉換：

```python
numbers = [int(x) for x in input().split()]
```

---

## 6. `while True` + `break`

適合需要「一直執行直到某個條件成立」的情況：

```python
while True:
    command = input()

    if command == "quit":
        break
```

### 觀念

* `while True`：建立持續迴圈
* `break`：立即離開迴圈
* 適合輸入型程式。

---

## 7. Slice 切片

基本形式：

```python
list[start:stop]
```

注意：

> `stop` 不包含。

例如：

```python
numbers = [0, 1, 2, 3, 4]

numbers[1:4]
```

結果：

```python
[1, 2, 3]
```

### 反向切片

可以使用負數與負步長：

```python
numbers[::-1]
```

取得反轉後的 list。

---

## 8. 常用內建函式

### `sum()`

```python
sum(numbers)
```

計算總和。

### `max()`

```python
max(numbers)
```

取得最大值。

### `abs()`

```python
abs(-5)
```

得到絕對值：

```text
5
```

這些函式可以直接使用，不需要自己重新實作。

---

## 9. f-string

適合將變數放進字串：

```python
name = "Peter"
age = 20

print(f"{name} is {age} years old")
```

`f"..."` 讓 `{}` 裡面的 Python 表達式被計算。

---

## 10. String Multiplication

字串可以乘上整數：

```python
print("*" * 5)
```

結果：

```text
*****
```

這在輸出星號圖形、分隔線等題目非常方便。

---

# 11. Grade Statistics

Part 4 的重要練習之一是 **Grade Statistics**。

這個練習的核心不是單純算平均，而是學習：

> **輸入資料 → 儲存資料 → 計算 → 分類 → 輸出**

典型資料流程：

```text
輸入
 ↓
取得分數
 ↓
儲存
 ↓
計算平均
 ↓
依門檻分類 Grade
 ↓
統計各 Grade 人數
 ↓
輸出結果
```

---

## 12. Boundary 邊界條件

這類題目很容易錯在：

> 「剛好等於門檻時算哪一級？」

例如：

```text
>= 90
>= 80
>= 70
```

要仔細確認題目規定的是：

* `>`
* `>=`
* `<`
* `<=`

### 原則

**不要憑直覺決定邊界。**

把題目的分數門檻逐一翻成條件。

---

# 13. Grade 作為 List Index

Part 4 很重要的一個資料設計思考：

如果 Grade 只有：

```text
0 1 2 3 4 5
```

可以直接建立：

```python
grades = [0] * 6
```

然後：

```python
grades[grade] += 1
```

例如：

```text
grade = 3
```

就直接增加：

```python
grades[3]
```

### 核心概念

> **如果資料本身有連續的數字編號，可以考慮直接利用 index 儲存對應資料。**

這比建立一堆：

```python
grade0
grade1
grade2
...
```

更合理。

---

# 14. 星號分布

如果：

```python
grades[5] == 4
```

代表 Grade 5 有 4 人。

就可以利用：

```python
"*" * grades[5]
```

產生：

```text
****
```

因此資料可以直接轉換成視覺化輸出：

```text
5: ****
4: *******
3: *****
2: ***
1: *
0:
```

這裡結合了：

* List
* Index
* Loop
* String multiplication

---

# 15. Part 4 的重要思維

Part 4 不只是「學更多語法」，而是在開始建立：

### 資料 → 結構 → 函式 → 流程

例如：

```text
原始輸入
   ↓
List 儲存
   ↓
函式處理
   ↓
條件判斷
   ↓
統計資料
   ↓
輸出
```

這是從單純寫小片段程式，開始往**完整程式結構**前進的重要階段。

---

# Part 4 核心清單

* [ ] 函式 `def`
* [ ] 參數與 `return`
* [ ] `main()`
* [ ] `if __name__ == "__main__":`
* [ ] List
* [ ] List index
* [ ] Negative index
* [ ] Nested list
* [ ] `input().split()`
* [ ] `while True`
* [ ] `break`
* [ ] Slice
* [ ] Reverse slice
* [ ] `sum()`
* [ ] `max()`
* [ ] `abs()`
* [ ] f-string
* [ ] String multiplication
* [ ] 資料統計
* [ ] Boundary 條件
* [ ] 使用 List index 設計資料
* [ ] 用星號呈現統計資料

## Part 4 一句話總結

> **Part 4 的核心，是從「會寫基本 Python」進一步學會用函式與資料結構組織一個完整的小程式。**
