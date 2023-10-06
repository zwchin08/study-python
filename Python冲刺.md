# 【第１１章】仮想環境とパッケージ

```python
易错点
Zen = 'SimpleIsBetterThanComplex'
Zen[0] = 'J'  #错   字符串不能变   
```

![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-15-22-12-59-image.png)![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-15-22-10-55-image.png)

```
プライマリプロンプト
セカンダリプロンプト
未定義の変数はNameErrorが表示される

1-5. 四捨五入
round()関数を使う
通常の四捨五入
>>> round(3.14)
-> 3
小数点第一位で四捨五入する場合
>>> round(3.14, 1)
-> 3.1


>>> 'dosen\'t' -> "dosen't"  相同 >>> "dosen't" -> "dosent"
改行 -> \n
改行を行いたい場合はprint()を使用する。不适用的话不换行。


タブ(インデント) -> \t  
同じくprint()を使用する。


トリプルクオーテーション(シングルもしくはダブル)を使用する

文字列はn文字目を指定して変更は出来ない==>TypeError    


リストの一部を取得することをインデクシングという


正常に終了した場合にのみ実行されるfor文の中で使用出来るelse句
0~9まで出力され、for文が終了した後にelse句が実行される


kansu(1, x=10, y=20, z=30, 2, 3, 4)　　xxx    
キーワード引数の後に位置引数を書けない。



a = [1, 2, 3, 4, 5]
square = list(map(lambda x: x**2, a))
print(square)
map(関数, シーケンス)と指定するのがmap関数の使用上のルール


ダブルクオーテーションを3つ書き、その中にコメントを記述する
docstringとは？


list_num.extend([4, 5])　　　这里不能只增加数，要用列表
extend(6)としてもリストではないのでエラーになります。


pop()  First In First Out位置
print(list_num.index(1))    引数に値を指定するとindex番号が分かる

sort()  从小到大
reverse()   把list  反过来，但是不一定是从到到小，若想从大到小先使用一次sort()
在使用reverse() ，而sort(reverse=True)一次性就是从大到小

list_b = list_a  传地址
list_b = list_a.copy()  两个不同的list

キューとは
First in First out
先に入れたデータを先に出す 

data = (1, 2, 3)
data[0] = 1  #TypeError: 'tuple' object does not support item assignment
ここがタプルとリストの大きな違いです。0



モジュールの検索パス;モジュールをどこから探しているか、呼び出し先を表示
import sys
print(sys.path) 


「コンパイル済」 Pythonファイル
ファイル名.pyc がコンパイル済    __pycache__ディレクトリに保存されるみ
.pyを変更するとコンパイルを自動的にやりなおす 
pyc时py文件编译后生成的二进制文件，进行加载的时候速度很快



ジェネレータ
def word(data):
    for s in data:
        yield s

for one_word in word("game"):
    print(one_word)
```

- `data`に0~9を1つずつ追加する

```python
data = []  # 空のリストを宣言
for i in range(10):
    data.append(i)

# step1(空のリストを宣言)
data = []

# step2(for i in ~をリスト内に持ってくる)
data = [for i in range(10)]

# step3(追加する値iを先頭に書く)
data = [i for i in range(10)]
```

```python
data = [] # 空のリストを宣言
for i in range(10):
  data.append(i)
print(data)
```

```python
def reverse(data):
    # game -> 4文字 - 1, (3, -1, -1)
    # index3からindex0まで-1ずつ取得
    for index in range(len(data) - 1, -1, -1):
        yield data[index]

for char in reverse("game"):
    print(char)  
# e
# m
# a
# g
```

各コマンドの意味  
`getcwd` -> get current working directory  
`chdir` -> change directory  
`mkdir` -> make directory

```python
# OSというライブラリをインポートする
import os

# カレントディレクトリを返す
os.getcwd()

# カレントディレクトリを変更
# 現在のディレクトリ内にsampleディレクトリを作成後
os.chdir("./sample")

# ディレクトリを作成するコマンドの実行
# 上でディレクトリを変更しているのでsampleディレクトリ内にsample2ディレクトリが作成される
os.system(('mkdir sample2'))
```

```python
import glob
##glob -> 英語で「かたまり」という意味
 #globを用いることで特定のパターンにマッチするファイルを取得することができる。
# globディレクトリの「.txt」ファイルを探す
# 相対パスでpathを指定する
files = glob.glob('./glob/*.txt')
print(files) =>['./glob/sample1.txt', './glob/sample2.txt', './glob/sample3.txt']
```

```python
import zlib
#压缩
sentence = "あいうえお" * 100
print(len(sentence))

# UTF-8に指定することでbyte型になる(compressの引数はbyte型である必要があります)
after_file = zlib.compress(sentence.encode("UTF-8"))
print(len(after_file))
```

```python
仮想環境の生成: venv(旧称: pyvenv),Pythonのバージョン管理が可能な仮想環境
```

# 【第１章】Pythonのメリット

### ⽬次

1. なぜ、「Pythonは簡単」とよばれるのか？

2. 読みやすいコードの理由

3. みんなが読みやすくするために（コーディングスタイル）Coding style编码

### なぜ、「Pythonは簡単」と呼ばれるのか？

JavaやCなどを使って書くとなるとコンパイルが必要で、 コーディング→コンパイル→テスト→再コンパイル

以下は、⼤きなメリットです。

1. 簡単だと⾔って、シェルスクリプトと同様の役割ではなく⼤きなプログラムを
   書くためのデータ構造やサポート、エラーチェック機構が提供されている。

