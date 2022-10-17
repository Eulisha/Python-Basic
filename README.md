# Python-Basic
本文是給從Javascript想快速入門Python用的介紹

## Table of Content
- [切換時容易混亂的小提醒](#切換時容易混亂的小提醒)
  - [和Javascript有點不一樣又好用的地方](#和Javascript有點不一樣又好用的地方)
  - [轉換語言時很容易想剁手的地方](#轉換語言時很容易想剁手的地方)
  - [還是Javasciprt感覺比較方便的地方](#還是Javasciprt感覺比較方便的地方)
- [Python語法的重點整理](#Python語法的重點整理)
  - [主要的型態](#主要的型態)
  - [型態取得與轉換](#型態取得與轉換)
  - [變數](#變數)
    - [基本篇](#基本篇)
    - [全域變數 與 區域變數](#全域變數-與-區域變數)
    - [Call by value, refernce, sharing, or ??](#Call-by-value,-refernce,-sharing,-or-??)
  - [運算子](#運算子)
  - [排序](#排序)
  - [錯誤處理](#錯誤處理)
  - [重要又不重要的系統功能](#重要又不重要的系統功能)
  - [流程控制(if/for/while/break/def)](#流程控制(if/for/while/break/def))
    - [if-else](#if-else)
    - [For迴圈](#For迴圈)
    - [While迴圈](#While迴圈)
    - [Def (也就是function啦)](#Def-(也就是function啦))

## 切換時容易混亂的小提醒
### 轉換語言時很容易想剁手的地方
  - 千萬記得縮排縮排縮排！！！！
  - 是 `elif` 不是 `else if`！！！
  - if a==b 的等號只有兩個！
  - dictionary只有 `物件['key']`的用法，沒有 `物件.key`的用法
  - array 是 `for in ` 「in in in in in in」！！！唸一百變！Python沒有 `for of`這個東東！
  
### 和Javascript有點不一樣又好用的地方
- 切割取出： 
  - 使用`[開始:結束]` 或 `[開始:]` 或 `[:結束]` 語法，支援反向呼叫
  - 適用於string或array
  - 注意終點沒有被包含
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
assignment = {sqs:'Euli',rds:'Tim',dynamodb: 'Adam'}
print('Euli' in name) #output: True
print('Euli' in names) #output: True
print('sqs' in assignment) #output: True
```
- Exception有定義好各種類型可以直接用
```python
try:
  #執行內容
except (RuntimeError, TypeError, NameError):
  pass
except RuntimeError:
  print('system err')

```
  
### 還是Javasciprt感覺比較方便的地方
  - 取dict內容時，`字典名.items / keys / values()` 的方法不能直接取出內容來使用，需要另外跑迴圈
  ```python
  assignment = {'sqs':'Euli','rds':'Tim','dynamodb': 'Adam'}
  
  # 不能直接取！會噴object is not subscriptable！
  print(thisdict.values()[0])
  
  # 要像這樣自己跑迴圈轉乘可以用的array才行
  assignment_array = []
    for value in assignment.values(): 
    assignment_array.append(value)
  print(assignment_array)
  ```

  - 沒有ES6方便的解構賦值法
  ```python
  # 不能這樣用！會跳錯cannot assign to set display！
  assignment = {'sqs':'Euli','rds':'Tim','dynamodb': 'Adam'}
  {sqs, rds} = assignment 
  ```

[Python語法的重點整理](#Python語法的重點整理)
- [主要的型態](#主要的型態)
- [型態取得與轉換](#型態取得與轉換)
************
以下開始是細節: 
## Python語法的重點整理
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
    - 長度： `len()`，適用於string或array
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
      `f”字串{變數/函式名}字串”`
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
    - 長度： `len()`，適用於string或array
    - 新增物件：增加物件在最後 `list名稱.append(物件)`
    - 新增物件於指定位置：將增加物件加在指定index之前 `list名稱.insert(index,物件)`
    - 新增物件組：將物件組加在最後 `list名稱.exend(物件組)`，也可以加入tuple
    - 刪除指定物件： `list名稱.remove(物件)`
    - 刪除指定index： `list名稱.pop(index)` 如果沒有指定index則會刪除最後一個
    - 刪除大絕：`del list名稱[index]` 如果沒有指定index則會刪除整個array
    - 刪除所有物件：`list名稱.clear()`
  - Dict字典: `字典名 = {key1:value1, key2:value2}`
    - 呼叫： `字典名["key名稱"]`
    - 新增或更新值：`字典名[key名]=值`  
    - 新增或更新物件：`字典1.update(字典2)`
    - 刪除：`字典名.pop("key名")`
    - 刪除最後一個：`字典名.popitem("key")`
    - 刪除大絕： `del 字典名["key名"]` 如果沒有指定key則會刪除整個
    - 刪除所有物件：`字典名.clear()`
    - 取dict內容: `dic名稱.items()` 、`dic名稱.keys()`、`dic名稱.values()` ，注意需要跑loop才能取出來
  - Tuple 元組: 序列、不可更變 `(物件,物件)` #從def回傳多個值時為tuple型態
  - Set: 非序列、不可更變、不允許重複
  #### 型態取得與轉換
  - 取得型態: `type(變數)`
  - 型態轉換: `float(3)`、`int(5.0)`、`str(3)`
  - 指定型態casting: 如果有需要指定變數的型別，可以透過以下方法來指定`x=int(1)`

變數
- 基本篇
- 全域變數 與 區域變數
- Call by value, refernce, sharing, or ??
運算子
排序
錯誤處理
重要又不重要的系統功能

### 變數
#### 基本篇
  - 在Python的世界，不需要做變數宣告、也不需要宣告變數是否可以變更，總之直接建立即可
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
- 在python，只要是宣告在非function之外的變數就是全域變數，function裡面可以取用、也可以對他進行覆值。不過在function裡面對全域變數的改動，僅限於function內，不會更動到全域的值。
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
#### Call by value, refernce, sharing, or ??

- 拷貝物件
  python簡單複製物件的方式有以下，但都只會淺拷貝，若要深拷貝需要使用套件
  ```
  b = list(a)
  b = a[:]
  b = a.copy()
  ```
- 記憶體指派
  - 對於不可變物件(Imutable Object)如數字、字串，每次都會當然每次指派都會是新的。
  - 可變物件 (Mutable Object)如list、dictionary，傳遞的是物件的參照(記憶體位址)，所以物件裡面的內容是可以改變的
  - 但如果對可變物件重新賦值，那就會獲得新的參照，新舊物件會變成不同的物件。
  不錯的文章可以參考：
  [Python 是 Pass By Value, Pass by Reference, 還是 Pass by Sharing？](https://medium.com/starbugs/python-%E4%B8%80%E6%AC%A1%E6%90%9E%E6%87%82-pass-by-value-pass-by-reference-%E8%88%87-pass-by-sharing-1873a2c6ac46)

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

### 錯誤處理
- 接錯誤: `try.. except..`，python有區分各種類型的exception可以協助判斷
```python
try:
  #執行內容
except 錯誤種類:
  pass #跳過
except (錯誤種類1,錯誤種類2):
  #處理方式
else:
  #沒有錯誤發生
finally:
  #都結束時
```
- 拋錯誤
```python
raise Exception('內容')
```

### 重要又不重要的系統功能
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



## 流程控制(if/for/while/def)
### if-else
- 標準寫法：`if elif else`
```python
if left==target:
  mid+1 = left
elif right==target:
  mid-1 = right
else:
  return mid
```
- 再複習一下符號
  - 比較符號：`==`、`!=`、`>`、`<'、`>=`、`<=`
  - 邏輯符號：`and`、`or`、`not`、 `is`、`is not` 

- 寫成一句：
  - `if 條件: 執行1`
  - `執行1 if 條件 else 執行2 `
  ```python
  if a > b: print('a bigger')
  print('a bigger') if a > b else print('b bigger')
  ```
- 判斷是否包含： `if 值 in 物件:`

### For迴圈 
- `for 變數 in 物件組合:` 或 `for 變數 in range(開始,結束,間距):`
- 中斷時用 `break`、`continue`、`pass`
```python
names = ['Euli', 'Tim', 'Adam', 'Kelvin']
for name in names:
  print(name)
for num in range(1,7,2):   #只能是數字，若直接輸入一數則預設為0~n-1
  print(num) #1,3,5
for i in range(len(names)):
  print(names[i])
  if i == 2:
    break
```

### While迴圈
- `while:`
- 中斷時用 `break`、`continue`、`pass`
```python
while a < 5:
  print(a)
```
### Def (也就是function啦)
- `Def 函式名稱(傳入值): return`
```python
def binary_search(target):
  # algorithm
binary_search(target)
```
- return 可以多個值，外面也可以直接接多個值
```python
def group_member():
  return 'Euli', 'Tim'
student1, student2 = group_member()
```
- 可以偷用 `*` 如果不知道有幾個參數
```python
def seminar(*students):
  for student in students:
    print(student)
seminar('Euli','Tim','Adam')
```
- key-value方式傳參數： `def名(key1=value1,key2=value2)`
- 而且可以用`**`如果不知道有幾個
```python
def seminar(**student):
    print(student['Euli'])
seminar(stu1 = 'Euli',stu2 = 'Tim',stu3 = 'Adam')
```
- 也可以用default vlaue: `def 名稱(變數 = 值)`
- 可以將def傳入def：`def名(def名)`
