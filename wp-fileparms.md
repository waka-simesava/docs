# サブディレクトリにインストールした WordPressで fileperms の Warning

WordPress をインストールする際にドメインが当たっているルートディレクトリではなく、「wp」や「cms」などのサブディレクトリにインストールするケースがあると思います。

先日、とあるサブディレクトリにインストールしたWordPressで、一般設定画面で fileperms の Warning が表示されていました。

```
Warning: fileperms(): stat failed for /**/**/cms/index.php in /**/**/cms/wp-admin/includes/file.php on line XXXX
```

WordPress の動作そのものには影響はないものの、そのままにしておくのは不快なので原因を探り、解決できました。
ドメインが当たっているルートで表示する手順として多くのサイトで紹介されているサブディレクトリの index.php を、適宜内容を書き換えてルートディレクトリに移動させるという手順ですが、この index.php は「移動」ではなく「複製」、つまり**元の index.php ファイルは編集せずにそのまま残しておく**必要がある様です。ドメインのルートには require のパスを修正した index.php を配置する形になります。

WordPress側で、index.phpのファイルのパーミッションを `fileperms()` で取得している様です。だからそこにないとパーミッションが取れないということみたいです。

これらを踏まえて、例として「sample」ディレクトリにインストールした場合、下記の様な手順になると思います。

## 1. 管理画面側  

1. [設定] > [一般] 画面に移動  
1. [サイトアドレス] の、サブディレクトリ部分を削除し [変更を保存]  
`https://your-domain.co.jp/sample` なら、  
`https://your-domain.co.jp` となる様に。  

※ この際、[WordPress アドレス] 箇所はそのままにしてください。

## 2. サブディレクトリの `index.php` ファイルを**複製**し編集  

`require( dirname( __FILE__ ) . '/sample/wp-blog-header.php' );`  
-> この中の `/sample` を取る。  
-> この様になる : `require( dirname( __FILE__ ) . '/wp-blog-header.php' );`  
-> これをドメインのルート（要は1つ前の階層）へ配置  
※ この際、サブディレクトリ内にあった `index.php` はそのまま、そのディレクトリに、なにも編集せずに残しておきます。「移動&編集」ではありません。

## 3. サブディレクトリの `.htaccess` ファイル

- `RewriteBase /sample/`
- `RewriteRule . /sample/index.php [L]`  

これらの記述内の `/sample` を取る。

- `RewriteBase /`
- `RewriteRule . /index.php [L]`

編集した .htaccess をドメインのルート（1つ前の階層）へ移動
