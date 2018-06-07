# 程式碼混淆

---

程式碼混淆分為兩個區塊，首先需要對`build.gradle\(Module：app\)`進行基本的設定，可以參照下方設定。

* minifyEnable：是否混淆。
* zipAlignEnabled：是否壓縮。
* shrinkResources：是否移除無用的resources文件，可以減少APK的大小。
* proguardFiles：系統預設的android混淆文件，內文已經有基本的混淆聲明了`proguard-rules.pro`是可自定義的混淆一般皆在此做設定。

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



