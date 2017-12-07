### 崩溃日志 iOS .crash文件处理 symbolicatecrash
```
1.find /Applications/Xcode.app -name symbolicatecrash -type f
2.cp   /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/PrivateFrameworks/DTDeviceKitBase.framework/Versions/A/Resources /symbolicatecrash /data/crash   
3. Xcode>Window>Organize在Archives找到上传的App－右击－Show in Finder 右击后显示包内容 复制ProjectName.app和ProjectName.app.dSYM到crash文件夹里  

4. export DEVELOPER_DIR="/Applications/XCode.app/Contents/Developer"

5. ./symbolicatecrash /Users/XXX/Desktop/crach/crashLog.txt /Users/XXX/Desktop/crach/ProjectName.app.dSYM > crashLogEnd.crash
```
