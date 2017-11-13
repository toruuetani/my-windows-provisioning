# my-windows-provisioning
Windows10@BootCamp の設定方法


## 基本方針
- プログラム等は C ドライブにインストールする。
- データは Z ドライブ（ VeraCrypt にて作成した暗号化コンテナ）に保存する。
- 各種データは OneDrive で同期し、同期先を `Z:\OneDrive` に変更する。


## キーボード設定
キーボードの英数・かなをIMEのOFF・ONに割り当てる。
* 言語バーの [ツール] をクリックし、[プロパティ] をクリック。
* ［全般］タブをクリックし、［編集操作］セクションで［変更］ボタンをクリック。
* ［キー］カラムの［ひらがな］行の［入力/変換済み文字なし］カラムにある [ひらがなキー] を選択し、［変更］ボタンをクリック。
 * ［機能選択］ダイアログボックスで［IME-オン］を選択し、［OK］ボタンをクリック。
* ［キー］カラムの［無変換］行の［入力/変換済み文字なし］カラムにある [かな切替] を選択し、［変更］ボタンをクリック。
 * ［機能選択］ダイアログボックスで［IME-オフ］を選択し、［OK］ボタンをクリック。


## アプリリスト
 - [Adobe Acrobat Reader DC](https://get.adobe.com/jp/reader/)
 - [Git](https://git-for-windows.github.io/)
 - [GitKraken](https://www.gitkraken.com/)
 - [Go](https://golang.org/dl/) ※C:\Go にインストールすること
 - [Google Chrome](https://www.google.co.jp/chrome/browser/desktop/)
 - [iTunes](http://www.apple.com/jp/itunes/download/)
 - [Launchy: The Open Source Keystroke Launcher](http://www.launchy.net/download.php)
 - [Lhaplus](http://forest.watch.impress.co.jp/library/software/lhaplus/)
 - [Orchis](http://www.eonet.ne.jp/~gorota/)
 - [WinMerge 日本語版](http://www.geocities.co.jp/SiliconValley-SanJose/8165/winmerge.html)
 - [WinShot](http://forest.watch.impress.co.jp/library/software/winshot/)

### OneDrive で同期するツール
- Z:\OneDrive\Tools\Cmder ・・・ [Cmder](http://cmder.net/)
- Z:\OneDrive\Tools\RLogin ・・・ [RLogin](http://nanno.dip.jp/softlib/man/rlogin/)
- Z:\OneDrive\Tools\WinSCP ・・・ [WinSCP](https://winscp.net/eng/docs/lang:jp)
- Z:\OneDrive\Tools\Wmv ・・・ [AGDRec](http://t-ishii.la.coocan.jp/download/AGDRec.html)


## 環境変数
GOPATH=Z:\ を追加する。
PATH設定に下記ディレクトリを追加する。
- %GOPATH%\bin
- Z:\OneDrive\Tools\Bin


## Cisco VPN Client Ver.5.0.07.0440
Windows10 には対応してないため、そのままではインストールできない。
```
Error 27850  Unable to manage networking component. 
Operatin system corruptioin may be preventing installation. 
```

以下の手順に従う。

1. ftp://files.citrix.com/winfix.exe から winfix.exe をダウンロードして実行
1. ftp://files.citrix.com/dneupdate64.msi から dneupdate64.msi をダウンロードして実行
1. vpnclient_setup.msi を右クリックして 互換性をWindows 7に設定しておく。
1. vpnclient_setup.msi を実行

ここまででインストールは可能になるが、コネクションを確立しようとしてもエラーになる。
```
Secure VPN Connection terminated locally by the Client.
Reason 442: Failed to enable Virtual Adapter.
```

1. これは以下の手順で回避可能。
1. レジストリエディタを起動
1. `HKLM\SYSTEM\CurrentControlSet\Services\CVirtA` の `DisplayName` の値を
   `Cisco Systems VPN Adapter for 64-bit Windows` に変更
1. 再起動


## go ライブラリ
`go-get.bat` を実行して必須ライブラリをインストールする。


## Visual Studio Code 設定
```https://github.com/adobe-fonts/source-han-code-jp/archive/2.000R.zip``` をダウンロードしてインストールしておく。
メニューから File -> Preferences -> User Settings と選択し、 ```settings.json``` を以下のように編集する。
```
{
    "editor.fontFamily": "'Myrica M', Consolas, 'Courier New', monospace",
    "editor.fontSize": 15,
    "workbench.editor.enablePreview": false
}
```
