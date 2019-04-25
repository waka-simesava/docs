## 「[cd to...](https://github.com/jbtule/cdto) 」とは

「[cd to...](https://github.com/jbtule/cdto) 」は Mac の Finder のツールバーに配置しておくことで、ターミナル起動＆移動がワンクリックで可能になる便利なアプリです。

ワンクリックで現在開いているディレクトリに移動した状態でターミナルが起動します。

> [参考記事]  
> [cd to... (Finderからワンクリックでターミナルを開く） - Qiita](https://qiita.com/sadoru/items/8a53c3d3b63a0fe45276)

## まずはアプリをダウンロード

1. https://github.com/jbtule/cdto にアクセス
1. [Download Latest cdto.zip] をクリック
1. `cdto_(バージョン).zip` をダウンロードして解凍

## 起動したいコマンドラインツールを決める

iterm・terminal・unsigned・x11_xterm の中から起動したいコマンドラインツールを選ぶ。  
例えば「iterm」であれば、「iterm」フォルダの中にある [cd to] 。これを…

1. 任意の場所に移動（「アプリケーション」等に。）
1. アプリのアイコンを、⌘キーを押しながらファインダーのツールバーの好きな位置にドラッグ

## 「cd to...」のアイコンを変える（任意）

上記の手順でアプリ自体は十分使えるが、個人的にアイコンが気に入らなかったので、自作した。  
[こちらのPSD](./files/cdto/cd_to.psd.zip) ファイルを使って好きなアイコンを作って書き出す。

[アセットを抽出] すると、
1. `cd_to-assets` フォルダ（さらにその中に `ico1.iconset` フォルダ）が生成される
1. ターミナルで `cd_to-assets` フォルダに移動する
1. 下記のコマンドで `ico1.icns` を生成する  
`iconutil -c icns ico1.iconset`
1. cd to アプリを `⌘` + `I` で情報をみて、アイコンのところに出来上がったアイコン（icnsファイル）をドラッグすると、アイコンが変更される

