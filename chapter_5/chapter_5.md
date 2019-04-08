
# 山口大学工学部 ワークショップ 2019  解説資料


---

## 第5章 さまざまな電子部品の接続

---


### 1. Raspberry Piに様々な電子部品を接続する
第3章では、Raspberry PiにLEDを接続して点灯/消灯を制御した。この他にも、モータ・センサなどのような様々な電子部品をRaspberry Piに接続して制御すると、ソフトウェアだけでは実現できない様々なデバイスを製作することが可能になる。  
本章では、さまざまな電子部品とその使用例を簡潔に紹介し、自分が実現したいデバイスを製作するためのヒントとなることを目的とする。

---

### 2.LEDの点滅を制御

第3章では、Raspberry PiにLEDを接続して点灯/消灯を制御した。これをプログラムによって制御したい。

---

### 3.温度・湿度・気圧センサ BME280

Raspberry PiはPythonとの相性が良く、Raspbianには標準でPythonの実行環境が用意されている。

---


### 4. サーボモータ SG-90

まずは簡単なPythonプログラムを動かしてみよう。
以下のサイトから、最も基本的なPythonのプログラムをダウンロードする。  
[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/hello.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/hello.py)  
Pythonプログラムは、拡張子が`.py`で表される。メモ帳などのエディタで開いて編集することができる。

次の手順に従い、Raspberry Pi上で`hello.py`を実行する。  
1. `hello.py`を`/home/pi`にコピーする。  
2. ターミナルを立ち上げる。  
3. `hello.py`を実行する。  
`$python hello.py`  

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

### 5.USBカメラ C270

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

### 6.for文

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

### 7.if文とfor文の合わせ技

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

### 8.ファイル出力

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

### 参考:Pythonの学習方法

Python（に限らず多くのプログラミング言語）には数えきれないほどの文法や規則があり、そのすべてを短期間で理解し使いこなすことは容易ではない。
Pythonを徐々に習得するには、実現したいことや疑問に思うことが出るたびに、面倒くさがらずこまめに他人に質問したり、Webで検索したり、Python関連の書籍を読んだりして解決することが重要である。  
また、Pythonは非常に人気の言語であるため、Web上で多くの人が様々な応用例を公開している。自分がやりたいことと似たサンプルプログラムを発見したら、それをまねて、あるいはそれをベースにしてアレンジを加えるというのも効率的な手法である。  
Pythonには、例として画像の取り扱いやWebのスクレイピングなど、特定の分野のプログラミングをより効率的にするために、よく使うであろう機能をあらかじめまとめた「ライブラリ」と呼ばれる仕組みがある。ライブラリを用いると、自分でゼロからプログラミングするよりも、ずっと効率的に目的を達成することができる。既存のライブラリは先人の努力の賜物であるので、最大限活用させてもらおう（車輪の再発明を防ぐ）。


[前の章へ](https://yu-workshop2019.github.io/chapter_3/chapter_3)


[次の章へ](https://yu-workshop2019.github.io/chapter_5/chapter_5)


[目次へ](https://yu-workshop2019.github.io/manual)


[トップページへ](https://yu-workshop2019.github.io/)