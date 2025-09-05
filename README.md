# XS-Stock

## 關鍵字

### 忽略字

XS語法內有一些特殊的忽略字。這些忽略字通常是英文常見的介係詞，可以任意使用在語法內，以便增加程式碼的可閱讀性。程式執行時這些忽略字會被自動省略，沒有任何作用。

目前提供的忽略字列表如下：

| A   | An   | At    | Based |
| --- | ---- | ----- | ----- |
| By  | Does | From  | Is    |
| Of  | On   | Place | Than  |
| The | Was  |       |       |

### 常數

系統內建常數

以下為系統目前提供的內建常數名稱，以及常數所對應的數值。

| 常數名稱  | 數值    |
| --------- | ------- |
| PI        | 3.14159 |
| Sunday    | 0       |
| Monday    | 1       |
| Tuesday   | 2       |
| Wednesday | 3       |
| Thursday  | 4       |
| Friday    | 5       |
| Saturday  | 6       |

在腳本內可以直接使用常數名稱，以增加可讀性。例如:

```xscript
Value1 = PI
```

跟

```xscript
Value1 = 3.14159
```

是一樣的意思，可是程式讀起來會比較清楚。

### 流程控制

在腳本撰寫的過程當中，我們可能會使用到一些比較複雜的邏輯進行運算。簡單的條列陳述沒有辦法達到這個需求，這時候我們就會需要一些流程控制的語法來幫忙。

- 條件判斷

  條件判斷是最常使用的一種流程控制，會依執行的順序依序判斷，符合後即條出。XSscript提供以下三種條件判斷式：

  [If Then Else](#ifthenelse)

  Switch Case Default

  Once
- 迴圈

  另一種流程控制是迴圈。迴圈用在計算或比較需要重複執行的情況，例如計算過去10期的值，就可以利用迴圈來完成。XSscript提供以下三種條件判斷式：

  For To (DownTo)

  While

  Repeat Until
- 中斷

  在執行的過程中，為了提升效率，可以控制電腦跳過某些計算不執行。就可以用中斷語法來達成。

  Break：跳出迴圈

  Return：跳出腳本

  Ret（RetVal）
- 多行語法

  Begin End

  XSscript的執行是一行為單位（用分號“;”結尾）。所以在流程控制中，通常都會搭配Begin…End使用。Begin…End可以讓我們用多行的陳述式進行運算，而非原先僅能使用單行陳述式。
- 數列關係

  Cross Over（Cross Above）：判斷是否黃金交叉

  Cross Under（Cross Below）：判斷是否死亡交叉
- 邏輯判斷

  Not：取得相反值

  And：判斷條件是否同時成立

  Or：判斷是否有任一條件成立

  XOR：計算差集

#### IF/THEN/ELSE

使用 **IF/THEN/ELSE** 這三個語法來判斷某個條件成立時該執行那個動作，不成立時又該執行那個動作。

如果只需要判斷某個條件成立時該執行那個動作，則使用以下的語法:

```xscript
If Close > Open Then Ret = 1;
```

在上述範例內如果Close值大於Open值的話則 Ret 變數的數值會被設定為1。

如果當條件成立時需要執行多個指令的話，則使用 **Begin/End** 的語法來包圍所需要執行的指令。

```xscript
If Close > Open Then 
Begin
    Value1 = Close - Open;
    Value2 = High - Low;
End;
```

如果條件成立時跟不成立時都需要執行不同的指令的話，則可以加入 **ELSE** 語法來定義條件不成立時該執行的動作。

```xscript
If Close > Open Then
    Value1 = Close - Open
Else
    Value1 = Open - Close;
```

在上述範例內當Close的數值不大於Open的數值時，程式會執行Else內的語法。以這個例子為例，Value1的數值就是這根bar的實體高度。

同樣的，Else之後也可以使用Begin/End語法來定義多個指令，範例如下:

```xscript
If Close > Open Then 
Begin
    Value1 = Close - Open;
    Value2 = High - Low;
End
Else 
Begin
    Value1 = Open - Close;
    Value2 = High - Low;
End;
```

Else後面也可以接if，用else if來進行多層次的條件判斷，從腳本上至下依序縮小判斷範圍，範例如下:

```xscript
if value1 < 0 then 
    value2 = 1
else if value1 < 10 then //等同於if  0 <= value1 and value1 < 10
    value2 = 2
else if value1 < 20 then //等同於if  0 <= value1 and value1 < 10
    value2 = 3
else  //等同於if  20<= value1 
    value2 = 4;
```

### 宣告

宣告是在腳本中引入變數使用。變數是用來存放計算後的數值，方便重複使用或增加腳本的可讀性。
變數需要先經過宣告的程序後才能使用，並且在宣告的同時也需要指定變數的類型、名稱或初始值等變數的屬性。

在XSscript中，一共有下列宣告變數的語法：

- 宣告變數

  Var（Variable、Variables、Vars）

  IntrabarPersist
- 宣告陣列

  Array（Arrays）
- 宣告輸入

  Input（Inputs）

  inputkind（inputkind）
- 宣告數值輸入（函數）

  Numeric

  NumericSimple

  NumericSeries

  NumericRef

  NumericArray

  NumericArrayRef
- 宣告字串輸入（函數）

  String

  StringSimple

  StringSeries

  StringRef

  StringArray

  StringArrayRef
- 宣告布林輸入（函數）

  TrueFalse

  TrueFalseSimple

  TrueFalseSeries

  TrueFalseRef

  TrueFalseArray

  TrueFalseArrayRef
