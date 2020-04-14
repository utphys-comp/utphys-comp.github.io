# LaTeX環境

オンラインサービスでよければ Overleaf を使うのが最も簡単。オフラインで利用したい場合には、PCにTeX Liveをインストールする。ただし、かなりのダウンロード量になることに注意

### Overleaf

* オンラインLaTeXエディタ。Webブラウザ上でLaTeX文書の作成、保存、コンパイルが可能
* 使用方法

  1. 初回のみ: [https://www.overleaf.com](https://www.overleaf.com) にアクセスし、「Register」からユーザ登録を行う
  1. 2回目以降: EmailとPasswordを入力してログインする
  1. 新しい文書の作成
     1. 「New Project」→「Blank Project」を選択し、適当な名前(例: 計算機実験Iレポート1)を入力して「Create」
     1. 日本語の文章を作成する場合に必要な準備
        - 左上のファイルアイコンをクリックして、「New File」を選択、「File Name」に「latexmkrc」を指定して「Create」
        - 左のファイル一覧にlatexmkrcが現れるので選択し、以下の通り入力する

          ```
          $latex = 'platex';
          $bibtex = 'pbibtex';
          $dvipdf = 'dvipdfmx %O -o %D %S';
          $makeindex = 'mendex %O -o %D %S';
          $pdf_mode = 3;
          ```

        - メニューボタンを押して、「Compiler」に「LaTeX」を選択する

  1. main.texを編集する。ファイル一覧のPDFをクリックし「Recompile」ボタンを押すと、PDFファイルが作成される。あるいは、右上の矢印「Split Screen」をクリックしてLaTeXのソースコードとPDFプレビューを並べて表示することもできる

### Windows

* LaTeX (TeX Live)のインストール

  1. [https://www.tug.org/texlive/acquire-netinstall.html](https://www.tug.org/texlive/acquire-netinstall.html) にアクセス
  2. install-tl-windows.exe (18MB)をダウンロードして開く
  3. 指示にしたがってインストールを進める

### macOS

* LaTeX (TeX Live)のインストール

  1. [https://texwiki.texjp.org/?TeX%20Live%2FMac](https://texwiki.texjp.org/?TeX%20Live%2FMac) にしたがってインストール

* TeXShopで日本語の文書をコンパイルするには、初回に以下の設定が必要

  1. 「TexShop」メニュー > 「環境設定」を開く
  2. 左下の「設定プロファイル」プルダウンから「pTeX (ptex2pdf)」を選んだ後、「OK」
  3. TeXShopを終了し、再度開く

* macOSでキーボードからバックスラッシュ「\」が入力できないときは、option + ¥ を使えばよい