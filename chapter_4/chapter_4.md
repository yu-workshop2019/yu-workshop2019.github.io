# 山口大学工学部 ワークショップ 2019  解説資料


---

## 第4章 プログラミング言語Python(パイソン)を使う

---


### 1. プログラミングとプログラミング言語

人間がコンピュータにさまざまな仕事をさせたいときに、そのための指令を書き記したものをプログラムという（コード・ソース・ソースコードなどともいう）。
また、プログラムをすること（＝コンピュータに与えるための指令を組み立てること）をプログラミングという。
Raspberry Piもコンピュータの一つであるから、プログラミングという方法を知っていると、Raspberry Piをより効率よく、より高度に扱うことができる。

プログラミングのために用いる言語をプログラミング言語という。日本人同士が意思疎通するときには日本語を用いる。
コンピュータと意思疎通しようとするときにはプログラミング言語で会話しなければならない。
プログラミング言語には多くの種類があり、それらの言語には、ある目的に対して得意不得意があるので、適切なものを選択して用いる必要がある。

ここでは、Raspberry Piと相性が良く、比較的記述が簡単で、Web上にサンプルが豊富であるなどの理由から、Python(パイソン)というプログラミング言語を用いる。

---

### 2.Pythonに関する基本的事項

Raspberry PiはPythonとの相性が良く、Raspbianには標準でPythonの実行環境が用意されている。
従って、Raspberry PiでPythonを使おうとするときには、ただプログラムを書きさえすればよい。

Pythonは簡潔な記述を特長とする理解しやすい言語であるが、「インデント」を重視するという独特な作法があるので注意が必要である。
インデントとは段落のことで、キーボードのTabキーを押すことで挿入されるいくつか（たいていは4つ）の空白である。
Pythonでは、プログラム内での意味上の区切りを、インデントの増減によって表す（カッコで表す言語もある）。
これは、インデントによって誰でも自然に美しいプログラムが書けるようにという設計思想である。
Pythonプログラムが意図したとおりに動かないときには、インデントが崩れている可能性も考えられる。

---

### 参考:WindowsでのPythonの実行

