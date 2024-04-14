# WSL2の導入

本文の目的は、Windows10 PC上にWSL2 (Windows Subsystem for Linux 2)を用いて仮想的にLinux環境を導入するまでの手順を解説することである。WSL2の導入によって Windows 10でLinux環境を実現を仮想的に実行することができる。また、VS Codeを用いることでよりスムーズな開発環境を実現することも出来る[^1]

[^1]: 本ドキュメントは主に西村俊祐氏(物理学科2020年進学)によるものである

一度WSL2の環境構築をしてしまえば、Windowsで開発を行う上で必要な環境はほとんど整っていると言える。しかしながらWSL2の導入には(2020年12月現在では)やや複雑な手順を踏む必要があり、時間もそれなりにかかる。そのためパソコン操作に不慣れな場合はceenvを使う事をお勧めする[^2]

[^2]: とはいえWSL 2を使いこなせるとカッコいい気もするし、やってみたいですよね

なるべく本文のみを参照して環境構築が出来るように努めるが、PC環境によっては異なる操作が必要な場合もある。そのため何か不明な点やエラーで上手く行かない場合は、計算機実験Slackで質問をしたり[^3]、エラーコードをコピペして検索するなどして頂きたい

[^3]: Windowsユーザーでない限りWSLには触れないので、検索に便りがちになる場合もあります。筆者にTwitterなどで質問して頂いても構いません

追記(2024年4月 - ST): Windows 11でもWindows 10　(OSビルド 20262以降)の場合とほぼ同じ手順でWSL2がインストールできることを確認済みである。ただし、Windows 11では、手順1で `wsl --install` を実行するだけで、手順6のUbuntuのインストールまで自動的に行われるようである

### 注意事項

WSL2の環境構築をする前に共有しておきたい注意事項は以下の通りである

- 環境構築には時間がかかる
- 不慣れな事をするので、結構疲れる
- 環境によってはWSL2を導入できない場合もある(インストールの章で詳しく述べる。確認されたい)

以上を踏まえてなおWSL2環境を導入したい方は、以下の解説にお付き合いいただければと思う。
適宜参考文献へのリンクを掲載する。特に公式ドキュメントは信頼度が高い内容であるので、参照して頂きたい。
執筆(2020年12月)時点でのリンクであるので、リンク切れが起きている可能性がある。その際は本文のキーワードを検索するなどして頂きたい[^4]

[^4]: 検索して見つけた文献にリンクを更新して頂けると嬉しいです。この文章の更新に携わりたい方は先生に相談して頂ければと思います

## WSL2とは