2. モジュールに分割して再利⽤が可能。（このことで同じコードを増やす必要が
   ない）

3. また、たくさんの標準モジュールが存在。

4. インタプリタ⾔語のため（1⾏1⾏読み込むため）時間の節約になる。

5. 拡張可能な為、C⾔語などからインタプリタに追加できるためバイナリ形式のラ
   イブラリをリンクすることができる。（つまり、拡張⾔語として扱うことがで
   きる。）

### 読みやすいコードの理由

1. データ型（⾼⽔準）が、複雑な操作を単⼀⽂で表記できる

2. ⽂のグルーピングはインデント  句子分组被缩进

3. 変数や引数の宣⾔が不要

## 

PEP8（https://pep8-ja.readthedocs.io/ja/latest/）は、Pythonのコーディングルール
がまとめられています。その中でも特に気を付ける部分を箇条書きでまとめます。

1. 1⾏79⽂字で折り返す。

2. 関数やクラス、関数内の⼤きめのブロックを分離するのに空⽩⾏を使う。

3. 可能であればコメントは独⽴させる。（blockコメント）

4. <mark>docstringを使う</mark>。（ドキュメンテーション⽂字列） 就是用三引号备注

5. 演算⼦の周囲やカンマの後ろにはスペースを⼊れるが、括弧の内側すぐには⼊
   れない。

```python
 a = f(1, 2) - g(3, 4)
```

6. クラスや関数には⼀貫した命名を⾏う。
   
   - <mark>クラス→キャメルケース、パスカルケース     Camel Case, Pascal Case</mark>
   
   - <mark>関数、メソッド→スネークケース                     → Snake Case</mark>
   
   - メソッドの第⼀引数として常にselfを使う。
   
   - ⽂字コードはデフォルトであるUTF-8を基本的に使うか、さらに⼀般的なASCII
     を使う。
   
   - ⽂字コード同様に、識別⼦に⾮ASCIIを⼊れないこと。

# 【第２章】インタプリタ【インタープリターの使い⽅】

### 操作⽅法

- 起動コマンド
  
  ```python
  python    
  # 実⾏すると、>>> という記号（プライマリプロンプト）が表⽰されるPrimary Prompt。
  # ちなみに、if⽂を書いてenterを押すとでる ... は、セカンダリプロンプトとい
  う。
  ```

- 終了
  
  ```python
  quit() もしくは windows Ctrl + z   苹果Ctrl + d
  
  ## ctrl + z(ファイル終端キャラクタ-EOF)を押すと、コード０（ゼロ）を返して終了
  する。
  ```

- その他
  
  ```python
  python -c <command>
  # コマンドでpythonを実⾏する
  # 例：python -c "print('hello')" ⇒ hello と出⼒。
  
  python -m <module-name>
  # モジュールを実⾏。sys.pathから指定されたモジュール名のモジュールを探し、
  #     その内容を__main__モジュールとして実行する。
  # 例：python -m main ⇒ main.pyがあるカレントディレクトリで実⾏すると、
  main.pyを実⾏する。
  Ctrl + P
  # インタプリタの⾏編集機能（対話型編集、ヒストリ置換、コード補完）が使⽤
  できるか確認できる。
  # ビープ⾳がなるなら使える。
  # ^P という⽂字が出てくる場合は使⽤できない＝バックスペースで⼊⼒中の⾏の１
  ⽂字を消すことができない。
  _（アンダースコア）
  ## 対話モードで最後に表⽰した式を代⼊してある。
  ```
  
  ![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-00-26-02-image.png)
  
  ※スクリプトモードで実⾏するとき、ソースコードはUTF-8でエンコードしないと
  正常に作動しないことがあるので、注意。
  UTF-8以外のエンコーディングを使う場合はソースコードの最初の⾏に特殊コメン
  ト⾏を追加します。
  
  ```python
  # -*- coding: encoding -*-
  ```
  
  Tabにて、変数とモジュールの**補完機能**が呼び出せます。やっている内容としてはPythonの⽂の名前、現在のローカル変数、使⽤できるモジュール名を検索する。
  また、**ヒストリ**ーはユーザーディレクトリの.python_historyというファイルに保管
  されている。

- 拡張された対話型インタプリタ
  
  bpython, **IPython**などといった標準のインタプリタから機能を増したものがある。

# 【第３章】データ定義

### ⽬次  数値と⽂字列

### 数値

1. 浮動⼩数点数のサポートもしているため、演算対象の⽅が混合していた場合、
   整数は浮動⼩数点に変換されます。  支持浮点数，计算时整型转换浮点型。
   
   ```python
   print(4 * 3.75 - 1)
   ## 14.0と表⽰されます
   ```

2. 整数、浮動⼩数点数のほかに10進数(Decimal)、有理数(Fraction)、複素数もサポ
   ートされている。
   
   ```python
   ## Decimal
   print(Decimal(1) / Decimal(7))
   ## Fraction
   print(Fraction(1, 3))
   ## complex number
   print(3+5j)
   ```

### ⽂字列

1. エスケープシーケンス
   
   ```python
   # ￥記号出したいとき
   print("\\")
   # 出⼒内で改⾏したいとき
   print("こんにちは\nこんばんは")
   # もしくは"""と改⾏で囲むことでもOK
   print("""こんにちは
   こんばんは""")
   # 例外 \nとそのまま出したいとき
   print("\\n")
   print(r"\n")
   ```

2. ⽂字列リテラルを複数⾏にわたって書く場合の⼀つとして、トリプルクォーテ
   ーションを使うことができる。