Raspbianの場合と異なり、Windows上でPythonプログラムを実行するには、実行環境を整える必要がある。
WindowsでPythonの実行環境を整えるには、[anaconda](https://www.anaconda.com/distribution/)を用いるのが便利である。

---

### 参考:エディタgedit

Raspberry Pi上でプログラムを編集するには、geditと呼ばれるエディタが便利である。

geditのインストール

`$sudo apt-get install gedit`

hogehoge.pyをgeditで開く

`$gedit /home/pi/hogehoge.py`

---


### 3. Hello, world!

まずは簡単なPythonプログラムを動かしてみよう。
以下のサイトから、最も基本的なPythonのプログラムをダウンロードする。  
[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/hello.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/hello.py)  
Pythonプログラムは、拡張子が`.py`で表される。メモ帳などのエディタで開いて編集することができる。

次の手順に従い、Raspberry Pi上で`hello.py`を実行する。  
1. `hello.py`を`/home/pi`にコピーする。  
2. ターミナルを立ち上げる。  
3. `hello.py`を実行する。  
`$python hello.py`  

以下、Pythonプログラムを実行するときはこのようにする。また、Pythonプログラムは`/home/pi`に置くこととする。

`hello.py`は、3行の簡単なプログラムである。  

hello.py
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

print "Hello, world!"
```

ここで、`hello.py`の1行目と2行目の部分
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-
```
は、pythonプログラムを動かすときの「おまじない」のような記述であるので、ここではこの記述について深く考える必要はない。
従って、`hello.py`は、実質的に以下のたった1行からなるプログラムだと考えてよい。
```
print "Hello, world!"
```
これはPythonプログラムのもっとも単純なかたちと言える。文字列を画面に出力させたいときには、このように記述する。
`""`の中の文字列を変更して実行すると、実行結果も変化することを確認してみよう。

---

### 4.if文

プログラムの中で、ある条件に合致しているかどうかによって、処理を分岐させたいことがある。このような処理を「条件分岐」という。
Pythonでこれを実現するには、if文を用いる方法がある。  
Pythonでif文を用いた例をダウンロードする。  
[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/if.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/if.py)  

if.py
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

number = 1
#number = 2
print("numberには" + str(number) + "が代入されています")

if (number == 1):
    print("数字は1です")
else:
    print("数字は1ではありません")
```

`if.py`では、変数`number`に代入された数字が１であるかを判定し、その結果によって、出力する処理を分岐させている。
具体的には、変数`number`に代入された数字が１であるならば、`数字は1です`と出力され、そうでないならば、`数字は1ではありません`と出力される。  
Pythonには「コメントアウト」と呼ばれる機能があり、行頭に`#`が付された行は実行されない（無視される）。
したがって、`if.py`の5行目にある`number=2`は無視されている。
ここで、5行目の`number=2`のコメントアウトを外す(`#`を取り去る)と、この行の記述が有効になり、変数`number`には2が代入される。  
`number=1`と`number=2`の各場合について、実行結果を確認し、違いを見つけよう。

---

### 5.for文

プログラムの中で、ある処理を何度も繰り返し実行させたいことがある。このような処理を「繰り返し」とか「反復」などという。
ある処理を100回実行させたいときに、その処理を100回記述するのは非常に非効率である。
Pythonで効率的にこれを実現するには、for文を用いる方法がある。  
Pythonでfor文を用いた例をダウンロードする。  
[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/for.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/for.py)  

for.py
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

for i in range(0, 100):
    print(str(i))
```

`for.py`は、for文を用いた簡単なプログラムである。for文の内部で、変数`i`には0から99(100-1)までの数字が1ずつ増加され、次々に代入されていく。
for文の繰り返しのことを「ループ」と呼ぶ。ループ内で変数`i`を表示させ、結果を確認している。
for文内の`(0,100)`の数字を適当に変更して実行し、結果を確認しよう。

また、1から100の数字の和を求めるプログラムを作ってみよう。解答例は以下。  
[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/sum.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/sum.py)  

---

### 6.if文とfor文の合わせ技

if文とfor文を組み合わせると、以下のようなこともできる。

[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/if_for.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/if_for.py)  

if_for.py
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

for i in range(1, 100):
    if (i % 3 == 0):
        print(str(i) + "は3の倍数です")
```
`if_for.py`は、1から99の数字の中で3の倍数であるものだけを表示するプログラムである。for文の中でif文を用いて、各数字が3の倍数であるかを判定している。  
if文内の記号`%`は、剰余を求める演算子である。この場合、「変数`i`に代入されている数字を3で割った余りが0である」場合、すなわち、変数`i`が3の倍数である場合には、`3は3の倍数です`のように表示される。

---

### 7.ファイル出力

プログラムで計算した結果などは、プログラムを終了させると失われてしまう。
計算結果や測定結果などをテキストファイルに出力（保存）するためには以下のようにする。

[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/output.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/output.py)  

output.py
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

filename = "output.txt"

text = 'あいうえお'

with open(filename, mode='a') as f:
    f.write(text)
```

`output.py`では、変数`text`に代入された文字列`あいうえお`を、変数`filename`に指定されたファイル名`output.txt`に出力している。  
`output.py`を実行すると、`/home/pi/output.txt`という新しいファイルが生成されているはずである。適当なエディタで`output.txt`を開いて中身を見てみよう。

以下のようにすると、複数行からなるテキストファイルを出力することもできる。
[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/output_for.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/output_for.py)  

output_for.py
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

filename = "output_for.txt"

with open(filename, mode='a') as f:
    for i in range(0, 100):
        f.write(str(i) + "\n")
```

ここで、`\n`は改行することを表す。`output_for.txt`を開いて中身を確認してみよう。

---

### 8. FizzBuzz

ここまでのことを理解したら、プログラミングの問題で有名な「FizzBuzz」を作ってみよう。  
FizzBuzzは、条件分岐、反復、画面出力など、プログラミングの基本的な技法を駆使して作られるため、その言語を理解しているかを知るにはもってこいである。  
FizzBuzzとは、次のような条件を満たすプログラムのことである。

1.1から100までの数字を画面に出力する  
2.ただし、その数字が3で割り切れるならば、数字の代わりに"Fizz"と出力する  
3.また、その数字が5で割り切れるならば、数字の代わりに"Buzz"と出力する  
4.また、その数字が3と5のどちらでも割り切れる（すなわち、その数字が15で割り切れる）ならば、数字の代わりに"FizzBuzz"と出力する

すなわち、FizzBuzzのプログラムの出力結果（の一部）は次のようになる。

```
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
16

(以下続く...)
```

解凍例は以下。  
[https://ja.wikipedia.org/wiki/Fizz_Buzz](https://ja.wikipedia.org/wiki/Fizz_Buzz)

---

### 9.関数

Pythonで関数を使用するためには以下のようにする。

[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/func.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/func.py)

プログラムを実行してみよう。

func.py
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

def func():
    print("funcを実行しました。")

def pow(x):
    print("powを実行しました。")
    return(x * x)

def rand():
    import random
    print("randを実行しました。")
    a = random.randint(0, 9)
    b = random.randint(0, 9)
    return (a, b)

def main():
    print("mainを実行しました。")

    #funcの実行
    func()

    #powの実行
    x = 5
    print(str(x) + "の2乗は" + str(pow(x)) + "です。")

    #randの実行
    a, b = rand()
    print("2つの乱数は、" + str(a) + "と" +  str(b) + "です。")

#プログラム実行時に実行される部分
if __name__ == '__main__':
    print("まずここが実行されます。")
    main()
```

Pythonは動的型付け（変数に代入された内容から、自動的に変数の型を類推する）に対応した言語であるので、C言語などと異なり、関数に戻り値の型などを明記する必要はない。関数の内部はインデントで字下げする必要があることに注意。

`func.py`は、文字を表示するだけの関数`func()`、引数として受け取った自然数の二乗を返す関数`pow()`、0～9の範囲の整数の乱数を2つ返す関数`rand()`、これらの関数を呼び出す関数`main()`からなる。関数`rand()`に注目するとわかるように、Pythonでは複数の戻り値を返すことができる。もちろん、複数の引数を渡すこともできる。

特徴的なのは、33行目の`if __name__ == '__main__':`という見慣れない記述である。  
Pythonでは、自作のプログラムを「モジュール」として他のプログラムから使用することができる。たとえば、このプログラム`func.py`を、他のプログラム内で、

```
import func
a = func.pow(4)
```

などのようにインポートすることができる。この場合、変数`a`には、`func.py`の関数である`pow()`に引数として4が渡された結果である16が代入される。

ここで、`func.py`が、1.直接(`$python ./func.py`などのように)実行された場合 と、2.他のプログラムからモジュールとしてインポートされた場合　の2パターンについて、それぞれ異なる挙動をさせたい場合を考える。  
1.の場合のように、`func.py`が直接実行された場合には、まず`if __name__ == '__main__':`以下の部分が実行される。したがって、1.の場合に実行したい処理は、`if __name__ == '__main__':`部分に記述しておけばよい。`func.py`では、`if __name__ == '__main__':`部分で関数`main()`を呼び出し、関数`main()`内で、それぞれの関数を呼び出している。  
一方、2.の場合では`if __name__ == '__main__':`は実行されない。

`func.py`をインポートして、`func.py`内の関数を呼び出すようなPythonプログラムを作ってみよう。

回答例は以下。

[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/call_func.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/call_func.py)

---

### 参考:Pythonの学習方法

Python（に限らず多くのプログラミング言語）には数えきれないほどの文法や規則があり、そのすべてを短期間で理解し使いこなすことは容易ではない。
Pythonを徐々に習得するには、実現したいことや疑問に思うことが出るたびに、面倒くさがらずこまめに他人に質問したり、Webで検索したり、Python関連の書籍を読んだりして解決することが重要である。  
また、Pythonは非常に人気の言語であるため、Web上で多くの人が様々な応用例を公開している。自分がやりたいことと似たサンプルプログラムを発見したら、それをまねて、あるいはそれをベースにしてアレンジを加えるというのも効率的な手法である。  
Pythonには、例として画像の取り扱いやWebのスクレイピングなど、特定の分野のプログラミングをより効率的にするために、よく使うであろう機能をあらかじめまとめた「ライブラリ」と呼ばれる仕組みがある。ライブラリを用いると、自分でゼロからプログラミングするよりも、ずっと効率的に目的を達成することができる。既存のライブラリは先人の努力の賜物であるので、最大限活用させてもらおう（[車輪の再発明](https://ja.wikipedia.org/wiki/%E8%BB%8A%E8%BC%AA%E3%81%AE%E5%86%8D%E7%99%BA%E6%98%8E)を防ぐ）。


[前の章へ](https://yu-workshop2019.github.io/chapter_3/chapter_3)


[次の章へ](https://yu-workshop2019.github.io/chapter_5/chapter_5)


[目次へ](https://yu-workshop2019.github.io/manual)


[トップページへ](https://yu-workshop2019.github.io/)
