端末の移行時の Sass、 Node.js 関連のローカル開発環境のセットアップ手順。
（ Mojave にて動作確認済）  
※ `~`（チルダ : ユーザーディレクトリ）で実行のこと。

# Xcode 関連

Xcode は本来アプリ開発のための IDE であるが、Sass および Compass 等の動作に Xcode コマンドラインツールが使用されるため必要となる。  
また、抱き合わせでインストールされる Simulator は iOS での動作確認のため、制作現場でよく用いられる。  

## Xcode のインストール
[Xcode - Mac App Store](https://itunes.apple.com/jp/app/xcode/id497799835?mt=12) からインストール  

## Xcode コマンドラインツールのインストール
gem（ RubyGems のライブラリ）のインストールに必要となる。  
コマンドラインで入れる手順は下記。  

1. `xcode-select --install`  
1. `sudo gcc --version` でライセンスに同意  
1. スペースキーでライセンスを読む  
1. `agree` と入力  

（もしかしたら Mac App Store からのインストールも可能かもしれない）

# Sass 関連

## RubyGems のアップデート
RubyGems（ Ruby 言語用の PMS ）が古いバージョンであることが多いのでアップデートが必要になる場合がある。

1. アップデート前のバージョンの確認（任意）  
`gem -v`  
1. アップデート  
`sudo gem update --system`  
1. アップデートできたかの確認（任意）  
`gem -v`  

> *Note:*
> `sass -v` や `npm -v` など、 `** -v` でバージョンを確認できる。  
> インストールされているものはバージョンが表示される。  
> インストールされていない、インストールに失敗しているものは `**: command not found` となる。  
> 正常にインストールできているかを確認する方法に用いられる。  

## node のインストール
1. [Node.js](https://nodejs.org/) にアクセスしてLTS（長期サポート版）をダウンロード  
1. インストーラーを起動してインストール  
※node を入れたら npm も自動的にインストールされる  

## Sass のインストール
Yosemite 以前は下記コマンドでインストール  
`sudo gem install sass`  

El Capitan 以降は SIP の影響を考慮してインストール先を変更する必要がある  
`sudo gem install -n /usr/local/bin sass`  

### 確認
`sass -v`  

### `gyp ERR! configure error` が出たら…
npm の設定値を適宜変更して再挑戦  

1. npm の所有者の設定値を設定  
`sudo npm config set user 0`  
1. npm の権限の設定値を root で実行できるように設定  
`sudo npm config set unsafe-perm true`  
1. もう一度 Sass のインストールを試す  

# コンパイラ関連

## Gulp のインストール

Gulp はタスクランナー。Sass 、Pug 等のコンパイルや仮想化などプラグインを組み合わせて開発用の環境を用意するためのもの。  
Gulp に限らず、タスクランナー依存のプラグインは内包する npm が動作する Ruby のバージョンや依存 npm のバージョン等が干渉する恐れがあるので、リスクを理解した上で利用する。  

1. `sudo npm install gulp -g`  
1. `sudo npm install gulp --save-dev`  

## Compass のインストール

Sass をベースにしたフレームワーク。タスクランナーの様に、生成先ディレクトリや圧縮形式、ベンダープレフィックス付与などの設定が可能。  
※2017年に非推奨となり、開発者サポートが終了しているので新規開発への利用は推奨しない　　

Yosemite 以前は下記コマンドでインストール  
`sudo gem install compass`  

El Capitan 以降は SIP の影響を考慮してインストール先を変更する必要がある  
`sudo gem install -n /usr/local/bin compass`  

## コンパイル用GUI
- [Koala](http://koala-app.com/)  
単純で使いやすく、Compass も動く。  
ただし、ソースファイル内に日本語等のマルチバイト文字があるとコンパイルエラーが発生する場合がある。  
Notification when compile is completed にチェックを入れると、コンパイル完了時にデスクトップ通知が表示されるようになる。
- [Prepros](https://prepros.io/)  
多機能、高機能でUIもきれいだが、非推奨パッケージのサポートはしていないので Compass は動かない。  
書き出し先や圧縮形式の設定などの Prepros 独自の設定ファイルが作成される。  