3. スライスのポイント！！！！！
   
   ```python
   +---+---+---+---+---+
   | R | e | i | n | a |
   +---+---+---+---+---+
   0   1   2   3   4   5
   -5   -4  -3  -2  -1
   ## インデックスに範囲外を指定するとIndexErrorとなるが、
   ## スライスは柔軟に対応してくれる。
   text = "Reina"
   print(text[24]) # IndexError
   print(text[2:24]) # ina    这种剩下多少打出来多少不报错
   print(text[1000:) #不报错
   print(text[1000:1000) #不报错
   ```

### ⽂字列はイミュータプル(immutable)

- そのため、変更できない。新しく⽣成する必要がある。
  
  ```python
  ## int型だと・・
  num1 = 1
  num1 = 2 ## mutableのため変更できる
  ## String型だと・・・
  text = "Reina"
  text[2] = e ## TypeError
  ```

# 【第４章】条件分岐と関数

### ⽬次

1. if文
   
   eilfの列挙で、多⾔語のswitchやcase⽂の役割も⽰してくれる。
   
   ```python
   x = int(input("整数を⼊れてください。"))
   if x < 0:
   x =0
   elif x == 0:
   print("ゼロ")
   else: ## オプションである
   print("ゼロ以上")
   ```

```
2. for⽂

- シーケンスのアイテムに対し、その順序で反復をかける。

- また、反復対象のコレクションに変更を加えるコードは⻑くなりがちなので
  コピーにループをかけたり、新しく作り直す⽅法が考えられる。

  ```python
  text = "KawaiiReinaChan"
  for i in text:
  print(i)
```

3. while⽂

ループ条件がTrueである限り実⾏を繰り返す。0はFalseであり、0でない整数が
Trueとなる。

```python
a, b = 0, 1 ## ちなみに多重代⼊という。
while a < 10:
print(a)
a, b = b, a + b
```

4. break,continueとelse
   
   - break → ループから抜ける！
   
   - continue → 後の処理⾶ばして次のループいっちゃう！
   
   - else節に注意！
     
     ```python
     for i in range(1,6):
         for x in range(1,6):
             print(i,x)
             if i / x == 1:
                 print("breakする")
                 break
             elif i / x == 2:
                 continue
                 print("---")
             else:
                 print("breakが起きなかった")
     ```

5. 関数の定義
   
   - 関数の実⾏→新しいシンボル表が導⼊され、関数内のローカル変数に使われ
     る。
   
   - 変数を参照する場合はローカル＞各関数＞グローバル＞ビルドインという順序
     になっているため、関数内からグローバル変数や外側の関数の変数の値に直接
     代⼊できない。しかし、外側の関数の変数についてはnonlocal⽂で指定すること
     ができる。
   
   - 戻り値は、1つの値を返しつつ関数から復帰するものです。式を引数に持たない
     場合はNoneを返します。また、関数の末尾に達した場合も同様。
     
     ```python
     def calc(a, b):
     """
     簡単な計算を⾏う ←ここがdocstring！
     """
     return a + b
     def calc2(a):
     print(a)
     print(calc2(0))
     ## Noneが返ってきます
     ```

6. range()関数
   
   - ビルドイン関数のrange()を使って、等差級数（ようするに指定した数字までの
     範囲を選択できること）を⽣成できる。
   
   - 終端値は⼊らないこと（range(10)の場合、０から９番⽬であること）に注意す
     る。
     
     ```python
     print(range(5, 10))
     print(range(0, 10, 3))
     ## シーケンスのインデックスで反復をかけたいときはlen()と組み合わせる
     text = "kawaiireinachan"
     for i in range(len(text)):
         print(i)
     ## enumerate()を使った場合
     text = "kawaiireinachan"
     for i, v in enumerate(text):
         print(i, v) ## インデックスと中⾝が同時に出⼒される。同時に出⼒される。
     ```

7. 引数のデフォルト値
   
   - いくつかの引数にデフォルト値を設定するということ。
   
   - コール⽅法が⾊々ある。
   
   - ＊をつけるとタプル、＊＊をつけるとディクショナリとして複数指定できる。
     （＊、＊＊の順番厳守）
     
     ```python
     def calc1(a, b=3):## デフォルト値を設定することができる
         print(a, b)
     calc1("hello")    # hello 3
     calc1("hello","world") ##hello world
      # 可変⻑引数
     def calc2(a, *args, **keywords):
         print(a)  # hello
         print(args) # ('wolrd', 'python')
         print(keywords)#  {'key': 'Yeah!!!'}
     calc2("hello", "wolrd", "python", key="Yeah!!!")
     ```

8. キーワード引数
   
   - コールするときに「キーワード＝値」の形でキーワード引数をとれる。
   
   - <mark>必ず位置引数を先に、キーワード引数を後にしなければならない。</mark>
     キーワード引数の順序を間違えると、どれの引数？ってなる。（エラーになる）
     
     ```python
     def calc1(a, b=3,c=4):
         print(a, b, c)
     calc1(a="hello")
     ## 無効なコール
     #TypeError: calc1() missing 1 required positional argument: 'a'
     # calc1() 
     #SyntaxError: positional argument follows keyword argument
     # calc1(a="hello", "world") 
     #TypeError: calc1() got multiple values for argument 'a'
     # calc1("hello", a="hello") 
     #TypeError: calc1() got an unexpected keyword argument 'aa'
     #calc1(aa="hello") 
     ```
     
     def calc1(a, b,c=4):
     
         print(a, b, c)
     
     # calc1(a="hello")
     
     calc1(b="hello",a=3)　　#ok反写顺序可以，就是括号里面如果有没登号的要写在前面
     
     ```
     
     ```

9. 特殊引数
   
   pythonの関数定義は制限されている。こうすることで、開発者の可読性、パフォーマンスが上がる。
   
   ```python
   def calc(a, b, / c, * d, e):
   ## 位置のみ/位置またはキーワード*キーワードのみ
   ## /と*はあってもなくてもOK
   ```
   
   - 1. 位置またはキーワード引数
        
        - /も*も存在しない場合、引数は位置引数、キーワード引数どちらとしても渡すことができる。
     
     2. 位置引数
        
        - 定義から、位置引数のみである引数は順序がありキーワード引数として渡
          せないため/より前に置かれる。そのため、以降は位置引数またがキーワード引数のみ。
     
     3. キーワードのみ引数
        
        - キーワード引数のみとするためには、直前に*をつける必要がある。
          
          ```python
          ## 位置またはキーワード引数
          def calc(arg):
          ## 位置引数
          def calc(arg,/):
          ## キーワードのみ引数
          def calc(*,arg)
          ```

10. 引数リストのアンパック
    
    引数にしたいものが既にリストやタプルになっている場合に、アンパックする必要がある。
    
    ```python
    def show_args(*args):
    print(args)
    return args
    args = (4,5,6,'ya')
    show_args(*args)
    ```

11. lambda
    
    ```python
    ## lamda 基礎
    def pow1(x):
        return x ** 2
    ## pow1を無名関数で書く
    pow2 = lambda x: x ** 2
    print(pow2(3))
    # 代⼊する引数aです
    a = 4
    def func1(x):
        return 2 * x**2 - 3*x + 1
    ## func1を無名関数で書いた例
    func2 = lambda x: 2 * x**2
    # 返り値の出⼒です
    print(func1(a))
    print(func2(a))
    ## 計算
    x = 5
    y = 6
    z = 2
    # lambdaを⽤いてfunc4を作成してください
    func4 = lambda x, y, z: x*y + z
    # 出⼒します
    print(func4(x, y, z))
    ## if
    # 引数が3未満ならば2を掛け、3以上ならば3で割って5で⾜す関数
    lower_three2 = lambda x: x * 2 if x < 3 else x/3 + 5
    print(lower_three2(2))
    # lambdaを⽤いてfunc5を作成してください
    func5 = lambda x: x**2 - 40*x + 350 if x >= 10 and x < 30 else 50
    # 返り値を出⼒します
    print(func5(10))
    print(func5(5))
    2 - 3*x + 1
    ```

12. 関数注釈
    
    - 完全任意のメタデータ情報。
    
    - 関数の引数や返り値にアノテーション（注釈）となる式を記述できる。
      
      ```python
      def func(x: 'x の説明', y: 'yの説明') -> '戻り値の説明':
           return x * y
      print(func.__annotations__)
      ```

# 【第５章】コレクション

### リスト

- mutaple(可変体) ＝ 内容の⼊れ替えができる

- 様々なメソッドがある

- アンパッキング     #a,b,c=list[1,2,3]
  
  ```python
  list.append(x) 　　 #末尾にアイテム1つ追加。 a[len(a):] = [x] と等価。
  
  a是一个列表，用了列表的切片这个知识点。len(a)表示获取列表a的长度。
  举例说明： a = [1,2,3] x = [4]例如列表a的长度是3，那么代入就是a[3:]，
  那么意思就是从列表往后面，增加列表x的值，因为列表是可变的，因此最终
  a列表编程[1,2,3,4],a[len(a):] = [x]这里的x其实是一个列表，可以同时添加很多数
  
  list.extend(x)　　#末尾にiterableの全アイテムを追加することでリストを伸⻑する。
  a[len(a):] = iterable と等価。
  
  list.insert(i, x)    #指定された位置にアイテムを挿⼊する。
  a.insert(len(a), x) は a.append(x)と表せる。
  ```

```
![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-09-08-56-image.png)

