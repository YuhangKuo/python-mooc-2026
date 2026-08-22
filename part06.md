可以。上一個檔案產生工具目前不可用，我直接把 **Part 6 筆記整理成可存成 `.md` 的內容**給你。

````markdown
# Helsinki Python Programming MOOC 2026 — Part 6 筆記

> Part 6 主題：Reading files、Writing files、Handling errors、Local and global variables

---

## 1. Part 6 完成內容

### Reading files
- 讀取文字檔
- `for line in file`
- `strip()` / `rstrip()`
- `split()`
- 將檔案資料整理成 `list` / `dictionary`
- CSV / 分隔資料處理

### Writing files
- `open(..., "w")`
- `open(..., "a")`
- `write()`
- `\n`
- 將資料寫入檔案

### Handling errors
- `try`
- `except`
- 輸入與錯誤處理

### Local and global variables
- local variable
- global variable
- scope
- 函式間傳遞資料

---

# 2. Reading files

基本模式：

```python
with open("file.txt") as file:
    for line in file:
        line = line.strip()
        print(line)
````

## `with open`

```python
with open("file.txt") as file:
```

預設是讀取模式。

`with` 區塊結束後會自動處理檔案關閉。

---

## `strip()` / `rstrip()`

```python
line = line.strip()
```

移除字串左右兩側的空白與換行。

```python
line = line.rstrip()
```

主要移除右側的空白與換行。

---

## `split()`

例如檔案：

```text
auto;car
roska;garbage
```

可以：

```python
parts = line.strip().split(";")
```

得到：

```python
["auto", "car"]
```

常見流程：

```text
檔案一行
↓
strip()
↓
split()
↓
取得欄位
```

---

# 3. 檔案資料與資料結構

Part 6 開始大量出現：

```text
檔案
 ↓
讀取
 ↓
解析
 ↓
整理成資料結構
 ↓
處理資料
```

例如：

```python
dictionary = {}

with open("dictionary.txt") as file:
    for line in file:
        parts = line.strip().split(":")
        dictionary[parts[0]] = parts[1]
```

---

# 4. Writing files

## `"w"`：write

```python
with open("file.txt", "w") as file:
    file.write("Hello\n")
```

`"w"` 是寫入模式。

如果檔案已經存在，原本內容會被覆蓋。

因此：

> **需要保留原有內容時，不要隨便使用 `"w"`。**

---

## `"a"`：append

```python
with open("file.txt", "a") as file:
    file.write("Another line\n")
```

`"a"` 會把新資料加入檔案尾端。

這是 `Dictionary stored in a file` 最重要的概念之一。

---

## `write()` 不會自動換行

```python
file.write("hello")
file.write("world")
```

結果：

```text
helloworld
```

如果希望下一筆資料換行：

```python
file.write("hello\n")
file.write("world\n")
```

結果：

```text
hello
world
```

---

# 5. 讀取與追加的差異

這題建立了很重要的概念：

```text
程式啟動
↓
讀取 dictionary.txt
↓
建立 Python 裡的資料
↓
程式執行
↓
使用者新增資料
↓
更新 Python 裡的資料
↓
"a" 追加到 dictionary.txt
```

也就是：

```text
檔案
    ↕
記憶體中的資料結構
```

兩邊是不同的資料。

如果只寫入檔案：

```python
file.write(...)
```

卻沒有更新 Python 中的資料：

```python
dictionary[finnish] = english
```

那麼使用者在同一次程式執行中立刻搜尋時，可能找不到剛剛新增的資料。

---

# 6. Dictionary stored in a file

這題最後通過 TMC。

自己的解法使用：

```python
dictionary = {}
```

讀取：

```python
with open("dictionary.txt") as file:
    dictionary = {}

    for line in file:
        parts = line.strip().split(":")
        dictionary[parts[0]] = parts[1]
```

新增時：

```python
dictionary[finnish] = english

with open("dictionary.txt", "a") as file:
    file.write(f"{finnish}:{english}\n")

print("Dictionary entry added")
```

搜尋：

```python
for finnish, english in dictionary.items():
    if search_term in finnish or search_term in english:
        print(f"{finnish} - {english}")
```

---

# 7. `==` 與 `in`

這題最後遇到的重要問題。

## `==`

```python
english == search_term
```

表示：

> 兩個字串必須完全相同。

例如：

```python
"swim" == "swimmer"
```

結果：

```python
False
```

---

## `in`

```python
search_term in english
```

表示：

> `search_term` 是否包含在 `english` 裡。

例如：

```python
"swim" in "swimmer"
```

結果：

```python
True
```

因此搜尋：

```text
swim
```

可以找到：

```text
uida - swim
uimari - swimmer
uimapuku - swimsuit
```

---

# 8. Dictionary 與題目中的「字典」

這題名稱是：

> Dictionary stored in a file

但這裡的「dictionary」是**芬蘭語－英語字典這個功能**。

不代表 Python 一定要使用 `dict`。

這兩種資料結構都可以完成題目。

---

## 自己的解法：Python `dict`

```python
dictionary = {
    "uida": "swim",
    "uimari": "swimmer",
    "uimapuku": "swimsuit"
}
```

搜尋：

```python
for finnish, english in dictionary.items():
    if search_term in finnish or search_term in english:
        print(f"{finnish} - {english}")
