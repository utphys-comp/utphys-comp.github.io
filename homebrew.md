# Homebrewによる環境整備

## macOSへのHomebrewのインストール

参考: [公式ドキュメント](https://brew.sh/index_ja)

### Homebrewのインストール

ターミナルを開き以下を実行する

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

途中でパスワードの入力が求められる

### パスの追加

Apple Silicon (M1/M2/M3)では以下を実行する必要がある

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> $HOME/.zprofile
```

### Homebrewの動作確認

一旦、ターミナルを閉じ、新しいターミナルを開く。以下を実行してバージョン番号(4.2.15など)が表示されることを確認する

```
brew --version
```

## C/C\+\+言語とBLAS/LAPACKの環境整備

### C/C\+\+言語のコンパイラのインストール

```bash
brew install gcc
```

GCCの最新版が、gcc-13 (Cコンパイラ)、g++-13 (C++コンパイラ)という名前でインストールされる

```bash
gcc-13 --version
```

### BLAS と LAPACK


```bash
brew install openblas lapack
```

## Gnuplot のインストール

```bash
brew install gnuplot
```

## SSH の方法

ceenvの場合と同様の操作でSSH接続が出来る。ceenvで用いる"LXTerminal"をmacOSのターミナルであると思って操作をすればよい。詳しくは[ECCSへのリモートアクセス](ssh_to_eccs)を参照されたい。

## テキストエディター

vimはデフォルトでmacOSにインストールされている。emacsは以下のコマンドでインストールする

```bash
brew install --cask emacs
```

## Pythonのインストール

Python 3, numpy, scipy, matplotlibのインストール

```
brew install python numpy scipy
pip3 install --upgrade pip
pip3 install --upgrade matplotlib
```
