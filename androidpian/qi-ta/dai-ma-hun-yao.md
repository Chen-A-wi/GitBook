# 程式碼混淆

---

程式碼混淆包括了程式碼壓縮、程式碼混淆以及資源壓缩等優化过程。依靠 ProGuard，混淆流程將主項目以及依賴庫中未被使用的類型、方法、屬性移除，這有助於避開 64K 方法數的瓶頸，在Android 5.0之前隨著不斷增加新功能及引用新 Library 很可能遇到方法數超過數量限制的問題。此外同時，將類型、方法等重命名为無意義的簡短名稱，增加逆向工程難度。可依靠 Android 的 Gradle 插件，移除未被使用的資源，可有效减小 apk 大小。

## 基本混淆配置

一般在 `build.gradle(Module: app)` 的預設應該是如下方所預設，接著可以照著這一步步進行修改。

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

參考資料：
* [**写给 Android 开发者的混淆使用手册**](https://www.diycode.cc/topics/380)
* [**Android Proguard(混淆)**](https://www.jianshu.com/p/60e82aafcfd0)

