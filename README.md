# aito のダウンロード

**aito** は、自分の PC に入れて使う、ブログやお知らせサイトを作るためのアプリです。記事を書き、写真を入れ、「サイトに反映」ボタンで公開できます。ほかのソフトを別に入れる必要はありません。

このリポジトリは、aito の**配布用のファイルだけ**を置く場所です。ファイルは [Releases](https://github.com/ryuzi/aito-releases/releases) にあります。ソースコードはここにはありません。

---

## 入れ方・更新のしかた（おすすめ）

次の1行をコピーして貼り付け、Enter を押すだけです。2回目以降は、同じ1行で新しい版に更新できます。書いた記事などのデータは別の場所にあるので、更新しても消えません。管理者のパスワードは要りません。

**Windows** — スタートボタンを右クリックして「ターミナル」または「Windows PowerShell」を開き、次の1行を貼り付けます。

```powershell
irm https://github.com/ryuzi/aito-releases/releases/latest/download/install.ps1 | iex
```

**Mac** — 「アプリケーション」→「ユーティリティ」の「ターミナル」を開き、次の1行を貼り付けます。

```sh
curl -fsSL https://github.com/ryuzi/aito-releases/releases/latest/download/install.sh | sh
```

**Linux** も Mac と同じ1行で入ります。

この1行は、パソコンに合うファイルを選んでダウンロードし、壊れていないこと・書き換えられていないことを確かめてから入れ、aito を起動します。ブラウザに「はじめに」の画面が出れば完了です。名前とパスワード、サイト名などを決めると書き始められます。

## うまくいかないとき（予備の方法）

[最新のリリース](https://github.com/ryuzi/aito-releases/releases/latest) の「Assets」から、自分のパソコン用のファイルをダウンロードして使うこともできます。この方法では、まだ署名のないアプリのため警告が出ます。

| パソコン | ファイル | 開き方 |
| :--- | :--- | :--- |
| Windows | `aito-<版>-windows-amd64.zip`（ARM の PC は `windows-arm64`） | 展開して `aito.exe` をダブルクリックします。「Windows によって PC が保護されました」と出たら、「詳細情報」を押してから「実行」を押します。 |
| Mac | `aito-<版>-darwin-arm64.zip`（Intel の Mac は `darwin-amd64`） | 展開して `aito` をダブルクリックします。「開けません」と出たら、「システム設定」→「プライバシーとセキュリティ」を開き、「このまま開く」を押します。 |
| Linux | `aito-<版>-linux-amd64.tar.gz`（ARM は `linux-arm64`） | 展開して `aito` を実行します。 |

Windows 11 の「スマート アプリ コントロール」がオンのパソコンでは、署名のないアプリはどの方法でも開けません。

## 公開用のサーバーに入れる（上級者向け）

Ubuntu / Debian のサーバーでは、次の1行で公開専用の aito を入れられます。`--domain` と `--email` は自分のものに置き換えます。

```sh
curl -fsSL https://github.com/ryuzi/aito-releases/releases/latest/download/install-server.sh | sudo bash -s -- --domain www.example.com --email you@example.com
```

サーバーから GitHub に接続できないときは、リリースから `install-server.sh`・`aito-server-<版>-linux-<arch>.tar.gz`・`SHA256SUMS` の3つをダウンロードしてサーバーに送り、`--archive` を付けて実行します。

```sh
sudo bash install-server.sh --archive aito-server-<版>-linux-amd64.tar.gz --domain www.example.com --email you@example.com
```

## ファイルの確かめ方（上級者向け）

各リリースの `SHA256SUMS` に、全ファイルの SHA256 ハッシュがあります。1行で入れる方法では、この確認を自動で行います。

```sh
# Mac・Linux（ダウンロードしたファイルと SHA256SUMS を同じフォルダに置き、「OK」と出れば一致）
grep ' aito-<版>-linux-amd64.tar.gz$' SHA256SUMS | sha256sum -c -        # Linux
grep ' aito-<版>-darwin-arm64.zip$' SHA256SUMS | shasum -a 256 -c -      # Mac
```

```powershell
# Windows（表示された値が SHA256SUMS の同じファイル名の行と一致すれば OK）
Get-FileHash .\aito-<版>-windows-amd64.zip -Algorithm SHA256
```

## 版の決め方

版は `v<大きな変更>.<機能追加>.<修正>` の形です（例: `v0.1.0`）。`v1.0.0` までは、使い方が変わることがあります。各版で変わったことは、それぞれのリリースの説明に書いてあります。
