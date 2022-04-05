# MATLAB

## MATLABとは

* 科学技術計算やデータ科学などのためのプログラミング言語
    * C言語やPython、R (アール)などのソフトウェア言語と比べて、初学者にとって負荷が少ない
    * 数値計算、数式処理、統計、画像処理、信号処理あるいはシミュレーションのライブラリが揃っている
    * コンパイラを行わずに使えるので、かなり多様な環境で利用可能
* 東京大学では2019年度よりMATLAB全学ライセンスを締結
    * 東京大学の正規メンバーであれば、誰でもいくつでも利用負担なしで利用可能

 ## MATLABの利用環境
 
* MATLAB (デスクトップ版)
    * インストールが必要
    * いったんインストールが完了すれば、オフラインでも利用可能
* MATLAB Online
    * 最新版のMATLABをインストールせずに利用可能
    * ブラウザで利用可能なクラウド実行環境
* MATLAB Mobile
    * iPhone、Androidアプリをインストールして利用
    * 現状、いろいろ制約あり(図の表示の制限、等)
* 全ての利用環境の間で MATLAB Drive でファイル共有可能

## MathWorksアカウントの設定

* MATLAB (デスクトップ版、Online、Mobile)、MATLAB Driveの利用に必要
* UTokyo MATLAB Campus-Wide Licenseのページへ進む
[https://www.u-tokyo.ac.jp/adm/dics/ja/matlabcwl.html](https://www.u-tokyo.ac.jp/adm/dics/ja/matlabcwl.html)
* 「MATLABポータルサイト/MATLAB portal site」をクリック
* 「サインインして使い始める」をクリック
* UTokyo Accountを要求されるので、入力
* 「Create a MathWorks Account」をクリック
* アカウント作成画面が出るので必要事項を入力。メールアドレスにはECCSクラウドメールのアドレス(xxxxx@g.ecc.u-tokyo.ac.jp)を入力
* メールアドレス確認のためのメールが届くので、「メールの確認」をクリック
* 参考: https://www.sodan.ecc.u-tokyo.ac.jp/faq/utokyo-matlab-cwl/

## MATLAB (デスクトップ版)のインストール

* 2022年3月に最新版R2022aがリリースされています。日本語文字化けの問題などが改善されていますので、最新版の利用を推奨します
* 作成したMATLABアカウントをつかって、前述のページにログイン
* 「R2022a」をクリックしてダウンロード・インストール
    * MATLAB本体と次のToolboxを選択: Curve Fitting, Econometric, Optimization, Statistics and Machine Learning, Symbolic Math
* **注: MATLAB本体と必要なパッケージをインストールすると合計で数GB以上になります。モバイルデータ通信ではパケット代が高額になってしまう恐れがありますのでやめておきましょう**
    * 以前のバージョン(R2021a等)がすでにインストールされている場合はしばらくはそちらを使う。あるいは、WiFi環境が使える機会にインストール

## MATLAB Mobileのインストール

* [https://jp.mathworks.com/products/matlab-mobile.html](https://jp.mathworks.com/products/matlab-mobile.html)
    * インターネットに接続できれば、どこからでも MathWorks Cloud に接続して MATLAB にアクセスできる
    * ファイルは MATLAB Drive に保存される
    * スマートフォンの加速度・位置センサーからデータ収集してMATLABで処理することが可能
* Google Play もしくは App Store からMATLABアプリをインストール
    * 初回、実行時に MathWorks アカウントとパスワードを入力する

## MATLAB Onlineの実行方法

* [https://jp.mathworks.com/products/matlab-online.htm](https://jp.mathworks.com/products/matlab-online.html) にアクセス
* 「MATLAB Onlineの使用を開始する」をクリック
* MathWorks アカウントとパスワードを入力する

## MATLABの実行

* MATLAB (デスクトップ版)、MATLAB Online、MATLAB Mobileのいずれかを開く
* コマンドウィンドウの ```>>``` のあとに ```1+1``` と入力し、Enter (あるいは、Return)キーを押す 
    * ```2``` と出力されればOK

## MATLABの基礎

* MATLAB QuickStart: [https://elf-c.he.u-tokyo.ac.jp/courses/383](https://elf-c.he.u-tokyo.ac.jp/courses/383)