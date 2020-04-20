# ECCSへのSSHリモートアクセス

### ceenvからECCSへのSSHアクセス

以下、「仮想OS」はVirtualBox内で動いているceenv、「ホストOS」はその上でVirtualBoxが動いているWindows、macOSなどを指す

1. ECCS (教育用計算機システム)にログインできるかどうかを確認 (初回のみ)
    - ホストOSでウェブブラウザを立ち上げ、セキュアWWWサーバ [https://secure.ecc.u-tokyo.ac.jp/index.html](https://secure.ecc.u-tokyo.ac.jp/index.html) にアクセス
    - 「ディスク使用量の確認」を行ってみる
    - UTokyo Account のユーザID (10桁の数字)とパスワードを入力
    - 「あなたのアカウントでは， xxxx GBまでディスクを使用することができます．あなたの現在のディスク使用量は xxxx GBです．」のようなメッセージが表示されればOK

1. SSH鍵ペアの作成 (初回のみ)
    - 仮想OS (ceenv)上でスタートメニュー ⇒ System Tools ⇒ LXTerminal を開く
    - コマンドラインから ```ssh-keygen -t rsa``` を実行する
    - ```Enter file in which to save the key (/***/.ssh/id\_rsa):``` と訊かれるが、何も入力せずに単に return キー(あるいは enter キー)を押す
    - ```Enter passphrase (empty for no passphrase):``` と訊かれるのでパスフレーズを入力し return キー(あるいは enter キー)を押す
    - ```Enter same passphrase again:``` と訊かれるので、上と同じパスフレーズを入力し return キー(あるいは enter キー)を押す
    - ここで入力する「パスフレーズ」は、UTokyo Accountなどの「パスワード」とは別のものである。「パスフレーズ」は自分で決める文字列であり、他のサービスに用いる「パスワード」とは異なるものにすべきである。また、設定した「パスフレーズ」は忘れずに覚えておくこと
    - 秘密鍵が ```$HOME/.ssh/id_rsa``` に、公開鍵が ```$HOME/.ssh/id_rsa.pub``` に作成される(コマンドラインから ```ls -l $HOME``` を実行してみよ)

1. ECCSにSSH公開鍵を登録 (初回のみ)
    - 仮想OS (ceenv)上で LXTerminal を開き、```cat  $HOME/.ssh/id_rsa.pub | xsel -b -i``` を実行する
    - SSH公開鍵がクリップボードにコピーされる
   - ホストOSでウェブブラウザを立ち上げ、セキュアWWWサーバ [https://secure.ecc.u-tokyo.ac.jp/index.html](https://secure.ecc.u-tokyo.ac.jp/index.html) にアクセス
   - 「SSHサーバ 公開鍵アップロード」をクリック
   - UTokyo Account のユーザID (10桁の数字)とパスワードを入力
   - 「送信方法」として「テキスト貼付け」を選択
   - 「テキスト」フィールドが表示されるので、枠内にクリップボード上のSSH公開鍵をペースト(右クリック ⇒「貼付け」等)
   - 「送信」をクリック

1. ECCSにSSHログイン
    - 仮想OS (ceenv)上で LXTerminal を開く
    - コマンドラインから ```ssh 1234567890@ssh0-01.ecc.u-tokyo.ac.jp``` を実行(```1234567890``` の部分は自分の共通IDに置き換える)
    - 初回のみ

        ```
        The authenticity of host 'ssh0-01.ecc.u-tokyo.ac.jp (192.51.223.234)' can't be established.
ECDSA key fingerprint is SHA256:3FC6xTeUAaOnpb3+o75NLLyxmWr67Orhp/Px+2LB9H4.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
        ```
       
       のような警告が表示されるが、```yes``` を入力し return キー(あるいは enter キー)を押す
    - ```Enter passphrase for key '/home/user/.ssh/id_rsa':``` と訊かれるので、SSH鍵ペアの作成時に設定したパスフレーズを入力する
    - ```ssh0-01m:~ 1234567890$``` のようなコマンドプロンプトが表示されたら、リモートログイン成功
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
    - コマンドラインから ```ssh 1234567890@ssh0-01.ecc.u-tokyo.ac.jp``` を実行(```1234567890``` の部分は自分の共通IDに置き換える)
    - 以下、ceenvの場合と同じ

### WindowsからECCSへのSSHアクセス

To be written...

### 参考資料

* [外部からのECCSの利用/SSHサーバ](https://www.ecc.u-tokyo.ac.jp/system/outside.html#ssh)
