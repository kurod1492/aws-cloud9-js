# AWS Cloud9 開発環境で Javascript を動かしてみる

## 概要

ウェブアプリケーションに Javascript のプログラムを導入する前に、手元で Javascript のプログラムを単体で動かしてみたいときがあります。
それを Cloud9 で行う手順をまとめました。

## 題材

以下の記事を参考にします。

[JavaScriptでドラック＆ドロップによる画像の入れ替えを実装する](https://blog.ver001.com/javascript-dragdrop-image-switch/)

## HTML ファイルの作成

Cloud9 を起動します。

新しいフォルダ js-test を作成します。

js-test の中に新しいファイル index.html を作成します。

index.html の内容として以下のコードを記述します。

    <!DOCTYPE html>
    <html lang="ja">
      <head>
        <meta charset="UTF-8">
        <script type='text/javascript' src='swapicon.js'></script>
        <title>Javascript の動作確認</title>
      </head>
      <body>
        <h1>Javascript の動作確認</h1>
        <h2>ドラッグ&ドロップで画像を入れかえる</h2>
        <img src="img/mail.png" id="mail" draggable="true" ondragstart="dragstart();" ondragover="dragover();" ondrop="drop(this);" />
        <img src="img/chat.png" id="chat" draggable="true" ondragstart="dragstart();" ondragover="dragover();" ondrop="drop(this);" />
        <img src="img/doc.png" id="doc" draggable="true" ondragstart="dragstart();" ondragover="dragover();" ondrop="drop(this);" />
        <img src="img/spreadsheet.png" id="spreadsheet" draggable="true" ondragstart="dragstart();" ondragover="dragover();" ondrop="drop(this);" />
      </body>
    </html>

## Javascript ファイルの作成

js-test の中に swapicon.js というファイルを作ります。

swapicon.js の内容として以下のコードを記述します。

    function dragstart()
    {
      //ドラッグ元のIDを保存
      event.dataTransfer.setData("text/plain", event.target.id);
    }
    function dragover()
    {
      event.preventDefault();
    }
    function drop(obj)
    {
      event.preventDefault();
      //ドラッグしている画像のIDを取得
      var id = event.dataTransfer.getData("text/plain");
      //ドロップ先のsrcを保存
      var buff = obj.src;
      //ドロップ先のsrcにドラッグ元のsrcを上書き
      obj.src = document.getElementById(id).src;
      //保存していたsrcをドラッグ元のsrcへ上書き
      document.getElementById(id).src = buff;
    }

## 画像ファイルをアップロード

img というフォルダを作成し、その中に画像ファイルをアップロードします。

画像ファイルを以下のリンクよりらダウンロードしておきます。

https://github.com/kurod1492/aws-cloud9-js/raw/master/mail.png

https://github.com/kurod1492/aws-cloud9-js/raw/master/chat.png

https://github.com/kurod1492/aws-cloud9-js/raw/master/doc.png

https://github.com/kurod1492/aws-cloud9-js/raw/master/spreadsheet.png

js-test フォルダを右クリックして New Folder をクリックすると新しいフォルダが作成されますので、img と入力してエンターを押します。

img フォルダが選択された状態で、Cloud9 のメニューの File -> Upload Local Files をクリックします。

画像ファイルを「Drag & drop file here」と書かれているところにドラッグ&ドロップします。ファイルがアップロードされます。
全てのファイルがアップロードされたら右上の x ボタンを押して閉じます。

## 動作確認

作成した index.html を開いている状態で、メニューバーの Preview から Preview index.html をクリックします。
そうすると、新しいタブが開いて、その中に index.html の内容が表示されます。

画像が4つ並んでいます。画像をドラッグ&ドロップすることができます。
画像を掴んで、別の画像の上で離すと、画像が入れ替わります。

