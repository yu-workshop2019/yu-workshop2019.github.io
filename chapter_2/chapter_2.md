# 山口大学工学部 ワークショップ 2019  解説資料


---

## 第2章 Raspberry Piのセットアップと初期設定

---


### 1. 開発環境

本資料は、以下の環境で開発されることを想定している。

- Raspberry Pi3 Model B

- ノートPCのOS：Microsoft Windows10

- Raspberry PiのOS：Raspbian Stretch

---

### 2. ノートPCの準備

ノートPCに以下のソフトをダウンロード・インストールする。

- [Win32 Disk Imager](https://forest.watch.impress.co.jp/docs/review/1067836.html)

  - SDカードにRaspbianOSを書き込んだり、バックアップしたりするためのソフト。

- [Tera Term](https://forest.watch.impress.co.jp/library/software/utf8teraterm/)

  - ノートPCからRaspberry PiにSSHログインするためのソフト。

- [WinSCP](https://forest.watch.impress.co.jp/library/software/winscp/)  
  
  - ノートPCからRaspberry Piにファイル転送するためのソフト。  
      
---

### 3. Raspbian OSイメージのmicroSDカードへの書き込み

Raspberry Piでは、microSDカードにOSを書き込んで使用する。

1. [Raspberry Pi財団の公式サイト](https://www.raspberrypi.org/downloads/raspbian/)から、Raspbianのイメージファイル（サイズ大）を
ノートPCにダウンロード・解凍する。  
2. 以下のページを参考にし、Win32 Disk Imagerを用いてmicroSDカードにRaspbian OSイメージを書き込む。  
[第57回「改めましてラズベリーパイの基本！(2) Raspberry Pi イメージファイルのインストール＆バックアップ 2017年度版」](https://deviceplus.jp/hobby/raspberrypi_entry_057/)

---

### 4. Raspberry Piの起動

いよいよRaspberry Piを起動する。

1. Raspbian OSを書き込んだmicroSDカードをRaspberry Piにセットする。  
1. Raspberry Piに以下のデバイスを接続する。  
  - ディスプレイ（HDMI）
  - キーボード（USB）
  - マウス（USB）  
1. Raspberry Piの電源端子（microUSBコネクタ）にACアダプタを接続する。この時点でRaspberry Piが起動する。  
1. 画面に意味不明な文字の羅列が表示されるのを眺める。  

---

### 5.初期設定

初めてRaspberry Piを使う前に、各種初期設定を行う。

1. ターミナルを立ち上げる。デスクトップ画面左上の黒いアイコンをクリック。  
1. 文字だけが表示された黒い画面が現れる。Linuxではこの画面で作業することが多い。  
1. ターミナルにコマンドを入力する。以下、コマンドには文頭に`$`をつけ、`$hogehoge`のようにあらわす。
ただし、`$`自体は入力しない。コマンドを入力し終えたらEnterキーを押す。  
`$sudo raspi-config`
1. ファイルシステムを拡張する。  
1. ロケール・キーボードレイアウト・Wi-Fiカントリーなどを設定する。  
1. 設定を終えたら再起動して変更を反映させる。今後、同様に何かシステム設定を変更したときには、変更を反映させるために再起動する。  
`$sudo reboot`

---

### 参考:ターミナルについて

- 実行したいコマンドの一部を入力した状態でTabキーを押すと、予想される候補が表示される。これを利用することで、効率的にコマンドが入力できる。

- 十字キーの上下で、過去に入力したコマンドを呼び出すことができる。これも効率的な入力には便利。

- `$history`で、過去に入力したコマンドの履歴を見ることができる。

- `Ctrl + Alt + T`で、ターミナルの窓を増やせる。いくつもの処理を並行して行わせたいときに便利。

---

### 参考:エディタ"nano"について

- Raspbian(Linux)では、OSの設定を設定ファイルと呼ばれるテキストファイルに記述して管理・変更することが多い。

- OSの設定を変更する(すなわち、設定ファイルを書き換える)には、エディタと呼ばれるソフト（Windowsでいうと「メモ帳」にあたる）を使う。

- ターミナル上で使用できるエディタに"nano"と呼ばれるものがあり、気軽に使いやすいので便利。

- nanoを起動するには、  
`$sudo nano`

- `sample.txt`という名前のファイルを開いてnanoで編集するには、  
`$sudo nano sample.txt`

- 上書き保存するには、`Ctrl+O`を押した後に`Enter`

- nanoを終了するには、`Ctrl+C`を押した後に`Enter`

---

### 6. httpのプロキシ回避

1. nanoで`~/.bashrc`を編集。  
`$sudo nano ~/.bashrc`  
2. `~/.bashrc`末尾に以下を追記  
```
export http_proxy=http://procy.cc.yamaguchi-u.ac.jp:8080/
export https_proxy=http://procy.cc.yamaguchi-u.ac.jp:8080/
export ftp_proxy=http://procy.cc.yamaguchi-u.ac.jp:8080/
```
3. 保存してnanoを終了。  
4． `$sudo reboot`

---

### 7. aptのプロキシ回避

1. nanoで`/etc/apt/apt.conf`を編集。  
`$sudo nano /etc/apt/apt.conf`  
2. `/etc/apt/apt.conf`に以下を追記  
```
Acquire::http::proxy "http://proxy.cc.yamaguchi-u.ac.jp:8080/";
Acquire::https::proxy "http://proxy.cc.yamaguchi-u.ac.jp:8080/";
Acquire::ftp::proxy "http://proxy.cc.yamaguchi-u.ac.jp:8080/";
```
3. 保存してnanoを終了。  
4． `$sudo reboot`

---

### 参考：apt（アプト）について

- Raspbianを含むLinux（より正確にはDebian）では、ソフトのインストールにapt（アプト）と呼ばれる仕組みを利用している。

- 自分が使っているOSに適合するプログラムのバージョンや依存関係などが管理されており、使用者はそれらについて意識することなく、
コマンド一つで簡単に適切なプログラムをインストールすることができる。

- 以下、`sl`というソフト（プログラム）のインストールを例に、aptの使い方を示す。

0. `sl`を実行してみる。当然、今`sl`はまだインストールされていないので、「そんなものはないよ」というメッセージが出るだけ。  
`$sl`  
1. aptが管理しているデータベースをアップデートする。  
`$sudo apt-get update`  
ターミナルにずらずらと文字がたくさん出る。  
2. aptによって`sl`をインストールする。  
`$sudo apt-get install sl`  
ターミナルにずらずらと文字がたくさん出る。  
3. `sl`がインストールされたか確認する。  
`$sl`  
正しくインストールされていると、ターミナル上に...？  
4. プログラムをアンインストールするには以下。  
`$sudo apt-get purge sl`  
5. aptで管理されている中からプログラムを探すには以下。  
完全一致  
`$sudo apt list sl`  
部分一致  
`$sudo apt search sl`  

---

### 8. 日本語環境の構築

Raspberry Piで日本語表示や日本語入力ができるようにする。

1. 日本語入力メソッドのインストール  
Googleが開発した入力メソッドであるmozc（モズク）を使用。  
`$sudo apt-get install fcitx-mozc`  
2. 日本語フォントのインストール  
これまたGoogleが提供している日本語向けフォントであるNotoフォントを使用。  
`$ sudo apt-get install fonts-noto`  
3. 半角/全角キーで入力切替ができるようになっているはず。  
4. スタートメニューから適当なエディタを開いて確認する。  

---

### 9. 日付時刻の設定

- 普通のPCと異なり、Raspberry Piには時刻を保持しておくための仕組みがない。そのため、起動していない状態が長く続くと時刻が狂う。

- 手動で時刻合わせをするには`date`コマンドを用いる。

- Raspberry Piの現在時刻を確認するには、以下のようにする。  
`$date`  

- Raspberry Piの日付時刻を2019年04月01日15時30分00秒にするには、以下のようにする。  
`$sudo date -s "2019/04/01 15:30:00"`  

---


### 10. Webの閲覧

ここまでの設定が正しくできていれば、ブラウザを開いてWebページを閲覧することができるはず。

1. yunetに接続する。有線の場合はRaspberry PiをLANケーブルで情報コンセントに接続する。  
無線の場合はデスクトップ右上のアイコンをクリックしてyunetを選択。パスフレーズを入力する。  
2. ブラウザを開く。ターミナルを開き、以下のコマンドを入力。ブラウザが立ち上がる。  
`$epiphany &`  
3. 学内LANの認証を通す。ブラウザのURL入力欄に`ic.cc.yamaguchi-u.ac.jp`と入力。  
認証ページに自分のユーザIDとパスワードを入力する。  
4. 何か適当なページが開けるかやってみる。  

---

### 11. 基本的なLinuxコマンド

Linuxコマンドは星の数ほどあり、そのすべてを解説することは現実的でない。  
ここでは、もっとも基本的で使用頻度の高いコマンドをいくつか紹介する。  　
他のコマンドについては、必要に応じてWebなどで検索する。

- `ls`

  - カレントディレクトリ（現在のフォルダ）の中身を見るときに用いる。
  
  - カレントディレクトリは、初期状態では`/home/pi`
  
  - より詳細な情報を表示するには、`$ls -la`

- `cd`

  - ディレクトリ（フォルダ）を移動するときに用いる。
  
  - カレントディレクトリに戻るには、`$cd`
  
  - 一つ上のディレクトリに戻るには、`$cd ..`
  
  - `/home/pi/test`というディレクトリに移動するには、`$cd /home/pi/test`（絶対パス）
  
  - カレントディレクトリが`/home/pi`であるときには、`$cd test`や`$cd ./test`のようにしてもよい。（相対パス）
  
- `cat`

  - ファイルの内容を表示するときに用いる。
  
  - `/home/pi/aiueo.txt`というファイルの内容を表示するには、`$cat /home/pi/aiueo.txt`（絶対パス）
  
  - カレントディレクトリが`/home/pi`であるときには、`$cat aiueo.txt`や`$cat ./aiueo.txt`のようにしてもよい。（相対パス）
  
  - `cat`コマンドはファイルを表示するだけで、編集することはできない。
  
  
---


[前の章へ](https://yu-workshop2019.github.io/chapter_1/chapter_1)


[次の章へ](https://yu-workshop2019.github.io/chapter_3/chapter_3)


[目次へ](https://yu-workshop2019.github.io/manual)


[トップページへ](https://yu-workshop2019.github.io/)
