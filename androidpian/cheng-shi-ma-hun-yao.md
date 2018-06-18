# 程式碼混淆

---

程式碼混淆分為兩個區塊，首先需要對`build.gradle(Module：app)`進行基本的設定，可以參照下方設定。

* minifyEnable：是否混淆。
* zipAlignEnabled：是否壓縮。
* shrinkResources：是否移除無用的resources文件，可以減少APK的大小。
* proguardFiles：系統預設的android混淆文件，內文已經有基本的混淆聲明了`proguard-rules.pro`是可自定義的一般皆在此做設定。

```java
android {
    ...
    buildTypes {
        release {
            // 混淆
            minifyEnabled true
            // Zipalign優化
            zipAlignEnabled true
            // 移除無用的resource文件
            shrinkResources true
            // 前一部分代表系统默認的android程序的混淆文件，該文件已经包含了基本的混淆聲明，後一个文件是自己的定義混淆文件
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    ...
}
```

接著我們來看看進階點的`proguard-rules.pro`裡面的設定，下面這是適應大部分專案的自定義設定。

```java
# Add project specific ProGuard rules here.
# By default, the flags in this file are appended to flags specified
# in C:\Users\Bang\AppData\Local\Android\sdk/tools/proguard/proguard-android.txt
# You can edit the include path and order by changing the proguardFiles
# directive in build.gradle.
#
# For more details, see
#   http://developer.android.com/guide/developing/tools/proguard.html

# Add any project specific keep options here:

# If your project uses WebView with JS, uncomment the following
# and specify the fully qualified class name to the JavaScript interface
# class:
#-keepclassmembers class fqcn.of.javascript.interface.for.webview {
#   public *;
#}
#

# 代碼混淆壓縮比，一般在0~7之間，預設為5一般這不做調整。
-optimizationpasses 5

# 混合時不用大小寫混合，混合後的類別名為小寫。
-dontusemixedcaseclassnames

# 指定不去忽略非公共庫的類別。
-dontskipnonpubliclibraryclasses

# 這句話能夠使我們的項目混淆後產生映射文件。
# 包含有類別名->混淆後類別名的映射關係。
-verbose

# 指定不忽略非公共庫的類別。
-dontskipnonpubliclibraryclassmembers

# 不做預校驗，preverify是proguard的四個步驟之一，Android不需要preverify，去掉這一步能夠加快混淆速度。
-dontpreverify

# 保留Annotation不混淆。
-keepattributes *Annotation*,InnerClasses

# 避免混淆泛型。
-keepattributes Signature

# 異常時保留顯示行號。
-keepattributes SourceFile,LineNumberTable

# 指定混淆採用的算法，後面的參數是個過濾器。
# 此過濾器事google推薦的算法一般不做更改。
-optimizations !code/simplification/cast,!field/*,!class/merging/*

# 保留我們使用的四大组件，自定義的Application等等這些類別不被混淆。
# 因為这些子類別都有可能被外部調用。
-keep public class * extends android.app.Activity
-keep public class * extends android.app.Appliction
-keep public class * extends android.app.Service
-keep public class * extends android.content.BroadcastReceiver
-keep public class * extends android.content.ContentProvider
-keep public class * extends android.app.backup.BackupAgentHelper
-keep public class * extends android.preference.Preference
-keep public class * extends android.view.View
-keep public class com.android.vending.licensing.ILicensingService


# 保留support下的所有類別。
-keep class android.support.** {*;}

# 保留繼承。
-keep public class * extends android.support.v4.**
-keep public class * extends android.support.v7.**
-keep public class * extends android.support.annotation.**

# 保留R下面的資源。
-keep class **.R$* {*;}

# 保留本地native方法不被混淆。
-keepclasseswithmembernames class * {
    native <methods>;
}

# 保留在Activity中的方法参数是view的方法，
# 這樣以来我們在layout中寫的onClick就不會被影響。
-keepclassmembers class * extends android.app.Activity{
    public void *(android.view.View);
}

# 保留列舉類不被混淆。
-keepclassmembers enum * {
    public static **[] values();
    public static ** valueOf(java.lang.String);
}

# 保留我们自定义控件（继承自View）不被混淆
-keep public class * extends android.view.View{
    *** get*();
    void set*(***);
    public <init>(android.content.Context);
    public <init>(android.content.Context, android.util.AttributeSet);
    public <init>(android.content.Context, android.util.AttributeSet, int);
}

# 保留Parcelable序列化類別不被混淆。
-keep class * implements android.os.Parcelable {
    public static final android.os.Parcelable$Creator *;
}

# 保留Serializable序列化的類別不被混淆。
-keepclassmembers class * implements java.io.Serializable {
    static final long serialVersionUID;
    private static final java.io.ObjectStreamField[] serialPersistentFields;
    !static !transient <fields>;
    !private <fields>;
    !private <methods>;
    private void writeObject(java.io.ObjectOutputStream);
    private void readObject(java.io.ObjectInputStream);
    java.lang.Object writeReplace();
    java.lang.Object readResolve();
}

# 對於帶有回調函數的onXXEvent、**On*Listener的，不能被混淆。
-keepclassmembers class * {
    void *(**On*Event);
    void *(**On*Listener);
}

# webView處理，如未使用到webView忽略即可。
-keepclassmembers class fqcn.of.javascript.interface.for.webview {
    public *;
}
-keepclassmembers class * extends android.webkit.webViewClient {
    public void *(android.webkit.WebView, java.lang.String, android.graphics.Bitmap);
    public boolean *(android.webkit.WebView, java.lang.String);
}
-keepclassmembers class * extends android.webkit.webViewClient {
    public void *(android.webkit.webView, jav.lang.String);
}
```

## 注意

寫到這裡你可能就會開始進行Buliding了但你會發現一件事，這在debug下是可以進行編譯的但是你想進一步編譯成APK進行上架時可能會發現怎麼會行不通呢？這作者是不是又欺騙我的感情了呢？

這是因為你實作時可能會加入第三方Library那這時，常見在程式碼轉譯成APK時會找不到第三方的方法類別等可以[參考此處](https://www.cnblogs.com/renkangke/archive/2013/05/31/3110635.html)。

所以當你引進3、4個第三方的Library時這些錯誤數量就如下圖很可觀的，這時也別擔心慢慢解開來即可。

我目前下述okhttp的錯誤是先使用-dontwarn忽略的，如右側`-dontwarn okhttp3.**`。

<center>
  <img src="/assets/Obfuscated_Code_Error.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 10px rgba(0, 0, 0, 0.4)" width="400" height="180" border="10"/>
</center>

[**參考資料**](https://blog.csdn.net/Two_Water/article/details/70233983)

