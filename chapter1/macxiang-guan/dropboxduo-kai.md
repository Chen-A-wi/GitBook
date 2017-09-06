# Dropbox多開

---

## 建立Dropbox

首先開啟Launchpad，應該會在其他資料夾中看到Terminal，接著打開它，輸入bash。

```
bash
```

完成後接著輸入下面的指令。

```
HOME=/Users/$USER/.dropbox-alt /Applications/Dropbox.app/Contents/MacOS/Dropbox
```

稍後Terminal執行，執行完後會跳出Dropbox之後依指示操作即可登入，Dropbox 資料夾將建立於帳號 Home 目錄下的 .dropbox-alt 資料夾內，如果需要再增加第三個Dropbox那在code裡的 .dropbox-alt 全改成 .dropbox-alt2以此類推即可。

## 建立啟動程式

再來需為第二個Dropbox建立啟動建立啟動程式，相信我你不會希望每次都藉由Terminal來啟動的，接著在Terminal輸入下面指令。

```
mkdir -p /Users/$USER/Applications/DropboxAltStarter.app/Contents/MacOS/

cat <<EOF >/Users/$USER/Applications/DropboxAltStarter.app/Contents/Info.plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
<key>CFBundlePackageType</key>
<string>APPL</string>
<key>CFBundleExecutable</key>
<string>DropboxAltStarter</string>
<key>LSUIElement</key>
<string>1</string>
</dict>
</plist>
EOF

cat <<EOF >/Users/$USER/Applications/DropboxAltStarter.app/Contents/MacOS/DropboxAltStarter
#!/bin/bash
# Assumes you have Dropbox in /Applications
HOME=/Users/$USER/.dropbox-alt /Applications/Dropbox.app/Contents/MacOS/Dropbox
EOF

chmod 755 /Users/$USER/Applications/DropboxAltStarter.app/Contents/MacOS/DropboxAltStarter
```

結束後，啟動程式 DropboxAltStarter 將建立於帳號 Home 目錄下的 Applications 裡。這裡如果需要建立第三個以上Dropbox也是將DropboxAltStarter.app 全改成 DropboxAltStarter2.app以此類推。

## 設定啟動程式

建立完啟動程式後可以去 系統偏好設定 =&gt; 使用者與群組 =&gt; 登入選項 將DropboxAltStarter加入即可。

## 實現Dropbox外同步備份

若想備份許多舊資料夾，方法之一是將它們全移到 Dropbox 裡。另外一個方法則不必移動資料夾，而是在 Dropbox 裡建立這些資料夾的分身捷徑。但分身建立方式必須是 Unix 式的 symbolic link，直接在 Mac 桌面視窗裡來增加捷徑並無法實際備份。

建立 symbolic link 須在 Terminal 裡輸入指令「ln -s」。指令範例：

```
ln -s /path/folder1 /Users/MKnight/Dropbox/folder2
```

其中 folder1 是本尊，folder2 是欲建立的分身命名。不只資料夾，分身指令對檔案也同樣有效。（更便利、不需經 Terminal 來建立 symbolic link 的方法：安裝右鍵選單SymbolicLinker。）

快速輸入本尊、分身路徑的方法是直接將資料夾用滑鼠拖入 Terminal 視窗裡。

### \[注意\]

1. Symbolic link 只能單向同步備份，意指：如果網路或遠端電腦更改了該分身，該分身在本端電腦上就會變回尋常資料夾。所以 Symbolic link 只適用於備份與單向分享。

2. Symbolic link 的右鍵選單無法出現 Dropbox 功能選項。

3. 以上問題皆可能在不久的將來被解決，因為官方已同意增加「同步鍊結 Dropbox 外資料夾」的功能。

#### 邀請連結

如果覺得不錯的話可以點選下方的邀請連結

[https://db.tt/KU7cXXJQ](https://db.tt/KU7cXXJQ)

參考資料：[《姆奈》MKnight：Dropbox 在 Mac 上的密技](http://mkhere.blogspot.tw/2010/03/dropbox-mac.html)