```

---

## 官解：`list + tuple`

官方解法使用：

```python
dictionary = [
    ("uida", "swim"),
    ("uimari", "swimmer"),
    ("uimapuku", "swimsuit")
]
```

然後：

```python
for word_fi, word_en in dictionary:
    if word in word_fi or word in word_en:
        print(f"{word_fi} - {word_en}")
```

---

## 兩種解法都可以

自己的 `dict` 解法：

```text
Finnish → English
```

比較像查表。

官方的：

```text
list
 ↓
tuple
 ↓
(Finnish, English)
```

比較像保存一筆一筆的翻譯配對。

這題因為可以搜尋 Finnish 或 English，而且是**部分匹配**，所以 `list + tuple` 很自然。

但自己的 `dict` 解法也能正確完成題目，而且已經通過 TMC。

### 重要觀念

> **不要因為題目叫 dictionary，就認定 Python 必須使用 `dict`。**

應該根據資料的實際操作需求選擇資料結構。

---

# 9. `list + tuple`

官方解法讓這題順便練習：

```python
dictionary = []

dictionary.append(("auto", "car"))
dictionary.append(("roska", "garbage"))
```

資料：

```python
[
    ("auto", "car"),
    ("roska", "garbage")
]
```

遍歷：

```python
for finnish, english in dictionary:
    ...
```

這裡：

```python
finnish, english
```

就是 tuple unpacking。

---

# 10. Handling errors

Part 6 開始正式處理程式可能發生的錯誤。

基本結構：

```python
try:
    # 可能發生錯誤的程式
except:
    # 錯誤發生時的處理
```

例如：

```python
try:
    number = int(input("Number: "))
except ValueError:
    print("Please type in a number")
```

重點：

> `try/except` 不是用來把所有錯誤隨便吃掉，而是處理預期可能發生的錯誤。

---

# 11. Local and global variables

## Local variable

在函式裡建立：

```python
def testing():
    x = 5
```

`x` 是 local variable。

它只存在於該函式的 scope。

---

## Global variable

函式外建立：

```python
x = 3

def testing():
    print(x)
```

函式可以讀取 global variable。

但一般來說，不應該依賴 global variable 來代替函式參數與回傳值。

比較好的方式：

```python
def calculate_sum(a, b):
    return a + b
```

透過：

```text
參數
 ↓
函式
 ↓
return
```

傳遞資料。

---

# 12. Part 6 實際除錯經驗

## `IndexError: string index out of range`

例如：

```python
word[i]
```

如果 `i` 超過字串最後一個 index，就會發生：

```text
IndexError
```

遇到這種錯誤先確認：

> 我現在存取的 index 是否一定存在？

---

## `EOFError: EOF when reading a line`

這次 Dictionary 題曾經遇到：

```text
EOFError: EOF when reading a line
```

發生在：

```python
function = input("Function: ")
```

這不一定代表 `input()` 本身寫錯。

互動式程式還要注意：

```text
程式碼
vs.
執行方式
vs.
TMC 測試環境
```

這次實際在 VS Code 終端機執行是正常的。

因此要先判斷：

> 是程式邏輯錯，還是執行／測試環境造成的錯誤。

---

# 13. Part 6 最重要的觀念

## 檔案操作

```python
open("file.txt")
```

讀取。

```python
open("file.txt", "w")
```

寫入／覆蓋。

```python
open("file.txt", "a")
```

追加。

---

## 檔案解析

```python
line.strip()
line.split(";")
```

---

## 搜尋

完全相同：

```python
a == b
```

部分包含：

```python
a in b
```

---

## 資料結構

```text
list
tuple
dict
```

不是固定哪一個最好。

要根據：

> 資料如何被儲存、搜尋、修改

來選擇。

---

## Scope

```text
local variable
global variable
function parameter
return value
```

理解變數在哪裡存在、在哪裡可以使用。

---

# 14. Part 6 完成後的能力

完成 Part 6 後，已經能處理：

```text
檔案
 ↓
讀取
 ↓
解析
 ↓
資料結構
 ↓
處理
 ↓
寫回檔案
```

並開始理解：

```text
錯誤
 ↓
try / except
```

以及：

```text
變數
 ↓
scope
 ↓
函式
 ↓
參數 / return
```

這是從單純寫小型練習，開始往實際 Python 程式靠近的重要階段。

---

# 15. Part 6 學習方式檢討

本 Part 過程維持：

```text
先自己解題
↓
TMC
↓
看錯誤
↓
自己修
↓
必要時最少提示
↓
最後才看官解
```

這次最後的 Dictionary 題尤其有價值：

* 自己完成
* TMC PASS
* 自己使用 `dict`
* 再比較官方的 `list + tuple`
* 確認兩種資料結構都能完成題目
* 理解 `==` 與 `in` 的差異
* 理解檔案資料與記憶體資料需要同步更新
* 理解 `"a"` 與 `"w"` 的差異

---

# 16. Part 6 完成狀態

**Part 6：PASS ✅**

最後一題：

**Dictionary stored in a file**

已通過 TMC。

本 Part 最重要的收穫：

> **開始真正理解「資料從檔案進入程式、在記憶體中處理，再寫回檔案」的完整流程。**

---

# 17. 下一階段

**Part 7**

Part 6 不需要再反覆重做。

如果之後遇到 Part 7 需要 Part 6 的概念，再回來查：

* file reading
* file writing
* `try/except`
* list / tuple / dictionary
* string processing
* variable scope

```
```
