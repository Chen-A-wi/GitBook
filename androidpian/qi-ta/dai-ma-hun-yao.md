# 程式碼混淆

---

程式碼混淆包括了程式碼壓縮、程式碼混淆以及資源壓缩等優化过程。依靠 ProGuard，混淆流程將主項目以及依賴庫中未被使用的類型、方法、屬性移除，這有助於避開 64K 方法數的瓶頸，在Android 5.0之前隨著不斷增加新功能及引用新 Library 很可能遇到方法數超過數量限制的問題。此外同時，將類型、方法等重命名为無意義的簡短名稱，增加逆向工程難度。可依靠 Android 的 Gradle 插件，移除未被使用的資源，可有效减小 apk 大小。

## 基本混淆配置

一般在`build.gradle(Module: app)`的預設應該是如下方所預設，接著可以照著這一步步進行修改。

```java
android {
    ...
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    ...
}
```

將其修改成，下方所寫。

```java
android {
    ...
    buildTypes {
        release {
            // 混淆
            minifyEnabled true
            // 優化程式碼壓縮
            zipAlignEnabled true
            // 移除無用的resource文件
            shrinkResources true
            // 前一部分代表系统默認的android程序的混淆文件，該文件包含了基本的混淆聲明，後一个文件是自己的定義混淆文件
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    ...
}
```

接下來就可以進行混淆規則的撰寫了，可在Gradle Scripts找到`proguard-rules.pro(ProGuard Rules for app)`檔案進行自定義，這是開發者混淆手冊所提供通用於大部分的混淆規則，有需要可自行添加刪除。

```java
#指定壓縮级别
-optimizationpasses 5

#不跳過非公共庫的類成员
-dontskipnonpubliclibraryclassmembers

#混淆時採用的算法
-optimizations !code/simplification/arithmetic,!field/*,!class/merging/*

#混淆類中的方法名
-useuniqueclassmembernames

#優化時允許訪問並修改有修飾符的類和類的成員
-allowaccessmodification

#將文件来源重命名為“SourceFile”字符串
-renamesourcefileattribute SourceFile
#保留行號
-keepattributes SourceFile,LineNumberTable

#保持所有 Serializable 接口的類成员
-keepclassmembers class * implements java.io.Serializable {
    static final long serialVersionUID;
    private static final java.io.ObjectStreamField[] serialPersistentFields;
    private void writeObject(java.io.ObjectOutputStream);
    private void readObject(java.io.ObjectInputStream);
    java.lang.Object writeReplace();
    java.lang.Object readResolve();
}

#Fragment不需要在AndroidManifest.xml中注冊，需要額外保護下
-keep public class * extends android.support.v4.app.Fragment
-keep public class * extends android.app.Fragment

# 保持測試相關的代碼
-dontnote junit.framework.**
-dontnote junit.runner.**
-dontwarn android.test.**
-dontwarn android.support.test.**
-dontwarn org.junit.**
```

參考資料：

* [**写给 Android 开发者的混淆使用手册**](https://www.diycode.cc/topics/380)
* [**Android Proguard\(混淆\)**](https://www.jianshu.com/p/60e82aafcfd0)



