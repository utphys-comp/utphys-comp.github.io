# ECCSへのSSHリモートアクセス

### ceenvからECCSへのSSHアクセス

以下、「仮想OS」はVirtualBox内で動いているceenv、「ホストOS」はその上でVirtualBoxが動いているWindows、macOSなどを指す

1. ECCS (教育用計算機システム)にログインできるかどうかを確認 (初回のみ)
    - ホストOSでウェブブラウザを立ち上げ、ECCSポータル [https://portal.ecc.u-tokyo.ac.jp/](https://portal.ecc.u-tokyo.ac.jp/) にアクセス
    - UTokyo Account のユーザID (10桁の数字)とパスワードを入力
    - ログインできればOK

1. SSH鍵ペアの作成 (初回のみ)
    - 仮想OS (ceenv)上でスタートメニュー ⇒ System Tools ⇒ LXTerminal を開く
    - コマンドラインから ```ssh-keygen -t rsa``` を実行する
    - ```Enter file in which to save the key (/***/.ssh/id\_rsa):``` と訊かれるが、何も入力せずに単に return キー(あるいは enter キー)を押す
    - ```Enter passphrase (empty for no passphrase):``` と訊かれるのでパスフレーズを入力し return キー(あるいは enter キー)を押す
    - ```Enter same passphrase again:``` と訊かれるので、上と同じパスフレーズを入力し return キー(あるいは enter キー)を押す
    - ここで入力する「パスフレーズ」は、UTokyo Accountなどの「パスワード」とは別のものである。「パスフレーズ」は自分で決める文字列であり、他のサービスに用いる「パスワード」とは異なるものにすべきである。また、設定した「パスフレーズ」は忘れずに覚えておくこと
    - 秘密鍵が ```$HOME/.ssh/id_rsa``` に、公開鍵が ```$HOME/.ssh/id_rsa.pub``` に作成される(コマンドラインから ```ls -a $HOME``` を実行して、```.ssh```というディレクトリが作成されていることを確認してみよ)

1. ECCSにSSH公開鍵を登録 (初回のみ)
    - 仮想OS (ceenv)上で LXTerminal を開き、```cat  $HOME/.ssh/id_rsa.pub | xsel -b -i``` を実行する
    - SSH公開鍵がクリップボードにコピーされる
   - ホストOSでウェブブラウザを立ち上げ、ECCSポータル [https://portal.ecc.u-tokyo.ac.jp/](https://portal.ecc.u-tokyo.ac.jp/) にアクセス・ログイン
   - 「SSHサーバ公開鍵アップロード」をクリック
   - 「送信方法」として「テキスト貼付け」を選択
   - 「テキスト」フィールドが表示されるので、枠内にクリップボード上のSSH公開鍵をペースト(右クリック ⇒「貼付け」等)
   - 「送信」をクリック

1. ECCSにSSHログイン
    - 仮想OS (ceenv)上で LXTerminal を開く
    - コマンドラインから ```ssh 1234567890@ssh01.ecc.u-tokyo.ac.jp``` を実行(```1234567890``` の部分は自分の共通IDに置き換える)
    - 初回のみ

        ```
        The authenticity of host 'ssh01.ecc.u-tokyo.ac.jp (192.51.223.226)' can't be established.
ECDSA key fingerprint is SHA256:4fUNtKacYcAKwPoQ9Npm3+1NNRNMLnajvSQUKiGUJ74.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
        ```
       
       のような警告が表示されるが、```yes``` を入力し return キー(あるいは enter キー)を押す
    - ```Enter passphrase for key '/home/user/.ssh/id_rsa':``` と訊かれるので、SSH鍵ペアの作成時に設定したパスフレーズを入力する
    - ```ssh01:~ 1234567890$``` のようなコマンドプロンプトが表示されたら、リモートログイン成功
    - ログアウトするには ```exit``` を実行する

### macOSからECCSへのSSHアクセス

1. ECCS (教育用計算機システム)にログインできるかどうかを確認 (初回のみ)
    - ceenvの場合と同じ

1. SSH鍵ペアの作成 (初回のみ)
    - macOS上で「ターミナル」を開く
    - コマンドラインから ```ssh-keygen -t rsa``` を実行する
    - 以下、ceenvの場合と同じ

1. ECCSにSSH公開鍵を登録 (初回のみ)
    - macOS上で「ターミナル」を開く
    - コマンドラインから、```pbcopy < $HOME/.ssh/id_rsa.pub``` を実行する
    - SSH公開鍵がクリップボードにコピーされる
    - 以下、ceenvの場合と同じ

1. ECCSにSSHログイン
    - macOS上で「ターミナル」を開く
    - コマンドラインから ```ssh 1234567890@ssh01.ecc.u-tokyo.ac.jp``` を実行(```1234567890``` の部分は自分の共通IDに置き換える)
    - 以下、ceenvの場合と同じ
    - パスフレーズを入力する際に「パスワードをキーチェーンに保存」にチェックを入れておくと、次回以降パスワードなしでSSHログインできるようになる

### Windows (Ubuntu WSL2)からECCSへのSSHアクセス

ceenvの場合と同じ

### 参考資料

* [外部からのECCSの利用/SSHサーバ](https://www.ecc.u-tokyo.ac.jp/system/outside.html#ssh)