```python
list.remove(x)
#値が引数に等しい最初のアイテムを削除する。なければValueError.

list.pop([i])
 #指定された位置のアイテムをリストから削除し、このアイテムを返す。
 #インデックスが指定されていないと、リストの最後のアイテムを返して
 #削除する。そのため[]はオプションである。

list.clear()
#リストからすべてのアイテムを削除する。del a[:]と等価。
```

```python
list.index(x[, start[, end]])
値がxに等しい最初のアイテムのインデックスを返す。アイテムがなければValueError.
オプション引数はスライスとして解釈される。
例子 :list = ["123","234","345","456","789","234","890"]
      print(list.index("234",2,4))
意思就是你想查的在什么位置，其中start和end可以省略，查出来默认第一个"234"；如果指定
了，就在指定范围内查找。

list.count(x)
リストの中の、引数の個数を返す。

list.sort(key=None, reverse=False)
リストをインプレース（コピーを取らず直接）で、ソートする。逆順はreverse()

list.copy()
リストのコピーを返す。a[:] と等価。

del list
listを変数ごと削除する。
```

- その他、リストでできること
  
  - リストをスタックとして扱うことができる。
  
  - リストをキューとして扱う。

- **リスト内法表記**
  
  ```python
  sample_1 = [x*x for x in range(11) ]
  print(sample_1)
  ```

### 

### タプル

- immutaple(不変体)  イミュータブル

- 各要素にアクセスするときはアンパッキング、インデックスでアクセスする。

- シーケンス・アンパッキング