参考: [公式ドキュメント](https://docs.microsoft.com/ja-jp/windows/wsl/)

WSL2とは、2020年にリリースされたWindows 10から直接アクセスの出来るLinux仮想環境を実現するシステムである。前身のWSL1から大幅にパフォーマンスを向上[^5]したものになっている。また、計算機実験では用いないが、Dockerという仮想環境の管理システムが使えるようになったりと、開発環境としての使いやすさが大幅に向上している[^6]

[^5]: ファイルアクセス周りだけはWSL 1の方が高機能とされています
[^6]: 私は特に開発をやっているわけではないので、そうらしいという話です。私からするとちょっと速くなったWSLという印象です

## WSL2のインストール

参考: [公式ドキュメント](https://docs.microsoft.com/ja-jp/windows/wsl/install-win10)

### 手順 1 Windows 10のバージョンの確認

Windows 10のバージョンによってインストール方法が異なるのでまずWindows 10のバージョンを確認する

1. `Win`+`R`を押して「ファイル名をして実行」を開く
2. `winver`と入力する

するとWindos 10のバージョンとOSビルドが表示される。WSL2のインストールには、**バージョン 1903**以上、**OSビルド 18362**以上が必要である

#### OSビルド 20262以降の場合

2020年12月現在ではWindows Insider Programのみで可能な操作である

1. スタートメニューを開く
2. "コマンドプロンプト"を検索ボックスなどで探し、右クリックして"管理者として実行"を押して開く
3. `wsl --install`と入力し、Windows を再起動する

Windows側の用意はこれだけで完了する。後は手順 5 の「Virtualization Technology の有効化」を行えばWSL 2の導入は完了し、手順6の「Linux のディストリビューションのインストール」で操作は完了する

#### OSビルドが20261以下の場合

以下の手順2~6が必要である

### 手順2 WSL機能と仮想マシン機能の有効化

まず、Windows 10において"Linux用Windowsサブシステム"機能と"仮想マシンプラットフォーム"機能を有効化する必要がある

1. スタートメニューを開く
2. Windowsの設定を開く
   - 検索ボックスに"settings"と入力しても実行ができる
3. 画面中央上部にある検索ボックスに"Windowsの機能の有効化または無効化"と入力し、管理画面を開く
   - "Windowsの"まで入力すれば候補に出てくるのでそれをクリックすれば OK
4. "Linux用Windowsサブシステム"と"仮想マシンプラットフォーム"左のチェックボックスをチェックする

以上で機能の有効化が完了する。公式ドキュメントではPowerShellを用いて以上の操作を行なっている

### 手順3 Linuxカーネル更新プログラム パッケージをダウンロードし、インストールする

1. 以下のリンクからパッケージのダウンロードをする
   - [x64マシン用WSL2Linuxカーネル更新プログラムパッケージ](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
2. ダウンロードしたパッケージを実行し、インストールする
   - 管理者権限のアクセス許可が求められるので、インストールを承認する

### 手順4 WSL2を既定のバージョンとして設定する

この段階では WSL1が既定のバージョンになっていて不便なので、WSL2を既定のバージョンとして設定する

1. スタートメニューを開く
2. "powershell"と入力し"PowerShell"を実行する
3. PowerShellで以下を入力する

    ```powershell
    wsl --set-default-version 2
    ```

以上でWindows側のWSL2の準備は完了である。後はPCのハードウェア側で仮想マシン支援機能を有効化する必要がある

### 手順5 Virtualizaiton Technology の有効化

**注意**: この手順の操作では WindowsではなくBIOS (あるいはUEFI)というパソコンのハードウェア側のソフトウェアの設定をする。使用しているパソコンによって手順が異なるので注意されたい

WSL2はIntelやAMDなどが提供する仮想化マシン支援技術(Virtualization Technology)をWindowsを動かすパソコンそのものについて有効化する必要がある。利用しているパソコンによって操作画面、手順が異なるので注意を要する。**詳しくはパソコンやマザーボードのメーカーwebページを参照すること。例えば「メーカー名 virtualization 有効化」や"メーカー名 enable virtualization"などと検索してみてほしい**

参考:

- [iSumsoft "How to Enable Virualization(Hypervisor) in BIOS/UEFI"](https://www.isumsoft.com/computer/enable-virtualization-technology-vt-x-in-bios-or-uefi.html)
- [Lenovo 「Virtualization Technology (VT-X)を有効にするには」](https://support.lenovo.com/ar/ja/solutions/ht500006)

1. パソコンを再起動する
2. 軌道直後の画面で`ファンクションキー`、`Enter`、`delete`キーなどを押してBIOS画面に入る
   - デバイスによって押すべきキーは異なるので注意
3. "Advanced", "Security", "Processor", "Virtualizaiton"などの項目の
    - Intel CPUの場合
        - Intel Virtualization Technology (VT-X)
        - Intel Vt-d
    - AMD CPUの場合
        - SVM Mode

    を"Enable"にする
4. 設定を保存してBIOSを退出する

### 手順6 Linux ディストリビューションのインストール

手順5まででWSL 2の準備は完了した。後はWSL 2に好みのLinuxディストリビューションをインストールすればWindows上に仮想的なLinux環境を実現できる

1. [Microsoft Store](https://aka.ms/wslstore)を開く
2. 好きなディストリビューション(ここではUbuntu 20.04 LTS)を選択する
3. 入手ボタンからインストールする

以上でLinuxの準備は完了である[^7]

Linux 環境の起動は他のソフトウェアと同様にスタートメニューでディストリビューションの名前を入力すれば可能である。初めて起動すると、Linux上でのユーザー名の登録とパスワードの登録がある。特にパスワードについてはよく使うので忘れないようにしておこう。ユーザー作成が完了したら、コマンドラインが出てくる。UNIXコマンドで操作が可能であり、基本的に ceenvの項目に書いてある操作が可能である

初めに以下のコマンドを入力して、システムの更新をしておこう

```bash
sudo apt update
sudo apt upgrade
```

このコマンドを実行すると何回かインストールして良いかを聞かれるので、ストレージの残量が十分あることを確認して`Y`(Yes の意味)あるいは`Return`を押す。

コマンドにおける`sudo`は"super user do"の略で、管理者として実行することを意味する。`apt`は"Advanced Package Tool"ので、アプリケーションの管理をしてくれるソフトウェアである。したがって、`sudo apt update`は"管理者としてaptのupdateコマンドを実行する"という命令になる

[^7]: お疲れ様でした

## C/C\+\+言語とBLAS/LAPACKの環境整備

### C/C\+\+言語のコンパイラのインストール

ここでは[GNU](https://gcc.gnu.org/)が提供するC/C\+\+言語コンパイラをインストールする。Ubuntu上では"build-essential"パッケージにGNUが提供するコンパイラと主要なライブラリが含まれているので、これをインストールする

1. Ubuntuを起動する
2. コマンドラインに以下を入力する

    ```bash
    sudo apt install build-essential
    ```

### BLAS と LAPACK

参考:

- [Netlib公式サイト](http://www.netlib.org/lapack/)
- [Ubuntu 20.04のBLAS (dgemm) をベンチマーク](http://verifiedby.me/adiary/0150)

BLASは様々な提供元がある。BLASについては様々な提供元がある。ここでは[Open BLAS](https://www.openblas.net/)をインストールする。LAPACKは[Netlib](http://www.netlib.org/lapack/)が提供するものをインストールする。
それぞれ以下のコマンドでインストール出来る

```bash
sudo apt install libopenblas-base
sudo apt install libopenblas-dev
```

```bash
sudo apt install liblapack-dev liblapack-doc
```

複数のBLASをインストールした場合は、`libblas.so-x86_64-linux-gnu`ファイルでの設定をする事によって利用するライブラリを変更することが出来る。コマンドは以下の通り

```bash
sudo update-alternatives --config libblas.so-x86_64-linux-gnu
```

環境によるが、筆者の場合は以下のような画面が出てくる

```bash
There are 3 choices for the alternative libblas.so-x86_64-linux-gnu (providing /usr/lib/x86_64-linux-gnu/libblas.so).

  Selection    Path                                                   Priority   Status
------------------------------------------------------------
  0            /usr/lib/x86_64-linux-gnu/openblas-pthread/libblas.so   100       auto mode
  1            /usr/lib/x86_64-linux-gnu/blas/libblas.so               10        manual mode
* 2            /usr/lib/x86_64-linux-gnu/libmkl_rt.so                  1         manual mode
  3            /usr/lib/x86_64-linux-gnu/openblas-pthread/libblas.so   100       manual mode

Press <enter> to keep the current choice[*], or type selection number:
```

読み込むBLASを変更したいときは、コマンドラインに出てくる指示に従えば簡単に変更が出来る

## Gnuplot のインストール

以下のコマンドでインストール出来る

```bash
sudo apt install gnuplot
```

なお、プロットの表示には、以下の「GUIの利用」に従いX serverを有効にしておくことが必要である

## SSH の方法

ceenvの場合と同様の操作でSSH接続が出来る。ceenvで用いる"LXTerminal"をUbuntuターミナルであると思って操作をすればよい。
詳しくは[ECCSへのリモートアクセス](ssh_to_eccs)を参照されたい。

## テキストエディター

テキストエディターはコーディングやコンフィグファイルの編集など、様々な場面で利用する機会が多い。有名な例として"Vim"や"Emacs"がある。[^vim]
これらのソフトウェアはいずれもaptを通じてインストールすることが出来る

```bash
sudo apt install vim
sudo apt install emacs
```

[^vim]: Vim派かEmacs派かというのは、きのこ-たけのこ戦争並に有名です。私はどちらかというとVim派ですが、普段は後述するVS Codeで編集をしているので中立寄りです

## GUIの利用

GnuplotやPythonのMatplotlibなどGUIを利用するプログラムについてはそのままでは表示することができない。以下の手順により、Windows側であらかじめX serverをインストール・実行しておく必要がある

参考:

- [WSL2の導入とGUI環境の構築とsshfsしたものもgnome-openしたい!! [Ubuntu18.04/20.04]](https://qiita.com/momomo_rimoto/items/51d533ae9529872696ce)
- [WSL2におけるVcXsrvの設定](https://qiita.com/ryoi084/items/0dff11134592d0bb895c)

#### Windows側の準備

Windows側では、Linuxが表示しようとしている画面を受け取るサーバーを用意する必要がある。ここでは"VcXsrv"を利用する。
VcXsrvのダウンロードは[https://sourceforge.net/projects/vcxsrv/](https://sourceforge.net/projects/vcxsrv/)から出来る。ダウンロードしたら案内に従ってインストールすればよい。
GUIを表示したい時は以下のような手順でX serverの起動を行えば良い。

1. xlaunch.exeを実行する(スタートメニューから開けばよい)
2. 画面の案内に従って設定する
3. "multiple window"を選び次に進む
4. "start no client"を選び次に進む
5. "clipboard"(いわゆるコピペ)を使用したければチェックを入れる
6. "Adittional parameters for VcXsrv"の欄に`-ac`と入力してから次に進む

毎回起動するのは面倒である。以下のような操作でパソコン起動時に自動でX serverも起動することが出来る

1. 上述の操作1-6をする
2. "Save configuration"ボタンを押し、"config.xlaunch"を移動させやすい場所(例えばデスクトップ)に保存する
3. 完了を押す
4. "Winキー"+"R"を押して`shell:startup`と入力する
5. "スタートアップ"という名前のフォルダが開くので、"config.xlaunch"をスタートアップフォルダ内に移動する

#### Ubuntu側の準備

Ubuntu側では、表示先をあらかじめ環境変数```DISPLAY```に設定する必要がある

1. ```cat /etc/resolv.conf``` でファイル```/etc/resolv.conf```の中身を表示する
2. 先頭が```nameserver```で始まる```nameserver 123.45.67.89```のような行(数字はUbuntuを実行するたびに異なる)があるのでこの数字(IPアドレス)を控えておく
3. 以下のコマンドを実行する。なお```123.45.67.89```の部分は手順2のIPアドレスの値を入れる

    ```bash
    export DISPLAY=123.45.67.89:0
    ```

以上の設定により、例えばターミナルからgnuplotを実行し、```plot sin(x)```と入力するとウインドウが開きsin関数がプロットされるはずである

Ubuntuターミナルを開くたびに、上記の手順を繰り返すのは面倒である。```$HOME/.bashrc```ファイルの最後に、以下の1行を追加しておけば自動的に環境変数が設定される

```bash
export DISPLAY=$(grep nameserver /etc/resolv.conf | cut -d " " -f 2):0
```

## WindowsとUbuntuの間のファイル共有

WindowsとWSL2で動いているUbuntuの間では互いにファイルを参照することができる。パフォーマンスの問題があるので、基本的にはそれぞれの中でファイルI/Oを完結させることが望ましいが、UbuntuのファイルをWindowsのエディタで編集したり、計算結果やプロットをコピーするなどであれば特に問題はない

### Windows側からUbuntuのファイルの参照

参考: [Accessing Linux files from Windows](https://devblogs.microsoft.com/commandline/whats-new-for-wsl-in-windows-10-version-1903/)

1. Ubuntuのターミナルで以下を実行する

    ```bash
    explorer.exe .
    ```
    
    最後に```.```が必要であることに注意
    
2. Windowsのエクスプローラーの画面が開き、その中にUbuntuのファイル一覧が表示される。通常のWindowsのファイルと同様に移動したり、VSCodeなどのアプリで開いて編集することが可能である

### Ubuntu側からWindowsのファイルの参照

1. Ubuntu内ではWindowsのファイルシステムが```/mnt```の下に見えている。例えばCドライブのパスは```/mnt/c```である

## Visual Studio Code (VSCode)

参考:

- [Visual Studio Code公式サイト](https://code.visualstudio.com/)
- [【WSL / WSL2】VSCode×WSLでWindows上にLinux開発環境を構築](https://qiita.com/_masa_u/items/d3c1fa7898b0783bc3ed)
- [WSL 2とVS CodeでC, Python, LaTeXを使えるようにした話](https://event.phys.s.u-tokyo.ac.jp/physlab2021/advent-calendar/epexwm73p/)

VSCodeは、Microsoftが提供する高機能なコードエディターである。様々な言語での開発をサポートしているほか、Git連携やWSL2との連携、各種クラウドサービスとの連携も可能である。折角WSL2での環境構築をした皆さんには是非VSCodeとの連携も行ってもらいたいが、手順が多いので根気よく行っていただきたい。一度環境構築をすると楽に作業を進めることが出来る

様々な文献があるので、適宜検索してほしい。参考に挙げた二つ目の記事は、わかりやすくWSL2との連携について説明がされている。
三つ目のリンクは筆者が理物Advent Calendar 2020の折りに書いた記事である。正直なところ読みにくい記事であるが、UbuntuへのPythonの導入やVS Code上でのtex編集のための環境構築についても言及しているので参考にして頂きたい
