# my-windows-provisioning
Windows10@BootCamp の設定方法


## 基本方針
- プログラム等は C ドライブにインストールする。
- データは Z ドライブ（ TrueCrypt にて作成した暗号化コンテナ）に保存する。
- 下記アプリはインストーラでインストールする。
 - [Adobe Acrobat Reader DC](https://get.adobe.com/jp/reader/)
 - [Atom](https://atom.io/) ※後述する Visual Studio Code でも可
 - [Google Chrome](https://www.google.co.jp/chrome/browser/desktop/)
 - [iTunes](http://www.apple.com/jp/itunes/download/)
 - [Launchy: The Open Source Keystroke Launcher](http://www.launchy.net/download.php)
 - [Lhaplus](http://forest.watch.impress.co.jp/library/software/lhaplus/)
 - [MacType](https://github.com/snowie2000/mactype/releases)
 - [Orchis](http://www.eonet.ne.jp/~gorota/)
 - [WinMerge 日本語版](http://www.geocities.co.jp/SiliconValley-SanJose/8165/winmerge.html)
 - [WinShot](http://forest.watch.impress.co.jp/library/software/winshot/)

## キーボード設定
Fnと同時押ししないとF1～F12が使えなくなるのでレジストリを変更する。
(最初からFnを同時押ししなくても良い場合も有り)
レジストリエディタを開き、 ```HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\KeyMagic``` のルートの ```OSXFnBehavior ``` の値、01を00に変更。

環境によっては ```ControlSet001``` の部分が ```ControlSet004``` だったりする。
更に、 ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\KeyMagic``` のルートにある ```OSXFnBehavior```  の値も、01を00に変更に変更。

キーボードの英数・かなをIMEのOFF・ONに割り当てる。
* 言語バーの [ツール] をクリックし、[プロパティ] をクリック。
* ［全般］タブをクリックし、［編集操作］セクションで［変更］ボタンをクリック。
* ［キー］カラムの［ひらがな］行の［入力/変換済み文字なし］カラムにある [ひらがなキー] を選択し、［変更］ボタンをクリック。
 * ［機能選択］ダイアログボックスで［IME-オン］を選択し、［OK］ボタンをクリック。
* ［キー］カラムの［無変換］行の［入力/変換済み文字なし］カラムにある [かな切替] を選択し、［変更］ボタンをクリック。
 * ［機能選択］ダイアログボックスで［IME-オフ］を選択し、［OK］ボタンをクリック。


## TrueCrypt Ver.7.1a
TrueCrypt 自体は開発が終了しているが、インストールは問題ない。
ただし、暗号化コンテナを作成してもエラーが出て使用できない。
これは `C:\Windows\System32\drivers\AppleHFS.sys` を `AppleHFS.sys.bkp` に
リネームして再起動すれば暗号化コンテナを作成できるようになる。

1. ボリューム作成
2. 暗号化されたファイルコンテナを作成
3. TrueCrypt標準ボリューム
4. ```C:\Works\AllWork.dat``` を選択
5. AES、RIPEMD-160選択
6. 40GB入力
7. NTFSを選択

作成したコンテナを Z: にマウントし、メニューから「お気に入り」->「選択したボリュームをログオン時にマウントする」
※以下の記述は Z: にマウントした状態を前提とする。


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



## Go
Go を https://golang.org/ からインストールしたら、環境変数 `GOPATH` を作成して `Z:\` に設定する。
さらに環境変数 `PATH` を `%PATH%;%GOPATH%\bin;` に設定する。


## Git
`go get` するには Git が不可欠なので https://git-scm.com/download/win からダウンロードしてインストールする。
また、ユーザー情報を下記のように設定しておく。
```
git config --global user.name "toruuetani"
git config --global user.email toruuetani __at__ gmail.com
```


## ghq
下記のコマンドを実行してインストールする。
```
go get github.com/motemen/ghq
```

設定ファイル `C:\Users\toru\.gitconfig` に ghq の設定を追記する。
```
[ghq]
  root = Z:/src
```

## SourceTree
メニューから「ツール」->「オプション」からプロジェクトフォルダを ```Z:\src\github.com\toruuetani``` にする。
マージを WinMerge でできるようにするため、設定ファイル `C:\Users\toru\.gitconfig` に WinMerge の設定を追記する。

```
[merge]
	tool = WinMerge
[mergetool "WinMerge"]
    cmd = \"C:/Program Files/WinMerge/WinMergeU.exe\" //e //u //wl //wr \"$LOCAL\" \"$BASE\" \"$REMOTE\" //o \"$MERGED\"
    trustExitCode = true
[diff]
	guitool = winmerge
[difftool "winmerge"]
	path = C:/Program Files/WinMerge/winmergeu.exe
	cmd = \"C:/Program Files/WinMerge/winmergeu.exe\" -e -u \"$LOCAL\" \"$REMOTE\"
```


## Visual Studio Code
```https://github.com/adobe-fonts/source-han-code-jp/archive/2.000R.zip``` をダウンロードしてインストールしておく。
メニューから File -> Preferences -> User Settings と選択し、 ```settings.json``` を以下のように編集する。
```
{
    "editor.fontFamily": "源ノ角ゴシック Code JP",
    "editor.fontSize": 14
}
```


## OneDrive
アンインストールは下記のコマンドで行う。

```
taskkill /f /im OneDrive.exe
%SystemRoot%\System32\OneDriveSetup.exe /uninstall  #32bitの場合
%SystemRoot%\SysWOW64\OneDriveSetup.exe /uninstall  #64bitの場合
```

レジストリエディタで下記を修正して、エクスプローラのナビから削除する。
```
キー：HKEY_CLASSES_ROOT\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}
エントリ：System.IsPinnedToNameSpaceTree (REG_DWORD)
値：0 (非表示)
```


