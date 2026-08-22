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
