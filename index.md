
# 計算機実習のための環境整備

## 必要な環境

* 「[計算機実験ハンドブック](https://github.com/utphys-comp/handbook/releases)」に書いてあることが、自宅のPCから一通り試せるような環境を準備する
    * プログラミング (オフライン・リモート利用)
        * エディタ、コンパイラ(C, C++, Fortran, BLAS/LAPACK, MPI/OpenMP)
    * 計算結果のプロット (オフライン利用)
        * gnuplot (python/matplotlib, MATLAB でも可)
    * 文書(レポート、論文)の作成 (オフライン・クラウド利用)
        * LaTeX (TeX Live あるいは Overleaf)
    * ネットワークの利用 (ECCSなどの大学の計算機にリモートアクセスできる環境)
	  * ターミナル、SSH
    * インタプリタ環境 (オフライン・クラウド利用)
	  * MATLAB、Python 2/3
    * 他の講義や実験で必要な計算機環境の整備についても、できるだけサポート

## 推奨環境

* ceenv + Overleaf
    * 自分で環境を用意できるのであれば、基本何を使ってもよい
    * しかし、個別の環境をサポートすることは不可能。問題が生じた時は、まず推奨環境で試した上で質問
    * サポートする側とされる側で同じ環境が揃っていることが重要
* 上記のceenv以外にもWSL2 (Windows 10の場合)やHomebrew (macOSの場合)などを使って、必要な環境を揃えることが可能である
    * [WSL2の導入](wsl) [西村俊祐氏(物理学科2020年進学)による]
* 上記に加えて、オンライン授業・実習を効果的に行うために、Webex/Zoom, ITC-LMS, Slackなどを活用する

## 準備

* UTokyo Account (東大限定)
    * これがないと UTAS にも ITC-LMS にもアクセスできない
    * オンライン講義のURLも分からない
* ECCSクラウドメール (@g.ecc.u-tokyo.ac.jp) (東大限定)
    * 「計算機実験Slack」や「SSH公開鍵登録フォーム」などにアクセス

* 「計算機実験」Slack (「計算機実験」限定)
    * 参加リンクはITL-LMSで通知

* オンライン会議システム Webex and/or Zoom (オンライン講義限定)
    *  [https://utelecon.github.io/oc/](https://utelecon.github.io/oc/) (情報が多すぎて読むのが大変)

* ceenv (Computer Experiment Environment)
    * VirtualBox仮想環境。UNIX全般、C, C++, Fortran, Python, 並列化プログラミング環境がこれ一つで揃う
    * ダウンロードサイズは1.5GB程度
    * インストール方法 [https://github.com/cmsi/MateriAppsLive/wiki/ceenv](https://github.com/cmsi/MateriAppsLive/wiki/ceenv)
    * [MateriApps LIVE!](https://cmsi.github.io/MateriAppsLive/) は ceenv に加えて、いろいろな物質科学シミュレーションも実行できる環境一式が揃っている (ただしサイズは少し大きい 〜2.6GB)

* (あるいはceenvの代わりに) Ubuntu (WSL2)

    * [WSL2の導入](wsl) [西村俊祐氏(物理学科2020年進学)による]

* LaTeX (計算機実験ハンドブック 第3章)
    * [LaTeX環境の整備](latex)

* Gnuplot (計算機実験ハンドブック 1.4節)
    * ceenv (gnuplotインストール済み)
    * Ubuntu (WSL2) (```sudo apt install gnuplot```でインストールできる)
    * [単体でのインストール](gnuplot)

* SSHリモートアクセス (計算機実験ハンドブック 1.2節)
    * [ECCSへのリモートアクセス](ssh-to-eccs) (東大限定)
    * [知の物理学研究センターワークステーション(ai)へのSSHリモートアクセス](ssh-to-ai) (「計算機実験」限定)

* MATLAB あるいは Python など、インタープリタ言語の一つに慣れておくと便利
    * 電卓としての利用、図の描画、行列演算、数式処理、任意精度計算、など
    * [MATLABのインストールと利用方法](matlab)
    * Pythonは[ceenv](https://github.com/cmsi/MateriAppsLive/wiki/ceenv)、あるいは[Google Collaboratory](https://colab.research.google.com)を利用
