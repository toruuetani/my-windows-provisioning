# my-windows-provisioning
Windows10@BootCamp の設定方法


## 基本方針
* プログラム等は C ドライブにインストールする。
* データは Z ドライブ（ [VeraCrypt](https://www.veracrypt.fr/en/Downloads.html) にて作成した暗号化コンテナ）に保存する。
  * 不具合解消のため ```C:\windows\system32\drivers``` にある ```applehfs.sys``` を `applehfs-old.sys``` にリネームする。
  * 暗号化ファイルコンテナは `C:\Works\AllWorks` とする。
  * ファイルシステムは NTFS とすること。
* 各種データは OneDrive で同期し、同期先を `Z:\OneDrive` に変更する。


## キーボード設定
キーボードの英数・かなをIMEのOFF・ONに割り当てる。


## ドライバ
Apple Super Drive を使用するため、下記ドライバをインストールする。
- Z:\OneDrive\Configuration\BootCamp\AppleODDInstaller64.exe


## アプリのインストール by Scoop
アプリは [Scoop](https://scoop.sh/) でインストールする。
ただし、後述するアプリは手動でインストールして Scoop では管理しない。

まずは powershell を管理者権限で起動し、以下のコマンドを入力する。

```
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
scoop install git
scoop bucket add extras
```

次に以下のコマンドでアプリをインストールする。

```
scoop install gitkraken
scoop install go
scoop install greenshot
scoop install launchy
scoop install windows-terminal
```

### Greenshot 設定
* Capture region に ```Control+Shift+F12``` にアサインする


## アプリのインストール
自動更新の機能を持つ以下のアプリは手動でインストールする。

  - [Google Chrome](https://www.google.co.jp/chrome/browser/desktop/)
  - [Trackpad++](http://trackpad.forbootcamp.org/#download)
- 開発用
  - [Visual Studio Code](https://code.visualstudio.com/download)
    - User Installer をダウンロードする
    - ```C:\VSCode``` にインストールする
- ユーティリティ
  - [Adobe Acrobat Reader DC](https://get.adobe.com/jp/reader/)
  - [iTunes - Microsoft Store](https://www.microsoft.com/ja-jp/p/itunes/9pb2mz1zmb1s?cid=appledotcom&rtc=1&activetab=pivot:overviewtab)


### OneDrive で同期するツール
これらは実行ファイル右クリックで「スタートにピン留めする」
- Z:\OneDrive\Tools\RLogin ・・・ [RLogin](http://nanno.dip.jp/softlib/man/rlogin/)
- Z:\OneDrive\Tools\WinSCP ・・・ [WinSCP](https://winscp.net/eng/docs/lang:jp)
- Z:\OneDrive\Tools\Wmv ・・・ [AGDRec](http://t-ishii.la.coocan.jp/download/AGDRec.html)


## 環境変数
GOPATH=Z:\ を追加する。
PATH設定に下記ディレクトリを追加する。
- %GOPATH%\bin
- %OneDrive%\Tools\Bin


## go ライブラリ
```
go get github.com/motemen/ghq
go get github.com/peco/peco
```

## Visual Studio Code 設定
拡張機能 `settings sync` をインストールする。 github token と gist ID を準備すること。
再起動後、 Visual Studio Code の画面で Shift + Alt + D を押して設定をダウンロードする。


