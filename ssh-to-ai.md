# 知の物理学研究センターワークステーション(ai)へのSSHリモートアクセス

* ECCSのSSHサーバは、ECCS2026への移行にともない、2026年2月に廃止された
* 大学外から ai にSSHログインする際には、ECCSのSSHサーバを経由せず、先に UTokyo VPN に接続する

### ceenvからaiへのSSHアクセス

以下、「仮想OS」はVirtualBox内で動いているceenv、「ホストOS」はその上でVirtualBoxが動いているWindows、macOSなどを指す

1. SSH鍵ペアの作成 (初回のみ)
    - 仮想OS (ceenv)上で LXTerminal を開く
    - コマンドラインから ```ssh-keygen -t rsa``` を実行する
    - ```Enter file in which to save the key (/***/.ssh/id_rsa):``` と訊かれるが、何も入力せずに単に return キー(あるいは enter キー)を押す
    - ```Enter passphrase (empty for no passphrase):``` と訊かれるのでパスフレーズを入力し return キー(あるいは enter キー)を押す
    - ```Enter same passphrase again:``` と訊かれるので、上と同じパスフレーズを入力し return キー(あるいは enter キー)を押す
    - 秘密鍵が ```$HOME/.ssh/id_rsa``` に、公開鍵が ```$HOME/.ssh/id_rsa.pub``` に作成される

1. aiにSSH公開鍵を登録 (初回のみ)
    - 仮想OS (ceenv)上で LXTerminal を開き、```cat  $HOME/.ssh/id_rsa.pub | xsel -b -i``` を実行する
    - SSH公開鍵がクリップボードにコピーされる
    - UTOLの「計算機実験I」のアンケート「計算機実験 SSH公開鍵登録フォーム」からコピーしたSSH公開鍵を登録する

1. 管理者から、アカウント作成、SSH公開鍵の登録の完了が届くまで(数日)待つ

1. UTokyo VPNに接続する
    - 大学外から接続する場合は、ホストOS側で先にUTokyo VPNへ接続する
    - 接続方法は [UTokyo VPN](https://utelecon.adm.u-tokyo.ac.jp/utokyo_vpn/) を参照

1. aiにSSHログイン
    - 仮想OS (ceenv)上で LXTerminal を開く
    - コマンドラインから ```ssh u1234567890@ai.phys.s.u-tokyo.ac.jp``` を実行(```u1234567890``` の部分は自分のaiのアカウント名(講義時に通知)に置き換える)
    - 初回のみ、ホスト鍵の確認が表示されたら ```yes``` を入力する
    - ```Enter passphrase for key '/home/user/.ssh/id_rsa':``` と訊かれるので、SSH鍵ペアの作成時に設定したパスフレーズを入力する
    - ai上のコマンドプロンプトが表示されたら、リモートログイン成功
    - ログアウトするには ```exit``` を実行する

### macOSからaiへのSSHアクセス

1. SSH鍵ペアの作成 (初回のみ)
    - macOS上で「ターミナル」を開く
    - コマンドラインから ```ssh-keygen -t rsa``` を実行する
    - 以下、ceenvの場合と同じ

1. aiにSSH公開鍵を登録 (初回のみ)
    - macOS上で「ターミナル」を開く
    - コマンドラインから、```pbcopy < $HOME/.ssh/id_rsa.pub``` を実行する
    - SSH公開鍵がクリップボードにコピーされる
    - 以下、ceenvの場合と同じ

1. 管理者がSSH公開鍵を登録作業を完了するまで待つ

    以下、ceenvの場合と同じ

### Windows (Ubuntu WSL2)からaiへのSSHアクセス

ceenvの場合とほぼ同じであるが、SSH鍵ペアを作成する前に ```eval `ssh-agent` ```コマンドを実行しておくとよい。
