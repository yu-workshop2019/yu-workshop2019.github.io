# 山口大学工学部 ワークショップ 2019  解説資料


---

## 解説資料を掲載しています。

---


### Slack（チャットツール）

- PCの場合は[ここ](https://slack.com/intl/ja-jp/)から。

- androidデバイスの場合は[ここ](https://play.google.com/store/apps/details?id=com.Slack&hl=ja)からアプリをダウンロード。

- iOSデバイスの場合は[ここ](https://itunes.apple.com/jp/app/slack/id618783545)からアプリをダウンロード。

---

### Raspberry Pi関連の参考書籍

ここで紹介する書籍は、すべて工学部図書館で貸出可能です。

- [Raspberry Piで学ぶ電子工作](http://bluebacks.kodansha.co.jp/books/9784062578912/appendix/)

- [実例で学ぶRaspberry Pi電子工作](http://bluebacks.kodansha.co.jp/books/9784062579506/appendix/)

- [Raspberry Piクックブック](https://www.oreilly.co.jp/books/9784873116907/)

- [Raspberry Piで学ぶ ROSロボット入門](https://www.rt-shop.jp/index.php?main_page=product_info&products_id=3540)

---

### Arduino関連の参考書籍

ここで紹介する書籍は、すべて工学部図書館で貸出可能です。

- [Arduinoをはじめよう 第3版](https://www.oreilly.co.jp/books/9784873117331/)

- [Prototyping Lab 第2版 --「作りながら考える」ためのArduino実践レシピ](https://www.oreilly.co.jp/books/9784873117898/)

---

### 1. 開発環境

以下の開発環境を想定しています。

ノートPCのOS：Microsoft Windows10

Raspberry PiのOS：Raspbian Stretch

---

```
sudo apt-get install sl
```

---

### 2. ノートPCの準備

1． ノートPCに以下のソフトをダウンロード・インストールする。

- [Win32 Disk Imager](https://forest.watch.impress.co.jp/docs/review/1067836.html)

  - SDカードにRaspbianOSを書き込んだり、バックアップしたりするためのソフトです。

- [Tera Term](https://forest.watch.impress.co.jp/library/software/utf8teraterm/)

  - ノートPCからRaspberry PiにSSHログインするためのソフトです。

- [WinSCP](https://forest.watch.impress.co.jp/library/software/winscp/)
  
  - ノートPCからRaspberry Piにファイル転送するためのソフトです。
  
2. [Raspberry Pi財団の公式サイト](https://www.raspberrypi.org/downloads/raspbian/)から、RaspbianのイメージファイルをノートPCにダウンロード・解凍する。
  
---


### 3. aptのプロキシ回避

1. nanoで`/etc/apt/apt.conf`を編集。

`$sudo nano /etc/apt/apt.conf`

2. `/etc/apt/apt.conf`に以下を追記

```
Acquire::http::proxy "http://proxy.cc.yamaguchi-u.ac.jp:8080/";
Acquire::https::proxy "http://proxy.cc.yamaguchi-u.ac.jp:8080/";
Acquire::ftp::proxy "http://proxy.cc.yamaguchi-u.ac.jp:8080/";
```

3. 保存して終了。

---


### 1. 

---

### 1. 

---


### 1. 

---


### 1. 

---

[トップページへ](https://yu-workshop2019.github.io/)
