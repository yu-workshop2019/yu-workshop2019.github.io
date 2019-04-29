

# 山口大学工学部 ワークショップ 2019  解説資料


---

## 第7章 その他の情報

本章では、Raspberry Piで何かデバイスを作るときに知っておくと便利な情報を掲載している。

---

### 1.シェルスクリプト

キーボードで毎回ターミナルにコマンドを入力する代わりに、入力したいコマンドをファイルに書いておいて、そのファイルを実行させると便利である。  
これは特に、コマンドが長く複雑なときや、コマンドがいくつもあるようなとき、また、同じコマンドをたびたび実行する必要があるときなどに便利である。  
そのようなファイルのことを「シェルスクリプト」という。シェルスクリプトは拡張子が`.sh`である。シェルスクリプトはプログラミング言語の一種であるといえる。

簡単な例を通してシェルスクリプトの振る舞いについて理解しよう。  
まず、ターミナル上で以下のコマンドを実行する。

`$date >> /home/pi/date.txt`

`/home/pi/date.txt`が生成されている。`date.txt`を開いて内容を確認する。

`cat /home/pi/date.txt`

実行した日付時刻が記録されているはずである。  
このことから、`$date >> /home/pi/date.txt`は、`/home/pi`以下に、実行時点の日付時刻が記録された`date.txt`というテキストファイルを生成するコマンドであることが分かる。

次に、シェルスクリプトで同じことをやってみよう。`record_date.sh`を作成する。

`$sudo nano /home/pi/record_date.sh`

`record_date.sh`には以下の内容を記述する。

```
#!/bin/bash
date >> /home/pi/date.txt
```
入力を終えたら保存し、nanoを終了する。

シェルスクリプトに書く内容は、ターミナル上に入力する内容と同じである。コマンドをどこに入力するかの違いでしかない。シェルスクリプトには、複数のコマンドを記述しておくこともできる。コマンドは一行に1つ記述する。コマンドは上から順に実行される。

シェルスクリプトを実行する前に、実行権限を付与しておく。

`$sudo chmod a+x /home/pi/record_date.sh`  
`$sudo chmod a+w /home/pi/date.txt`  

`record_date.sh`を実行する。

`$./record_date.sh`

`date.txt`を確認してみよう。

`cat /home/pi/date.txt`

---

### 2.プログラムの自動起動(/etc/rc.local)

---

### 3.プログラムの一定間隔での実行(cron)  

---

### 4.IPアドレスの固定(/etc/dhcpcd.conf)

---

### 5.SSHによるリモートログイン、SFTPによるファイル転送

---

### 6.RDPによるリモートデスクトップ接続(xrdp)

---


[前の章へ](https://yu-workshop2019.github.io/chapter_6/chapter_6)


[次の章へ](https://yu-workshop2019.github.io/chapter_8/chapter_8)


[目次へ](https://yu-workshop2019.github.io/manual)


[トップページへ](https://yu-workshop2019.github.io/)
