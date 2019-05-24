# my-windows-provisioning
Windows10@BootCamp の設定方法


## 基本方針
- プログラム等は C ドライブにインストールする。
- データは Z ドライブ（ [VeraCrypt](https://www.veracrypt.fr/en/Downloads.html) にて作成した暗号化コンテナ）に保存する。
 - 暗号化ファイルコンテナは `C:\Works\AllWorks` とする。
 - ファイルシステムは NTFS とすること。
- 各種データは OneDrive で同期し、同期先を `Z:\OneDrive` に変更する。


## キーボード設定
キーボードの英数・かなをIMEのOFF・ONに割り当てる。
* 言語バーの [ツール] をクリックし、[プロパティ] をクリック。
* ［全般］タブをクリックし、［編集操作］セクションで［変更］ボタンをクリック。
* ［キー］カラムの［ひらがな］行の［入力/変換済み文字なし］カラムにある [ひらがなキー] を選択し、［変更］ボタンをクリック。
 * ［機能選択］ダイアログボックスで［IME-オン］を選択し、［OK］ボタンをクリック。
* ［キー］カラムの［無変換］行の［入力/変換済み文字なし］カラムにある [かな切替] を選択し、［変更］ボタンをクリック。
 * ［機能選択］ダイアログボックスで［IME-オフ］を選択し、［OK］ボタンをクリック。


## ドライバ
Apple Super Drive を使用するため、下記ドライバをインストールする。
- Z:\OneDrive\Configuration\BootCamp\AppleODDInstaller64.exe

## アプリリスト
- 最初にインストール
  - [Google Chrome](https://www.google.co.jp/chrome/browser/desktop/)
  - [Launchy: The Open Source Keystroke Launcher](http://www.launchy.net/download.php)
  - [Trackpad++](http://trackpad.forbootcamp.org/#download)
- 開発用
  - [Git](https://git-for-windows.github.io/)
  - [GitKraken](https://www.gitkraken.com/)
  - [Go](https://golang.org/dl/) ※C:\Go にインストールすること
  - [Visual Studio Code](https://code.visualstudio.com/download)
- ユーティリティ
  - [Adobe Acrobat Reader DC](https://get.adobe.com/jp/reader/)
  - [iTunes](http://www.apple.com/jp/itunes/download/)
  - [7-Zip](https://sevenzip.osdn.jp/)
  - [Orchis](http://www.eonet.ne.jp/~gorota/)
  - [WinShot](http://forest.watch.impress.co.jp/library/software/winshot/)

### OneDrive で同期するツール
これらは実行ファイル右クリックで「スタートにピン留めする」
- Z:\OneDrive\Tools\Cmder ・・・ [Cmder](http://cmder.net/)
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