- タプル・パッキング
  
  ```python
  tuple1 = (1, 2)
  ## シーケンス・アンパッキング
  n, y, x = tuple3
  ## タプル・パッキング
  tuple2 = 1, 2 ## タプルの宣⾔をかっこよくした感じ
  ```

### 集合(set)

- 重複しない要素を順不同で集めたもの。

- イミュータブル  immutaple(不変体)

- 存在判定、重複エントリの排除が⽤途である。  <mark>查重</mark>

- ネストした集合の⽣成も⾏える。  可生成交集之类的。

- 削除にかかわる複数のメソッド
  
  ```python
  remove（値を指定して削除）
  
  这个discard()只能用在set上不能用在list,タプル上面
  #discard()函数不同于 remove() 函数，因为 remove() 在移除一个不存在的元素时
  #会发生错误，而 discard() 不会。
  
  discard（指定した要素をエラーなく削除）
  pop（ランダムに削除）　正常括号里面写消除的位置，如果不写默认最后一个
  clear() （すべての要素の削除）
  
  frozenset型 set型の仲間。イミュータブルであるが、辞書型のキーとして
  ⽤いることができる。違いとしては、setもfrozensetも集合であるが
  hashableである。set 对象是由具有唯一性的 hashable 对象所组成的无序多项集。
  ```

- 集合の⽐較
  
  - 完全⼀致は ==
  
  - 完全不⼀致は A.isdisjoint(B)
  
  - 部分⼀致は A.issubset(B) もしくは <=
  
  - 上位集合は A.issuperset(B) もしくは >=
    
    ```python
    set1 = {"A", "B", "C", "D"}
    set2 = set("ABCD")  ==>print(set2)==>{'B', 'A', 'D', 'C'}
    print(set1.issubset(set2))   #True竟然是对的！！！
    print(set2==set1)   #True竟然是对的！！！
    print(set2.issuperset(set1))    #True竟然是对的！！！
    ```

### ディクショナリ

- **キーの唯⼀性が特徴。**

- キーがディクショナリに存在するか確かめたいときにinというキーワードが使
  える。
  
  ```python
  dic = {"key1":"value1","key2":"value2"}
  ## ディクショナリのTips
  ## タプルをキーとする辞書の作成
  sample_2 = {(x, y): x*y for x in range(2) for y in range(2)}
  print(sample_2) #{(0, 0): 0, (0, 1): 0, (1, 0): 0, (1, 1): 1}
  ## 集合をキーとする辞書の作成
  sample_3 = {frozenset([x, y]): x*y for x in range(2) for y in range(2)}
  print(sample_3)
  #{frozenset({0}): 0, frozenset({0, 1}): 0, frozenset({1}): 1}
  
  ## ネストした辞書の作成
  sample_4 = {}
  for i in range(3):
      sample_4[i] = {}
  for j in range(3):
      sample_4[i][j] = i*j
  print(sample_4) #{0: {}, 1: {}, 2: {0: 0, 1: 2, 2: 4}}
  ##内包表記によるネストした辞書の作成
  ##通常の作成法のほかに、上記のような形でも辞書型を作成することができる。
  sample_5 = {x:{y:(x*y) for y in range(3)} for x in range(3)}
  print(sample_5)
  
  #{0: {0: 0, 1: 0, 2: 0}, 1: {0: 0, 1: 1, 2: 2}, 2: {0: 0, 1: 2, 2: 4}}
  ```

### ループのテクニック

```python
## ループのTips
list = ["A", "C", "B"]

## インデックスを伴ったループ
for i, j in enumerate(list):
    print(i,j)

## リストをソートしてループ
for i in sorted(list):
    print(i)

## リストを反転してループ
for i in reversed(list):  #反转的结果不是从到大小，而是把数列倒过来BCA
    print(i)  

dict = {"aaa":100 , "ccc":60, "bbb":200}
## 辞書のソート
list_sorted = sorted(dict)
print(list_sorted)    ==>输出只是key的一个排列 ['aaa', 'bbb', 'ccc']
## 辞書のキーと値を同時に取得
for key, val in dict.items():
    print(key,val)
```

### シーケンス、そのほか型の⽐較

```python
## ⽐較のTips
## リストの⽐較
print([1,2,3] == [1,2,3])
## タプルの⽐較
print((0,1,2) == (0,1,2))
## 集合の⽐較
print(set([0,1,2]) == set([0,1,2]))


## 異なる変数型の⽐較
print([0,1,2] == (0,1,2))  ==>False
## print([0,1,2] < (0,1,2)) ## 適切に⽐較するメソッドがないため、TypeError.
## ⼊れ⼦のシーケンスの⽐較   ## サブシーケンスで⽐較 ）４と０
print([[0,1,2], [3,4,5]] < [[0,1,2],[3,0,5],[6]]) 

## 要素数の異なるシーケンスの⽐較
print([0,1] < [0,1,2]) 
## そのほか⽐較
print(3 < (4==4)) ##丸括弧の評価により、右側が評価True(1)される
print(4 and 3 and 3)## 4and3 が先に評価。
## そのあと、3and3が評価される。戻り値は最後に評価された値。
```

### 演算⼦の優先順位

- 数値演算⼦>⽐較演算⼦>(notが⼀番⾼く、orが⼀番低い)

- 数値演算⼦>⽐較演算⼦>(notが⼀番⾼く、orが⼀番低い)

# 【第６章】モジュール

### モジュールとは

スクリプトで使ったりするファイルのこと。⻑いプログラムを書こうと思ったとき、モジュールに分割してスクリプトで使うことでより可読性が⾼くメンテナンスしやすくなる。

- ファイル名 = main.py のように接頭辞.pyをつける

