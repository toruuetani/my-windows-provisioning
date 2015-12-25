# my-windows-provisioning
Windows10@BootCamp の設定方法


## 基本方針
- プログラム等は C ドライブにインストールする。
- データは Z ドライブ（ TrueCrypt にて作成した暗号化コンテナ）に保存する。


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



## Go
Go を https://golang.org/ からインストールしたら、環境変数 `GOPATH` を作成して `Z:\` に設定する。
さらに環境変数 `PATH` を `%PATH%;%GOPATH%\bin;` に設定する。



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


