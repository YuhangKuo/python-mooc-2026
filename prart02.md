對，我看到了。你 GitHub 上現在的 `prart2` **不是 Markdown 壞掉，而是我上一版給你的內容本身就錯了**。你貼上去後，最外層的 Markdown 程式碼圍欄也一起被存進檔案了。([GitHub][1])

例如你現在檔案開頭直接變成：

```text
可以，這次我用**純 Markdown 原始碼**整理...
```

接著：

`````text
````markdown
# Python Programming MOOC — Part 2 筆記
`````

這當然會讓 GitHub 顯示異常。

### 正確做法

你的 `prart2` 檔案**內容第一行就應該是**：

```markdown
# Python Programming MOOC — Part 2 筆記
```

而不是：

```text
可以，這次我用...
```

也不要包含最外層的：

````markdown
```markdown
...
```
````

那只是我為了讓你在聊天裡「複製原始 Markdown」而加的外框，**不應該貼進檔案**。

---

另外我重新看了你的 GitHub 檔案，還有一個問題：你目前檔案叫 **`prart2`**，不是 `PART2.md`。GitHub 現在把它當成沒有 `.md` 副檔名的檔案，所以也不會按照 Markdown 文件正常呈現。([GitHub][1])

### 我建議你直接改成

```text
PART2.md
```

然後內容：

````markdown
# Python Programming MOOC — Part 2

## 核心概念

- `while`
- `while True`
- `break`
- `if / elif / else`
- `and / or`
- 計數器（counter）
- 累加器（accumulator）
- 狀態變數（state variable）
- 巢狀 `if`
- 從題目敘述拆解程式邏輯

---

## 1. `while`

`while` 讓程式在條件成立時重複執行。

```python
number = 1

while number <= 5:
    print(number)
    number += 1
````

---

## 2. `while True` + `break`

不知道要重複幾次時，可以使用：

```python
while True:
    ...
```

再用 `break` 決定何時停止：

```python
while True:
    number = int(input("Number: "))

    if number == 0:
        break
```

基本思考：

```text
輸入
 ↓
判斷是否停止
 ↓
否 → 處理資料
 ↓
回到迴圈
```

---

## 3. 計數器

用變數記錄發生幾次：

```python
count = 0

while True:
    number = int(input("Number: "))

    if number == 0:
        break

    count += 1
```

`count += 1` 等同於：

```python
count = count + 1
```

---

## 4. 累加器

用變數保存累積結果：

```python
total = 0

while True:
    number = int(input("Number: "))

    if number == 0:
        break

    total += number
```

---

## 5. 狀態變數：`previous`

有時候需要記住「上一輪」的資料。

```python
previous = ""

while True:
    word = input("Please type in a word: ")

    if word == "end" or word == previous:
        break

    story += word + " "
    previous = word
```

`previous` 保存上一個輸入，讓下一輪可以比較。

例如：

```text
apple
↓
previous = "apple"

banana
↓
previous = "banana"

banana
↓
目前輸入 == previous
↓
break
```

---

## 6. `if / elif / else`

```python
if condition:
    ...
elif another_condition:
    ...
else:
    ...
```

例如：

```python
if number > 0:
    print("Positive")
elif number < 0:
    print("Negative")
else:
    print("Zero")
```

---

## 7. 巢狀 `if`

一個 `if` 裡可以再放另一個 `if`。

閏年是很好的例子：

```python
if year % 100 == 0:
    if year % 400 == 0:
        break
elif year % 4 == 0:
    break
```

白話理解：

> 4 的倍數通常是閏年；100 是例外；400 又是例外中的例外。

例如：

```text
2024 → 閏年
1900 → 不是閏年
2000 → 閏年
2023 → 不是閏年
```

---

## 8. `and` / `or`

### `and`

兩個條件都必須成立：

```python
if age >= 18 and has_id:
    ...
```

### `or`

其中一個成立即可：

```python
if word == "end" or word == previous:
    break
```

如果兩個條件最後都做同一件事，可以考慮合併。

原本：

```python
if word == "end":
    break
elif word == previous:
    break
```

可以寫成：

```python
if word == "end" or word == previous:
    break
```

---

## 9. 不一定每件事都需要一個變數

例如最後的數字統計題。

可以記錄：

```python
numbers = 0
positives = 0
```

負數不一定需要另外建立 `negatives`：

```python
numbers - positives
```

因為：

```text
總數 = 正數 + 負數
```

所以：

```text
負數 = 總數 - 正數
```

這可以減少需要維護的狀態。

---

## 10. Part 2 常見模式

### 持續輸入直到特殊值

```python
while True:
    value = input()

    if value == "end":
        break

    ...
```

### 計數

```python
count = 0

while True:
    ...

    if ...:
        break

    count += 1
```

### 累加

```python
total = 0

while True:
    ...

    if ...:
        break

    total += value
```

### 保存上一輪

```python
previous = ""

while True:
    current = input()

    if current == previous:
        break

    previous = current
```

---

## 11. Part 2 最重要的學習

Part 2 的核心不是背題目答案，而是開始理解：

> **程式需要保存哪些狀態，以及什麼時候更新這些狀態。**

最重要的幾種變數：

```text
count    → 計數
total    → 累加
previous → 記住上一輪
```

---

## 12. 寫完後再比較官解

推薦流程：

```text
自己理解題目
↓
自己嘗試
↓
執行與測試
↓
Debug
↓
通過測試
↓
看官解
↓
比較自己的寫法
↓
找出更簡潔的思路
```

**先寫對，再考慮簡化。**

自己的正確答案可以保留。

官解的價值是學習另一種思考方式，而不是要求自己一定要寫得一模一樣。

---

## Part 2 一句話總結

> **Part 2 開始讓 Python 程式能持續取得資料、保存狀態、更新狀態，並根據條件決定何時停止。**

```

**這次請把上面真正的 Markdown 內容貼進檔案，不要把最外面的聊天說明一起貼進去。**

而且我建議你順便把 `prart2` 改成 `PART2.md`。你目前 GitHub 上這個檔案確實是 `prart2`。:contentReference[oaicite:2]{index=2}
```

[1]: https://github.com/YuhangKuo/python-mooc-2026/blob/main/prart2 "python-mooc-2026/prart2 at main · YuhangKuo/python-mooc-2026 · GitHub"