- グローバル変数__name__ = モジュールの中で、モジュール名がセットされている。※約束事

- モジュールのインポート
  
  ```python
  import <module-name>
  ## モジュールから定義されている名前をすべて取り込む
  from <module-name> import *
  ## _で始まる以外のすべての名前を取り込んでくれる。まあ、あんまり使われないかも。
  ## コード内で別名で使いたい場合
  import <module-name> as name
  ## 例
  import numpy as np
  ```

- モジュールの検索パス
  
  - たとえば、smapという名前のモジュールがimportされるとき、インタプリ
    タはどこにあるか検索する。
  
  - ⾒つからなかったら、sys.pathからディレクトリのリストを使ってsmap.pyを
    検索する。
  
  - <mark>**sys.pathは以下の場所に初期化されている。**</mark>
    
    - ⼊⼒スクリプトのあるディレクトリ
    
    - PYTHONPATH
    
    - インストールごとのデフォルト

### dir()関数

- ビルドイン関数dir()は、**モジュールが定義している名前を確認するために使う**。

- 返り値は⽂字列のリストで、ソート済み。

- 引数がないときは現在のレベルで定義されている名前のリストを返す。

- 変数、モジュール関数など、すべての型の名前がリストアップされることに注
  意。

### パッケージ

- モジュールの集まり（パッケージ）という説明を以前にしました。

- かみ砕くと、「ドット区切りのモジュール名」と使って、Pythonのモジュール
  を編成する⽅法。
  
  ```python
  import A.B
  パッケージAにあるサブモジュールBを指す。
  from A.B import C
  パッケージAにあるサブモジュールBの、アイテムCを呼び出す。
  この時のアイテムはサブモジュールでも、関数、クラス、変数などでもよい。
  もちろん、パッケージで定義されたほかの名前でも。
  ```

- パッケージ内の相互参照
  
  - 絶対import
  
  - 相対import → 現在のパッケージ名や親パッケージ名を前置したドットに
    よって⽰す。カレントモジュールに基づいて⾏われる。

### コンパイル済みのPythonファイル

- Pythonはコンパイル済モジュールを `__pycache__ `ディレクトリにキャッシュ
  する。

- キャッシュ名は、module.バージョン名.pyc  **缓存名称**是<mark>module.模块名称.pyc</mark>

- バージョン名はコンパイルされたファイル形式のコードでPythonのバー
  ジョン番号を含む。 version==>版本名

# 【第７章】⼊出⼒とファイル

### ⼊出⼒

- 出⼒⽅法
  
  - 式⽂
  
  - print()
  
  - write()
  
  ※標準出⼒のファイルオブジェクトsys.stdout
  
  ```python
  text1 = "reina"
  text2 = "chan"
  print(f"kawaii{text1}{text2}")
  ## フォーマット前に変換できる
  print(f"kawaii{text1!r}{text2!s}") ## r = repr(),s = str()
  print(f"kawaii{text1!a}{text2}") ## a = ascii()
  old = 23
  print("名前は{:<8s}です。年齢は{:>3d}歳です。".format(text1, old))
  ## 位置引数、キーワード引数も使える
  print("名前は{0},年齢は{1},そして{color}".format("chika", "18", color="オレンジ"))
  num = 1 + 3
  print(str(num)) ##⼈間   ===> 结果是4
  print(repr(num))## インタプリタ ===> 结果也是4
  pai = 3.141592
  print("円周率は%f" % pai)
  ```

### ファイルの読み書き

- ファイルを開く，open関数でファイルオブジェクトを返す
  
  ```python
  f = open("sample.txt", "w")
  ## w 書き出し専⽤
  ## r 読み込み専⽤
  ## r+ 読み書き両⽅
  ## a 追加
  ## 省略された場合はr
  ## b バイナリモードで開く！byteオブジェクトで読み書きされる。
  ## テキストモードの読み込みの注意点
  ## 読み込みの際に、プラットフォーム依存の⾏末⽂字は\nと変換されるのがデフォルト。
  ## 書き込みはプラットフォームごとに戻される。
  ## JPG,EXEなどのバイナリファイルではデータ壊すので注意。
  ```

- with()
  
  - ファイルが正しく閉じられる利点があり、例外が途中で創出されても処理さ
    れる。
  
  - finallyブロックの節約になる 
    
    ```python
    with open("sample.txt") as f:
    read = f.read()
    ## 閉じているかのチェック
    f.closed
    ```

- 読み書きなどのメソッド 
  
  ```python
  f.read(サイズ)
  読み込んで、str もしくは bytesのオブジェクトとして返す。
  f.write()
  書き込む
  f.tell
  ファイルの中の現在位置を整数でかえす。
  f.seek(オフセット, 起点)
  現在位置を変えたいとき。位置は参照している点と、オフセットの和で
  算出する。
  f.readline()
  ⼀⾏読む。
  ```

- Jsonデータの取り扱い
  
  - シリアライズ  （jsonモジュールでPythonのデータ階層構造をとって⽂字列にコ
    ンバートすること）    Serialized 序列化
  
  - シリアライズの逆をデシリアライズという。
    
    ```python
    import json
     ## オブジェクトをテキストファイルにシリアライズする
    json.dumps([1, "list", "simple"])
    ) ## 書き込み⽤にオープンしてるテキストファイルがある場合、このように書け。
    json.dump(x, fる。
    ## デコードする場合
    decode = json.load(f)
    ```
    
    ![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-11-36-48-image.png)
    
    ![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-11-40-33-image.png)
    
    ![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-11-39-40-image.png)![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-11-41-15-image.png)![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-11-41-30-image.png)

