### Processingのダウンロード

以下のダウンロードサイトからProcessingをダウンロードする。

[https://processing.org/download/](https://processing.org/download/)

通常は、「Windows 64bit版」を選択する。  
ダウンロードしたzipファイルを解凍するだけで使用可能。

---

### プロキシの設定

学内で、ネットワーク経由でProcessingにライブラリを追加するためには以下の設定を行う。

1．Processingを起動

2.ファイル -> 設定 をクリック

3.ウィンドウ下部の「詳細な設定は、次のファイルを編集することで可能です」の下の行をクリック  
例）C:\Users\USERNAME\AppData\Roaming\Processing\preferences.txt

4.フォルダが開く

5．Processingを閉じる

6.preferences.txtをメモ帳などで開く  
※preferences.txtがないときは、代わりにpreferences.oldをメモ帳などで開いて同様に変更する
※preferences.oldが2つ以上あるときには、ファイルを更新時刻順に並び替えて、更新時刻が新しい方を編集する

7.preferences.txtの一部を以下のように書き換える

"""
＜変更前＞
proxy.http.host=
proxy.http.port=
proxy.https.host=
proxy.https.port=

＜変更後＞
proxy.http.host=proxy.cc.yamaguchi-u.ac.jp
proxy.http.port=8080
proxy.https.host=proxy.cc.yamaguchi-u.ac.jp
proxy.https.port=8080
"""

7.Processingを再び起動

8.追加のライブラリがインストールできるようになる

より詳細な情報については以下のWebページを参照

[Processing3をプロキシ環境下で使う](https://sites.google.com/site/jglabo701/processing3wopurokishi-huan-jing-xiade-shiu)

