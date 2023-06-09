---
title: "【Docker】Reactの環境構築" # 記事のタイトル
emoji: "🎡" # アイキャッチとして使われる絵文字（1文字だけ）
type: "tech" # tech: 技術記事 / idea: アイデア記事
topics: ["python", "django"] # タグ。["markdown", "rust", "aws"]のように指定する
published: true # 公開設定（falseにすると下書き）
---
## はじめに
以前、DockerコマンドでReactを立ち上げる方法の勉強をしたので、執筆します。
下記の画面が表示されるまでを解説したいと思います。
![React_step6](/images/React_step6.png)


|  項目  | 内容  |
| ---- | ---- |
|  **対象者**  |  ・Docker初学者  |
|  **伝えたい内容**  |  ・DockerコマンドでReactを立ち上げる方法  |
|  **前提条件**  |  ・node:14.17.0 |

## Docker DeskTopのインストール
### 1. インストーラーのダウンロード
下記URLをクリックし、Docker Desktopのインストーラーをダウンロードします。
@[card](https://docs.docker.com/desktop/install/windows-install/)

![docker_desktop_step0](/images/docker_desktop_step0.png)

### 2. インストール開始
デフォルトのままのチェック状態で`OK`をクリックしてください。
![docker_desktop_step1](/images/docker_desktop_step1.png)
インストールに少し時間がかかります。
![docker_desktop_step2](/images/docker_desktop_step2.png)

### 3. PCの再起動
:::message alert
`Close and restart`をクリックすると、 **PCが再起動します。注意してください！**

※WSL2を有効化する為に、PCの再起動が必要です。
:::
![docker_desktop_step3](/images/docker_desktop_step3.png)
:::message alert
下記の画像が表示される場合は、**補足情報**を参照してください。
![docker_desktop_step5](/images/docker_desktop_step5.png)
:::


### 4. Docker Subscription Service Agreementを承認する
:::message
有料サブスクリプションサービスについて承認して利用します。
こちらの契約書は、主に企業やビジネス向けの契約書であり、個人利用にはあまり関係がありません。
:::
`Accept`をクリックしてください。

![docker_desktop_step4](/images/docker_desktop_step4.png)

### 5. インストール完了
下記の画像のようにDocker Desktopが問題なく起動出来たらOKです！

![docker_desktop_step6](/images/docker_desktop_step6.png)

## コンテナを作成する
### 1. docker runコマンド
Reactを動かせる環境(Nodejs)を作成する為に下記コマンドを実行します。
`Nodejsのバージョンを14.17.0でReact-envという名前のコンテナを作成するという意味になります。`
````bash
docker run -td --name="React-env" node:14.17.0 /bin/bash
````
### 2. 作成したコンテナを確認する
Docker Desktopを起動し、さきほどのコンテナが作成出来ている事を確認します。

![docker_desktop_step7](/images/docker_desktop_step7.png)

## Visual Studio Codeの拡張機能の追加
### 1. Docker
![extension_wsl](/images/extension_wsl.png)
### 2. Dev Containers
![extension_dev_containers](/images/extension_dev_containers.png)
### 3. WSL
![extension_docker](/images/extension_docker.png)

## Reactアプリを起動する
### 1. コンテナを起動する
Webアプリを作成する準備が整ったので作成していきます。
まずは、さきほど作成したコンテナを起動します。

1. Visual Studio Codeの左側の`Dcoker`のアイコンをクリックします。
2. さきほど作成したコンテナを右クリックで`Start`を押し、コンテナを起動します。

![React_step1](/images/React_step1.png)

:::message
Dcokerのアイコンをクリックしてもコンテナを確認出来ない場合は、Dcoker Desktopを起動してリロードしてみて下さい
:::

### 2. 起動したコンテナに接続する
Visual Studio CodeからRunning状態のコンテナに接続します。

1.先ほどのコンテナを右クリックから`Attach Visual Studio Code`をクリックします。
2.新しくVisual Studio Codeが起動します。

![React_step2](/images/React_step2.png)

### 3. 作成したコンテナと接続できている事を確認する
下記の画像が新しく起動したVisual Studio Codeになります。
パソコンの右下に`チェックマーク`が付いています。

![React_step3](/images/React_step3.png)

### 4. Reactアプリを作成する
画面左側の`フォルダーを開く`をクリックし
`/home `ディレクトリを開きます

![React_step4](/images/React_step4.png)

ターミナルを起動し、`/home`ディレクトリで
下記コマンドを実行し、Webアプリに必要なコードをインストールします。

````bash
npm install -g yarn
yarn create react-app sample_app --template typescript
````

:::message
【上記のコマンドの意味について】
yarn create react-app：yarnコマンドでReactのWebアプリを作成する
sample_app：Webアプリの名前
--template typescript：typescriptでWebアプリを構築する
:::

### 4. Reactを起動する
下記コマンドを実行して、Webアプリを起動します。
````bash
cd sample_app
yarn start
````
問題なく起動したら、上記のようなに
勝手にブラウザーが起動し、表示されます。

![React_step6](/images/React_step6.png)

## 補足情報

- **Q: WSLに関するエラー対応とは？**
    - A: 下記のようなエラーが発生する可能性があります。
![docker_desktop_step5](/images/docker_desktop_step5.png)
    1. Linux カーネル更新するインストーラーをダウンロードする
    @[card](https://learn.microsoft.com/ja-jp/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package)
    ![docker_desktop_web](/images/docker_desktop_web.png)
    2. インストーラーを実行する
    下記の画像のように手順を進め、WSLの更新を完了させてください。
    ![Linux_step0](/images/Linux_step0.png)
    ![Linux_step1](/images/Linux_step1.png)
- **Q: 接続先のコンテナの初期のファイル構成とは？**
    - A: 下記の通りです。
    ````bash
    /bin: 基本的なユーティリティやコマンドを含むバイナリファイルが格納されます。
    /boot: Linuxカーネルとブートローダーのファイルが格納されます。
    /dev: デバイスファイルが格納されます。
    /etc: システムの設定ファイルが格納されます。
    /home: ユーザーのホームディレクトリが格納されます。
    /lib: 共有ライブラリが格納されます。
    /lib64: 64ビットアーキテクチャ向けの共有ライブラリが格納されます。
    /media: 取り外し可能なメディア（CD、DVD、USBメモリなど）が自動的にマウントされる場所です。
    /mnt: 一時的にファイルシステムをマウントする場所です。
    /opt: オプションアプリケーション用に予約されています。
    /proc: カーネルとプロセスの情報が仮想ファイルシステムとして格納されます。
    /root: rootユーザーのホームディレクトリが格納されます。
    /run: 実行時に必要なファイルが格納されます。
    /sbin: システム管理者用のコマンドが格納されます。
    /srv: システム上のサービス用にデータが格納されます。
    /sys: カーネルパラメータを含むファイルシステムが格納されます。
    /tmp: 一時的なファイルが格納されます。
    /usr: 多くのアプリケーションやユーティリティが格納されます。
    /var: 変更可能なファイルが格納されます。
    ````
## おわりに
🎡のemojiがReactのロゴみたいに見える