# 【第８章】エラーと例外

### ★エラーの種類は構⽂エラー(syntax error)と例外(exception)★

### 構⽂エラー

- 構⽂解釈上のエラーとも呼ばれる。

- （パーサ、構⽂解釈器）は違反のある⾏を表⽰して^でさす。基本的には^の前が
  原因。

### 例外

- ⽂や構⽂が正しいときに実⾏すると検知されるエラーの総称。致命的ではない
  が、エラーメッセージに現れる。

- ⾃⾝で例外を定義することができる。

- 例外の種類
  
  ![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-11-54-37-image.png)

- 例外の処理
  
  - except節の順番に注意
  
  - except複数書くことができる！
    
    ```python
    try:
    x = int(input(""))
    except SintaxError as s: ## 例外名を省略すると、ワイルドカードにすることができる。
    print("正しく⼊⼒してください")
    except (TypeError, NameError):
    print()
    else: ## try節が例外を送出しない時
    print()
    finally: ## 例外があってもなくても最後に⾏われる処理
    print()   
    ```

- raise
  
  - 指定の例外を強制的に発⽣させることができる。
  
  - 例外の連鎖もできる。
    
    ```python
    raise NameError("エラーです！")
    ---------------------------------------------------------------------------
    NameError Traceback (most recent call last)
    ~\etc.py in <module>
    ----> 1 raise NameError("エラーです！")
    NameError: エラーです！
    raise ValueError ## 省略記
    raise RuntimeError from OSError ## 例外の連鎖
    ```

- # クリーンアップ
  
  - finally節で⾏う動作のこと。
  
  - except, else節の実⾏中に例外が発⽣した場合、finally節の実⾏後に再送出され
    る。
  
  - finally節がreturn⽂を含んでいた場合、戻り値はfinally節のreturn⽂からのものと
    なる。
  
  - ファイルごとでクリーンアップが定義されているオブジェクトはそれぞれのド
    キュメントから参照すること。
  
  - クリーンアップ処理としてよくあげられるのが、ファイルを開くときに使う
    
    ```python
    with open("sample.txt", r)
    ## ファイルを閉じる処理を書かなくていいので、クリーンアップ節の節約になる
    ## よく例として挙げられる。
    ```

# 【第９章】クラス

### クラスとは

- データと性能をひとまとまりにする⽅法。

- 新しいクラスを作ることは、新しいオブジェクト型を作ることであり、その⽅
  の新しいインスタンスを作ることを可能にする。

- クラスインスタンスはそれぞれに付属して状態を保持する属性、メソッドを持
  つことができる。

- ほかの⾔語と⽐べたPythonのクラスのメリット
  
  - クラスの継承は多重基底クラスを許容
  
  - 派⽣クラスは基底クラスのあらゆるメソッドをオーバーライド可能
  
  - メソッドは基底クラスのメソッドを同じ名前でコールできる。
  
  - オブジェクトには好きなだけデータが⼊れられる。

### クラスを使う

- 定義⽅法
  
  ```python
  class ClassName():
  <code>
  ```

- 上記のクラス定義を有効化するには、⼀度実⾏する必要がある。

- クラス定義に⼊ると新しい名前空間が作成されて、ローカルスコープとして使
  われる。そのため、ローカル変数への代⼊はすべてこの新しい名前空間に⾏われる。

- クラス定義から正常に抜けるとクラスオブジェクト(クラス定義で作られた名前
  空間の内容を包むラッパー)が作られる。

#### クラスオブジェクト

- ２種類の操作をサポートする。
  
  - obj.name という形で参照する。
    
    ```python
    obj.name という形で参照する。
    ## 例
    class MyClass():
    '''sample class'''
    i = 12345
    def func(self):
    return "aaa"
    ## iにアクセスする
    MyClass.i
    ## funcにアクセスする
    MyClass.func
    ## docにアクセスする
    MyClass.doc
    ```
  
  - インスタンス化
    
    - 関数の表記法が使われる。
      
      ```python
      class MyClass2():
      ## このように、⽣成するインスタンスが初期状態にカスタマイズし
      てあることが望ましい。
      ```python
      ## MyClass2を呼び出すと⾃動的にコールされる__init__ コンストラクタ
      ```
      
          def __init__(self):
          self.data = [] 
      
      x = MyClass2() ## 新しいインスタンスをxとして定義。
      
      ```
      
      ```

### インスタンスオブジェクト

先ほど作成したインスタンス。さて、なにができる？

- 属性参照

- 属性名として有効なもの
  
  - データ属性
  
  - メソッド → オブジェクトに「属した」関数。
    
    - たとえば、listオブジェクトのメソッドappend, removeなどなど…
    
    - 有効なメソッド名はクラスによって決まる。つまり、クラス属性のうち
      関数オブジェクトであるものはすべて対応したインスタンスのメソッド
      を定義したことになる。
      
      ```python
      ## 例
      class MyClass():
      '''sample class'''
      i = 12345
      def func(self):
      return "aaa"
      x = MyClass()
      Myclass.func ## 関数オブジェクト
      x.func ## メソッドオブジェクト
      MyClass.i ## クラスオブジェクトの属性参照
      x.i ## インスタンスオブジェクトのデータ属性
      ```

### メソッドオブジェクト

上記で出てきたメソッド。これには特殊性がある。

- 第⼀引数として、インスタンスオブジェクトが渡されることがある。
  
  ```python
  class MyClass():
  '''sample class'''
  i = 12345
  def func(self):
  return "aaa"
  x = MyClass()
  xf = x.func ## 引数なしでもコールできている。
  ## MyClassx)
  ```

### スコープと名前空間

```python
a = 100
def outer():
    b = 10
    def inner():
        nonlocal b  # 声明外部函数的局部变量
        print(r"inner b:", b)
        b = 20
        global a  # 声明全局变量
        a = 1000
        print("a ：", a)
    inner()
    print(r"outer b:", b)
