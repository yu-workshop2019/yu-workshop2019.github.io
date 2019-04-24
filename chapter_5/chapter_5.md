
# 山口大学工学部 ワークショップ 2019  解説資料


---

## 第5章 さまざまな電子部品の接続

---


### 1. Raspberry Piに様々な電子部品を接続する
第3章では、Raspberry PiにLEDを接続して点灯/消灯を制御した。この他にも、モータ・センサなどのような様々な電子部品をRaspberry Piに接続して制御すると、ソフトウェアだけでは実現できない様々なデバイスを製作することが可能になる。  
本章では、さまざまな電子部品とその使用例を簡潔に紹介し、自分が実現したいデバイスを製作するためのヒントとなることを目的とする。
以下の項目の中で興味をひかれたものを試してみよう。

---

### 2.LEDの点滅を制御

第3章では、Raspberry PiにLEDを接続して点灯/消灯を制御した。これをプログラムによって制御したい。
[第3章](https://yu-workshop2019.github.io/chapter_3/chapter_3)で作ったLEDの回路を用いる。

![LED](http://akizukidenshi.com/img/goods/L/I-11656.jpg)

1.WiringPi-Pythonのインストール  
ターミナル上で以下のコマンドを実行し、PythonでRaspberry PiのGPIOを制御するためのライブラリを導入する。
（大変長いので、Raspberry Pi上のブラウザでこのページを表示させ、ターミナルにコピペすることを推奨）

`$sudo apt-get update`  
`$sudo apt-get install git`  
`$git config --global http.proxy http://proxy.cc.yamaguchi-u.ac.jp:8080`  
`$git config --global https.proxy http://proxy.cc.yamaguchi-u.ac.jp:8080`  
`$sudo rm -rf WiringPi-Python`  
`$sudo apt-get install python-dev python-setuptools swig`  
`$git clone --recursive https://github.com/WiringPi/WiringPi-Python.git`  
`$cd WiringPi-Python/WiringPi`  
`$sudo ./build`  
`$cd ..`  
`$swig -python wiringpi.i`  
`$ sudo python setup.py install`  
`$sudo python3 setup.py install`  

2.LEDを点滅させるためのPythonプログラムをダウンロード

以下のページから、LEDを点滅させるためのPythonプログラムをダウンロードし、`/home/pi`にコピーする。
[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/lchica.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/lchica.py)

3.実行権限の追加

`$cd`  
`$sudo chmod +x ./lchika.py`  

4.プログラムの実行

WiringPi-Pythonを使用したPythonプログラムは、管理者権限(sudo)で実行する。  

`$sudo python ./lchika.py`  

5.プログラムの改良

点滅速度や点滅の割合を変更するとどうなるか確認してみよう。
また、LEDのON/OFFだけでなく、明るさを変更するにはどうすればよいか考え、実験してみよう。

---

### 3.温度・湿度・気圧センサ BME280

温度・湿度・気圧を1台で測定できるセンサ、BME280を用いて、Raspberry Piをデジタル百葉箱にしてみよう。

![BME280](http://akizukidenshi.com/img/goods/L/K-09421.jpg)

1.BME280のはんだ付け
BME280にピンヘッダをはんだ付けする。また、<u>J3と書かれた部分の金属面にもはんだを盛る。</u>
BME280のデータシートは以下。  
[http://akizukidenshi.com/download/ds/akizuki/AE-BME280_manu_v1.1.pdf](http://akizukidenshi.com/download/ds/akizuki/AE-BME280_manu_v1.1.pdf)

2.BME280とRaspberry Piの配線
ジャンプワイヤを用いて、以下のようにRaspberry PiとBME280を接続する。配線を間違えないよう注意。
Raspberry Piのピン配置については以下のサイトのいずれかを参照。  

[RaspberryPi2のPin配置](http://www.ic.daito.ac.jp/~mizutani/raspi/raspi_pins.html)  
[ツール・ラボ 第22回 Raspberry PiのGPIO概要](https://tool-lab.com/make/raspberrypi-startup-22)  
[ラズパイの出力電圧を確認してみた](https://qiita.com/takeru56/items/985ae67f97def2218208)  


3.Raspberry PiでI2Cの使用を許可
BME280は、I2C（アイツーシ－）と呼ばれる通信規格でデータをRaspberry Piに送信する。
Raspberry PiでI2Cが使用できるように設定を変更する。
raspi-configの"Advanced Option"にある。

`$sudo raspi-config`

4.I2C用のライブラリをインストール
PythonでI2Cを使用するためのライブラリをインストールする。ターミナルで以下のコマンドを実行。

`$sudo apt-get install i2c-tools`  
`$sudo apt-get python-smbus`  

5.BME280が認識されているかの確認  

ターミナルで以下のコマンドを実行。

`$sudo i2cdetect -y 1`  

BME280が正しく接続され、Raspberry Piから認識されているならば、"76"などの数字が表示される。
そうでない場合には、もう一度配線を確認してみる。

6.サンプルプログラムの入手
SWITCH SCIENCE という会社が公開してくれている、BME280から気温・湿度・気圧を取得して表示するプログラムを以下のページからダウンロードし、`/home/pi`にコピーする。  
[https://github.com/SWITCHSCIENCE/BME280/blob/master/Python27/bme280_sample.py](https://github.com/SWITCHSCIENCE/BME280/blob/master/Python27/bme280_sample.py)  

7.実行権限の追加

`$cd`  
`$sudo chmod +x ./bme280_sample.py`  


8.サンプルプログラムの実行

ターミナル上で以下のコマンドを実行。気温・湿度・気圧が表示されるはず。

`$sudo python /home/pi/bme280_sample.py`

センサ部分に息を吹きかけたりすると気温や湿度が変化するのがわかる。

9.連続的な値の取得とファイルへの出力

BME280から連続して値を取得し、Raspberry PiのmicroSDカードに書き込むように変更する。  
以下のサイトからプログラムをダウンロードし、`/home/pi`にコピーする。  
[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/bme280.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/bme280.py)

10.実行権限の追加と実行

`$cd`  
`$sudo chmod +x ./bme280.py`  
`$sudo python ./bme280.py`

停止するときにはターミナル上で`Ctrl+C`を押す。

`/home/pi`に、ファイル名に日付を含み、拡張子が`.csv`であるファイルができているはず。
これをExcelなどで開いてみよう。1秒ごとの温度・湿度・気圧が記録されている。
グラフなどを作成してみると、一日の気温・湿度・気圧の変化が視覚的に確認しやすい。

11.pyhonで簡易Webサーバを構築し、リアルタイムでデータを閲覧

---


### 4. サーボモータ SG-90

![SG-90](http://akizukidenshi.com/img/goods/C/M-08761.jpg)

---


### 5.USBカメラ C270で画像を取得

![C270](https://images-na.ssl-images-amazon.com/images/I/51hbFkBQtqL._SX355_.jpg)

1.Raspberry PiとC270の接続

Raspberry PiのUSBポートにC270を接続する。

2.認識されたかの確認

ターミナル上で以下のコマンドを実行。

`$lsusb`

Raspberry PiのUSBポートに接続されたデバイスの一覧が表示される。  
C270が認識されていれば、`logitech USB Camera`などの表示が見つかるはず。

3.OpenCVのインストール

Pythonなどから画像を取り扱うためのライブラリであるOpenCVをインストールする。  
ターミナル上で以下のコマンドを実行。

`$sudo apt-get install libopencv-dev python-opencv`  

このコマンドの実行が完了するにはしばらく時間がかかることがある。

4.USBカメラから画像を取得するPythonプログラムのダウンロード

以下のサイトから、USBカメラから画像を取得するPythonプログラムをダウンロードし、`/home/pi`にコピーする。
[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/get_image.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/get_image.py)

5.実行権限の追加

`$cd`  
`$sudo chmod +x ./get_image.py`  


6.サンプルプログラムの実行

ターミナル上で以下のコマンドを実行。`/home/pi`以下に画像ファイルが保存されているはず。

`$python /home/pi/get_image.py`

7.ストリーム（映像）の取得

同様にして、USBカメラからストリーム（映像）を取得し、画面上に表示してみる。

以下のサイトから、USBカメラからストリームを取得・表示するPythonプログラムをダウンロードし、`/home/pi`にコピーする。  
[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/stream.py](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/stream.py)

8.実行権限の追加と実行

`$cd`  
`$sudo chmod +x ./stream.py`  
`$python ./stream.py`

USBカメラから取得した映像が表示されたウィンドウが画面上に現れる。

OpenCVを用いると、取得したこれらの画像・映像に加工を加えたりすることもできる。

---


### 6.USBカメラ C270とmjpg-streamerでライブカメラ

![C270](https://images-na.ssl-images-amazon.com/images/I/51hbFkBQtqL._SX355_.jpg)

1.Raspberry PiとC270の接続

Raspberry PiのUSBポートにC270を接続する。

2.認識されたかの確認

ターミナル上で以下のコマンドを実行。

`$lsusb`

Raspberry PiのUSBポートに接続されたデバイスの一覧が表示される。  
C270が認識されていれば、`logitech USB Camera`などの表示が見つかるはず。

3.mjpg-streamerのインストール

Raspberry Piでライブカメラを実現するためのソフトである、mjpg-streamerをインストールする。  
（大変長いので、Raspberry Pi上のブラウザでこのページを表示させ、ターミナルにコピペすることを推奨）

`$sudo rm -rf /opt/mjpg-streamer`  
`$rm -rf mjpg-streamer`  
`$sudo apt-get update`  
`$sudo apt-get install git`  
`$git config --global http.proxy http://proxy.cc.yamaguchi-u.ac.jp:8080`  
`$git config --global https.proxy http://proxy.cc.yamaguchi-u.ac.jp:8080`  
`$sudo apt-get install libjpeg8-dev cmake`  
`$ git clone https://github.com/jacksonliam/mjpg-streamer.git`  
`$cd mjpg-streamer/mjpg-streamer-experimental`  
`$make`  
`$cd`  
`$sudo mv mjpg-streamer/mjpg-streamer-experimental /opt/mjpg-streamer` 

4.mjpg-streamer起動用スクリプトのダウンロード・配置

mjpg-streamerを起動させるためのシェルスクリプトを以下のページからダウンロードし、`/home/pi`にコピーする。

[https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/mjpg-streamer_start.sh](https://github.com/yu-workshop2019/yu-workshop2019_docs/blob/master/mjpg-streamer_start.sh)

5.Raspberry Piとルータの接続

Raspberry Piをyu-netなどから切り離す。 
LANケーブルを用いて、Raspberry Piとルータを接続する。Raspberry PiのLANポート部分にある緑色およびオレンジ色のLEDがついていることを確認する。

6.Raspberry PiのIPアドレスの確認

ターミナル上で以下のコマンドを実行。

`$ip a | grep eth0`

記号`|`は、`Shift+\`で入力できる。

`inet 192.168.0.5/24`などの表示が出るはず。この数字（IPアドレス）は、例えば`192.168.0.10`のように、多少異なってもよい。この番号（IPアドレス）を覚えておく。

7.実行権限の追加と実行

ターミナル上で以下のコマンドを実行。mjpg-streamerが起動する。

`$cd`  
`$sudo chmod +x ./mjpg-streamer_start.sh`  
`$./mjpg-streamer_start.sh`  

8.PCやスマホをネットワークに接続

Raspberry Piを接続したルータに、手持ちのPCやスマホを接続する。有線/無線どちらでもよい。

9.PCやスマホからのライブ映像視聴

PCやスマホのブラウザから、6.で調べた番号（IPアドレス）の9000番ポートにアクセスする。  
例えば、番号が`192.168.0.5`であった場合、ブラウザのURL入力欄に以下のように入力する。

`http://192.168.0.5:9000/`

mjpg-streamerからのストリーミング映像がブラウザに表示される。

8.mjpg-streamerのストリームをOpenCVで処理

---

### 7.WebIOPiで、Raspberry Piに接続された電子部品をPCやスマホから制御

---

### 8. JTalkで音声合成し、Raspberry Piを初音ミクの声で喋らせる

---









[前の章へ](https://yu-workshop2019.github.io/chapter_3/chapter_3)


[次の章へ](https://yu-workshop2019.github.io/chapter_5/chapter_5)


[目次へ](https://yu-workshop2019.github.io/manual)


[トップページへ](https://yu-workshop2019.github.io/)
