## 事前知識

このレッスンでは、VSCode入門とコマンドライン入門(Windowsを利用されている場合はPowershell入門)のレッスンを完了していることを前提にしています。まだ学習が住んでいない場合は、2つのレッスンをまず学習して下さい。

## Sassとは

Sass(**S**yntactically **A**wesome **S**tyle**S**heets)は、簡単に言うとCSSを拡張するための言語です。Bootstrapフレームワークでも採用されていて、世界中の多くのフロントエンド開発者が利用しています。このSassを使うことでCSSをより分かりやすく、また少ないコードで書くことが出来、フロントエンド開発をするなら必ず習得して置きたいスキルです。

## NPM、Node.jsのインストール

Sassを利用するにはNode.jsとNPMというパッケージがパソコンにインストールされている必要があります。以下の流れにしたがってまずNode.jsをインストールしてください。


1. [Node.jsのダウンロードページへアクセス](https://nodejs.org/ja/download/)
2. OSに応じて、推奨版をダウンロード(WindowsならWindows Installer、MacならMacOS Installer)
3. ダウンロードしたパッケージを開き、説明にしたがって進みインストールを完了する。
4. ターミナルまたはPowerShell上でNPM及びNodeがインストールされているか確認する。

インストールされているバージョンによって結果は異なりますが、以下のように表示されれば大丈夫です。

```bash
$ node -v
v8.11.3
$ npm -v
5.6.0
```

## Sassのインストール

1. ターミナルを開く
2. ターミナルで次のコマンドを実行する

```BASH
$ npm install -g sass
/usr/local/bin/sass -> /usr/local/lib/node_modules/sass/sass.js
+ sass@1.14.3
updated 1 package in 13.908s
```

3. バージョンを確認する。

```BASH
$ sass --version
1.14.3 compiled with dart2js 2.0.0
```

これでインストールされていることが確認でき、準備が完了しました。

### 上記の方法がうまくいかない場合

上記の方法がうまくいかない場合は、以下の方法をお試し下さい。また以下の方法もうまくいかない場合は、以下のURLにある方法もお試し下さい。なお、dart-sassを利用する場合は、後ほど利用する`--watch`というオプションが現状まだ未対応のためご注意ください。

[Standalone - dart-sass](https://github.com/sass/dart-sass#standalone)

**Windowsの場合**

1. Chocolateyのインストール

Chocolateyはパッケージマネージャーといわれるソフトウェアの一つです。次のコマンドでインストールすることが出来ます。PowerShellをAdministratorとして開いている必要がありますので注意して下さい。

```bash
$ Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

以下の公式ドキュメントも参考にして下さい。

[Install with PowerShell.exe](https://chocolatey.org/install#install-with-powershellexe)

2. Sassのインストール

以下のコマンドを実行してSassをインストールします。

```bash
$ choco install sass -prerelease
```

**Macの場合**

1. Homebrewのインストール

Homebrewはパッケージマネージャーといわれるソフトウェアの一つです。次のコマンドでインストールすることが出来ます。

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2. Sassのインストール

以下のコマンドを実行してSassをインストールします。

```bash
$ brew install sass/sass/sass
```