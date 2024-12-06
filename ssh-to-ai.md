# 知の物理学研究センターワークステーション(ai)へのSSHリモートアクセス

### ceenvからaiへのSSHアクセス

以下、「仮想OS」はVirtualBox内で動いているceenv、「ホストOS」はその上でVirtualBoxが動いているWindows、macOSなどを指す

1. ECCSへのSSHアクセスができるように設定を行う (初回のみ)
    - [ssh-to-ecc](ssh-to-eccs) 参照

1. aiにSSH公開鍵を登録 (初回のみ)
    - 仮想OS (ceenv)上で LXTerminal を開き、```cat  $HOME/.ssh/id_rsa.pub | xsel -b -i``` を実行する
    - SSH公開鍵がクリップボードにコピーされる
    - UTOLの「計算機実験I」のアンケート「計算機実験 SSH公開鍵登録フォーム」からコピーしたSSH公開鍵を登録する

1. 管理者から、アカウント作成、SSH公開鍵の登録の完了が届くまで(数日)待つ

1. aiにSSHログイン

    - 大学外部からaiに直接ログインすることはできないので、いったんECCSにSSHログインする。その際にはSSH Agent Forwardingという機能を使うことで、仮想OS (ceenv)の秘密鍵を使ってECCSからaiへのログインも可能となる
    - 仮想OS (ceenv)上で LXTerminal を開き、```ssh-add```コマンドを実行して、Forward Agentに鍵を登録する。その際、SSH鍵ペアのパスフレーズを訊かれるので入力する
    - いったんECCSにSSHログインする。その際に ```-A``` オプションをつけてForwardingを有効にする: ```ssh -A 1234567890@ssh01.ecc.u-tokyo.ac.jp``` を実行(```1234567890``` の部分は自分の共通IDに置き換える)
    - ECCSからaiにSSHログインする: ```ssh u1234567890@ai.phys.s.u-tokyo.ac.jp``` を実行(```u1234567890 ``` の部分は自分のaiのアカウント名(講義時に通知)に置き換える)

### macOSからaiへのSSHアクセス

1. ECCSへのSSHアクセスができるように設定を行う (初回のみ)
    - [ssh-to-ecc](ssh-to-eccs) 参照

1. aiにSSH公開鍵を登録 (初回のみ)
    - macOS上で「ターミナル」を開く
    - コマンドラインから、```pbcopy < $HOME/.ssh/id_rsa.pub``` を実行する
    - SSH公開鍵がクリップボードにコピーされる
    - 以下、ceenvの場合と同じ

1. 管理者がSSH公開鍵を登録作業を完了するまで待つ

    以下、ceenvの場合と同じ

### Windows (Ubuntu WSL2)からaiへのSSHアクセス

ceenvの場合とほぼ同じであるが、```ssh-add```コマンドを実行する前に、 ```eval `ssh-agent` ```コマンドを実行しておく必要がある。(参考: https://qiita.com/sshojiro/items/60982f06c1a0ba88c160)
