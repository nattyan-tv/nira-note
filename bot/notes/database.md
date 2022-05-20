# [NIRA Bot](../index)

## データベースについて
にらBOTのデータベースシステムについて、開発者共有及びメモとして残しておきます。

## Database
にらBOTは、クラウドデータベース管理システムを使用しています。  
基本的に[こちら](https://qiita.com/164kondo/items/eec4d1d8fd7648217935)を見れば出来るはずです。  

1. Google Drive API及びGoogle Spread Sheets APIをご自身又は管理用のGoogleアカウントで有効にして、認証情報の設定、秘密鍵の生成を行ってください。  
秘密鍵のデータは、`util/gapi.json`として保存してください。(もちろん、ローカルのどこかにもバックアップを取っておきましょう。)  
2. GoogleDriveの適当な場所に、適当にSpreadsheetを作成して、APIのクライアントアドレスを共有欄に追加しましょう。
3. URLからキーを取り出して、`setting.json`の`database`に書きこきましょう。
4. 多分出来てます。

## データベースの使い方
まず、実際にデータベースが有効になっているかをテストするには、`n!db write [セルの場所] [書き込むデータ]`とすることで、そのセルにデータを書き込むことができます。  
`n!db read [セルの場所]`で、そのセルのデータを表示することができます。　　
プログラムとしてデータベースを管理するには、データベースシートをインスタンスとして初期化(する風に)して、なんかいろいろやっていきます。

```py
from util import database

DBS = database.openSheet()
DATABASE_KEY = "B2"

print(DBS.acell(DATABASE_KEY).value)
value = "testdayo"
DBS.update_acell(DATABASE_KEY, value)
```

こんな感じのプログラムを書けば、データベースへの書き込み/読み込みが出来ます。  
辞書形式かつ、キーが`int`の場合は、JSON化の時にキーが`str`になります。  
なので、データ読み込み時に`str`から`int`キーに戻す必要があったりなかったりしますので、ご注意ください。