outer()
print("a ：" ,a)
#结果
#inner b: 10
#a ： 1000
#outer b: 20
#a ： 1000
```

![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-13-34-08-image.png)

### 継承

```python
## 基底クラスPersonを定義
class Person:    
   def __init__(self, name):
self.name = name
def getName(self):
return self.name
## 継承クラス
class Player(Person):
def __init__(self, nm, h):
super().__init__(nm)
s
def getName(self):
return "勇者：" + self.name
def getHp(self):
return self.hp
pr = Customer("鈴⽊", 100)
nm = pr.getName()
hp = pr.getHp()
print(nm, "さん")
print("体⼒は", hp,"です")elf.hp = h
```

### 多重継承

```python
## 多重継承の例
class A():
class B():
class C(A,B): ## A,Bを継承したサブクラス 左の親クラスが優先される。
```

### イテレータ

- コンテナオブジェクト（リストや⽂字列など…）などにアクセスするときも使
  うイテレータ（反復⼦）

- 反復可能オブジェクトは、それが内包するイテレータを返す__iter__メソッドを
  持つ

- イテレータは⾃⾝を戻り値とする__iter__メソッド、次の要素を返す__next__メ
  ソッドを持つ
  
  ```python
  # 例えば以下の動きなら・・・
  for i in [1, 2, 3]:
       print(i)
  ```
1. コンテナオブジェクト(今回は数字[1, 2, 3]のリスト）にiter()をコールするように
   なっている。

2. iter()は反復可能オブジェクトを返し、それは１つずつコンテナの要素にアクセ
   スする__next__()メソッドが定義してある。

3. つまり、__next___()メソッドが今回使⽤するリストに１つずつアクセスして、
   printしている。

4. アクセスできる要素が尽きると、StopIteration例外を送出→forは確認したら終了
   する。

5. また、__next__()はビルドイン関数next()でコールできる。例のコードをnext()
   でやってみる。
   
   ```python
   list1 = [1, 2, 3]
   it = iter(list1)
   print(next(it)) # 1
   print(next(it)) # 2
   print(next(it)) # 3
   ```
   
   ```python
   rangeについて  #这个不能使用
   r = range(3)
   print(next(r))
   ## 上記のことから、rangeは反復可能ではあるがイテレータではないことがわかる。
   ```

### ジェネレータ generator   发生器

- イテレータ（反復⼦）を作るためのツール。

- データを返す部分でyieldをというものを使う。
  
  ```python
  list1 = [1, 2, 3]
  reverse(list1):
  for i in range(list1):
  yield list1[i]
  ```

- ジェネレータでできること
  
  ```python
  ・__iter__(), __next__()の両メソッドが⾃動的に⽣成される。
  ・ローカル変数と実⾏状態が、コール間で⾃動保存されていること
  ・ジェネレータ終了時に⾃動的にStopIterationを送出する。。
  ```

- ジェネレータ式
  
  - ジェネレータを作成する式のこと。
  
  - イテレータを作成するジェネレータを式化したもの。
    
    ```python
    j = sum(i*i for i in range(10))
    ## これをforで取り出してみる。
    for i in j:
    print(j)   ====>报错
    ```

# 【第１０章】標準ライブラリ

### 標準ライブラリ⼀覧表

![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-13-53-29-image.png)

![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-13-53-50-image.png)

# 【第１１章】仮想環境とパッケージ

### 仮想環境とは

- 例えば、⾃分でプログラム作るときにAという部分はPython2.0, Bという部分は
  python3などバージョンを複数持って使いたいときがある。そのときに仮想環境を使う。
  
  - 作成⽅法  venv
  
  - 利⽤可能なもっとも新しいバージョンのPythonのインストール。
    
    ```python
    ## sample-envというディレクトリを作り、
    ## その中にディレクトリツリーを作成する。
    python3 -m venv sample-env
    ## ディレクトリは.venv（隠しディレクトリ）
    ```
  
  - 仮想環境の有効化
    
    ```python
    sample-env/Scripts/activate.bat
    source sample-env/bin/activate
    ```
  
  - 仮想環境を有効化すると、シェル・プロンプトが使⽤中の仮想環境を⽰すも
    のに変更する。また、pythonと⼊⼒したときに指定のバージョンのインス
    トール⾃体が実⾏されるように環境が改変される。

- pip によるパッケージ管理
  
  パッケージの操作をpipというプログラムを使う。
  
  ![](C:\Users\students\Desktop\我的学习笔记\img\2023-02-14-14-02-15-image.png)

# 【第１２章】浮動⼩数点

表現誤差

```python
print(0.3 == 0.1 + 0.1 + 0.1)
```

上記のコードがなぜFalseになるのか？

**それは、Pythonでは１０進数の分数には２進数の分数で正しく表現できない表現誤
差、という事実があるから。 **

```python
## decimal を使って1/10の正しい値を出してみると・・・
from decimal import Decimal as d
print(d.from_float(1/10)
```

そのため、コンピュータが１０進数の分数を２進数で精密に正しく知覚することが
難しい。あくまで、近似値としてあつかっているに近い。というよりかは、とても⻑い数字の羅列は丸めて表⽰されていることがほとんどである。
