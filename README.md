# my-windows-provisioning
Windows10@BootCamp の設定方法


## 基本方針
* プログラム等は C ドライブにインストールする。
* データは Z ドライブ（ [VeraCrypt](https://www.veracrypt.fr/en/Downloads.html) にて作成した暗号化コンテナ）に保存する。
  * コンテナが作成できない場合 ```C:\windows\system32\drivers``` にある ```applehfs.sys``` を ```applehfs-old.sys``` にリネームする。
  * 暗号化ファイルコンテナは `C:\Works\AllWorks` とする。
  * ファイルシステムは NTFS とすること。


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
scoop install ^
  ghq ^
  gitkraken ^
  go ^
  greenshot ^
  jq ^
  launchy ^
  mysql-workbench ^
  nvm ^
  peco ^
  pwsh ^
  sudo ^
  vscode ^
  windows-terminal ^
  winscp
```

### Git 設定
```
git config --global core.autocrlf false
git config --global ghq.root z:\src
```

### Go 設定
環境変数に GOPATH=Z:\ を追加する。
PATH設定に下記ディレクトリを追加する。
- %GOPATH%\bin

### Greenshot 設定
* Capture region に ```Control+Shift+F12``` にアサインする

### Launchy 設定
* カタログに以下を追加 ※実行可能ファイルも含むにチェックすること
  * C:\ProgramData\Microsoft\Windows\Start Menu
  * %APPDATA%\Microsoft\Windows\Start Menu\Programs
* スタートアップ登録
  * ```C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Scoop Apps``` にあるショートカットをコピー
  * エクスプローラーで ```shell:startup``` を入力して表示されるフォルダにペースト

### Visual Studio Code 設定
設定は公式の同期を使用する。アカウントは GitHub を利用すること。
右クリックで開けるように ```%USERPROFILE%\scoop\apps\vscode\current\vscode-install-context.reg``` を実行する。

## アプリのインストール
以下のアプリは手動でインストールする。

  - [Google Chrome](https://www.google.co.jp/chrome/browser/desktop/)
  - [Trackpad++](http://trackpad.forbootcamp.org/#download)
- 開発用
  - [Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/install/)
- ユーティリティ
  - [Adobe Acrobat Reader DC](https://get.adobe.com/jp/reader/)
  - [iTunes - Microsoft Store](https://www.microsoft.com/ja-jp/p/itunes/9pb2mz1zmb1s?cid=appledotcom&rtc=1&activetab=pivot:overviewtab)



