# Python-Basic

## Table of Content
[型態、變數、運算子、型態轉換](#型態、變數、運算子、型態轉換)
[計算類語法](#計算類語法)
[尋找取代](#尋找取代)
[轉換](#轉換)
[排序](#排序)
[處理異常語法](#處理異常語法)
[系統功能](#系統功能)
[流程控制(if/for/while/break/def)](#流程控制(if/for/while/break/def))


## Type、Variable、Operator、型態轉換
### 特性 ／方法
- 切割取出： 
  使用`[起點:終點]`語法，適用於string或array，注意終點沒有被包含
  支援反向呼叫、支援取數值`[開始,結束,間隔]`或`[開始:]` 或`[:結束]`
```python
name = 'Euli'
names = ['Euli','Tim','Adam','Kelvin']
print(name[1:2]) #output: u
print(names[0:2]) #output: ['Euli','Tim']
```
- 確認存在的用法：
```python
name = 'Eulisha'
names = ['Euli','Tim','Adam']
print('Euli' in name) #output: True
print('Euli' in names) #output: True
```
- 長度： `len()`，適用於string或array

### 主要的型態
  - Number 數字: `int` 整數、 `float` 小數
  - String 字串: `str` 
    - 一般字串 `student = 'Euli'`
    - 多行字串 
    ```python
    intro = '''My name is Euli.
    I'm learning python now.
    '''
    ````
    - 字串可以透過index來取出字母 `變數[index]`
    ```python
    name = 'Euli'
    print(name[0]) #output: E
    ```
    - 跳脫字元: `\` 例如`'I\'m student'`
    - 組合：`字串+字串`
    - 格式化字串：
    1. `%`方式
        將指定格式之變數插入字串之中 %方式 `“字串 %s/d/f 字串”%(變數1,變數2)` 
    2. `.format()` 方式
      ```python
      name = 'Euli'
      job = 'intern engineer'
      hobbit = 'coding'
      intro = 'I am {name}. I am a {job}. I like {hobbit}.' #用變數命名
      print(intro.format(name=name, job=job, hobbit=hobbit))
      intro = 'I am {1}. I am a {2}. I like {0}.'  #指定傳入的index
      print(intro.format(hobbit, name, job))
      ```
    3. f-String 方式
      `f”字串{變數/函式名}字串”` #python在判斷時會向上搜尋對應的變數
    #### 其他string方法
    - 清除空格 `字串.strip()`
    - 取代: `字串.replace('字串','字串')`
    ```python
    name = 'Euli'
    print(name.replace('uli', 'llie)) #output: Ellie
    ```
    - 切分：將字串切分並輸出成一個array `字串.split('分隔符號')`
    ```python
    intro = 'Hi, my name is Euli'
    print(into.split(' ')) #output: ['Hi,', 'my', 'name', 'is', 'Euli'] 
    ```
    - 查詢：在某個區間內尋找某字串 `字串.find(字串,開始,結束)`
    - 大小寫轉換
      - 大寫: `字串.upper()` 
      - 小寫: `字串.lower()` 
  - Boolean 布林: `bool`
    值為大寫的`True`或`False`，`
    Falsy value有：`0`、`None`、`''`、`()`、`[]`、`{}`
  - List 清單: `清單名 = [物件1, 物件2]`
    - 呼叫：`清單名[索引][二階索引]`
    - `list名稱.append(物件)`: 增加物件在最後一格, 若為物件組合彙整組放進去
    - `list名稱.insert(index,物件)`: 將增加物件加在指定index之前，這個方法只能放單一物件
    - `list名稱.pop()` #刪除最後一格
    - `list名稱.exend(物件組合)`: 將物件組合中的物件一一拿出來並放入指定list
    - 可以直接對一個區間的物件作修改
  - Dict字典: `字典名 = {key1:value1, key2:value2}`
    #數字/字串/turple都可以做key #不可相加 #若key重複後面會取代前面
    呼叫： `dic名稱[”key名稱”]`
    新增：`字典名[key名]=內容`  
    合併：`字典1.update(字典2)`
    `dic名稱.items()` 、`dic名稱.keys()`、`dic名稱.values()` #把dic變成包含key,value的list回傳
    `for key, vlaue in dic名稱.item/keys/values()` #透過for可以將key和value呼叫出來
    `dic名稱[”key名稱”]=值` #更新字典內物件的值
    `dic名稱[”新key名稱”]=值` #新增物件至字典最後
  - Tuple 元組: 序列、不可更變 `(物件,物件)` #從def回傳多個值時為tuple型態
    - 取得型態: `type(變數)`
    - 型態轉換: `float(3)`、`int(5.0)`、`str(3)`
    - 指定型態casting: 如果有需要指定變數的型別，可以透過以下方法來指定`x=int(1)`
  - Set: 非序列、不可更變、不允許重複

### 變數
#### 基本篇
  - 在Python當中，不需要做變數宣告，直接建立變數即可
  ```python
  x = 5
  y = 'Euli'
  ```
  
  - 非法的變數命名
    - 數字開頭： `2myname`
    - 使用「-」連接： `my-name`
    - 中間有空格： `my name`
    
  - 一次命名多個變數
  ```python
  python_king, algo_king, king_of_all = '小林','Jimmy','Kelvin'
  python_king = algo_king = C++_king = 'Kelvin'
  ```
  
  - 變數可以直接被覆蓋
  ```python
  x = 5
  x = 'Euli'
  print(x) #output: Euli
  ```
  
  - 取得變數的type
  ```python
  x = 5
  y = 3.0
  z = 'Euli'
  print(x) #output: <class 'int'>
  print(y) #output: <class 'float'>
  print(z) #output: <class 'str'>
  ```
  
  - 解構List
  ```python
  fruits = ["apple", "banana", "cherry"]
  x, y, z = fruits
  ```
#### 全域變數 與 區域變數
- 在python，只要是宣告在非function之外的變數都是全域變數，function裡面可以取用、也可以對他進行覆值。不過在function裡面對全域變數的改動，僅限於function內，不會更動到全域的值。
```python
king = 'kelvin'

def change_king(new_king):
  king = new_king
  print(king) #output: claudia
change_king('claudia')

print(king) #output: kelvin
```
- 若要改變，可以透過 `global 變數`來執行。 
```python
king = 'kelvin'

def change_king(new_king):
  global king
  king = new_king
  
change_king('claudia')
print(king) #output: claudia
```

### 運算子
- 普通的四則： `+`、`-`、`*`、`/`、`%`、`**` 次方、`//` 無條件捨去
  - 支援上面符號的簡化運算寫法：`x+=1`；但沒有`x++`
- 比較符號：`==`、`!=`、`>`、`<'、`>=`、`<=`
- 邏輯符號：`and`、`or`、`not`、 `is`、`is not` 
  - 注意binary數值與上述使用不同的符號
`len(物件)` #可以算出String/list/dic/turple長度
`count(字串,開始,結束)`:從某個區間中計算某個字串出現的次

### 排序
`清單.sort(reverse = True/False, key=指定排序方式)` #常配合`operator`使用
`sorted(清單)` #其餘用法同sort

### 處理異常語法
try語法
`try:`
`執行內容`
`except 異常名稱:`
`執行內容`

#常用異常名稱: `ValueError` (傳入無效的參數)

### 系統功能
  - 輸出: `print(物件,物件)` #物件間預設一個空白間隔、print後預設一個空行
    `print(物件,物件,end=”string”)`  #將預設的空行改為指定
    `print(物件*次數)` #將物件輸出數次，支援string/list/tuple

  - 輸入: `input(”提示文字”)` #輸入進來的內容一率為string型態
  - Comment 註解: 
    - 單行註解: `#註解` 
    - 多行註解: `"""註解"""` 或者 `'''註解'''`
  - 換行: 
    - `“\n”` 輸出時換行
    - `\` 程式碼換行
    - `\”` `\’` 已定義之符號要使用在字串時需加入\

anaconda安裝模組位置: C:\Users\user\anaconda3\Lib\site-packages

### Error 釋義
unhashable 非不可變得值
unsubscriptable: 非可以索引的(被下標)

定義：
def return多個值，可以用x,y=a(x,y)直接承接
for可以有多個變數,但只能提取list/dic ex. for x,y in [[1,2],[3,4]]
for 可以提turple(def回傳的值), 再用x[0]來把值提出來
如果def沒有return值，則會回傳None

### 流程控制(if/for/while/break/def)
If語法  #搭配的條件判斷有： `and` `or` `not` `==` `!=` `>` `<` `>=` `<=`
`if 條件1:`
`指令1`
`elif 條件2:`
`指令2`
`else 條件3:`
`指令3`

#判斷式成立後即會停止
`if 值 in 物件:` #可以判斷一個值是否有在物件中

Def語法
`Def 函式名稱(傳入值1,傳入值2):`
`定義內容`
`return 回傳值1,回傳值2,回傳值3`
`接回傳值變數1, 接回傳值變數2, 接回傳值變數3=函式名稱(傳入值1,傳入值2)`

函式名稱
#def是獨立的子程式，和外面的主程式使用之變數互不相通，故需要使用return來傳遞
#執行def時需將要求之值或變數傳入子程式
#子程式執行完成後，用return將指定的值依序傳出來 
**傳出的值/變數與傳入不相關，數量和名稱都不用相同
**傳出的值需要主程式有變數來接，可以一次用多個變數來相等
可以將函式傳入函式，用 `函式名(函式名)`，被傳入的函式不需要加上()
For迴圈  #可使用string/list/dic(提出key)
`for 變數 in 物件組合:`
`指令`
`for 變數 in range(開始,結束,間距):`   #只能是數字，若直接輸入一數則預設為0~n-1
`指令`
#提取出的變數，不一定要和指令相關，可當成重複物件次來用
#變數可以有多個

While語法
`while 判斷式:`
`執行內容`
停止遞迴：可以用`break`: 完全終止遞迴 或 `continue`: 終止此圈重下一圈開始
