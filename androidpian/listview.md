# ListView（活動列表）

---
ListView有很多種也是製作專案很常用到的東西，今天要講解的部分是稍微複雜的利用BaseAdapter來達成客製化的ListView。

## 定義Item物件

首先呢先在專案中創一個.xml想怎麼取名都可以，範例這邊呢就先叫item.xml好了。

那創立這xml主要是要定義這listView裡面每一列中有什麼物件以及物件位置，後續listView可藉由這xml來填入不同的資料。

接著我們在item.xml加入了imageView、textView、Button以及Guideline總共7個物件。

```
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">


    <ImageView
        android:id="@+id/item_imageView"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginBottom="32dp"
        android:layout_marginLeft="32dp"
        android:layout_marginRight="16dp"
        android:layout_marginTop="16dp"
        android:contentDescription=""
        app:layout_constraintBottom_toTopOf="@+id/guideline"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toLeftOf="@+id/guideline2"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.0"
        app:srcCompat="@mipmap/ic_launcher"
        tools:ignore="ContentDescription,RtlHardcoded" />

    <android.support.constraint.Guideline
        android:id="@+id/guideline"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_begin="107dp" />

    <TextView
        android:id="@+id/item_title"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginLeft="32dp"
        android:layout_marginTop="16dp"
        android:text="TextView"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintLeft_toLeftOf="@+id/guideline2"
        app:layout_constraintTop_toTopOf="parent"
        tools:ignore="HardcodedText,RtlHardcoded" />

    <TextView
        android:id="@+id/item_text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginLeft="32dp"
        android:layout_marginTop="16dp"
        android:text="TextView"
        app:layout_constraintLeft_toLeftOf="@+id/guideline2"
        app:layout_constraintTop_toBottomOf="@+id/item_title"
        tools:ignore="HardcodedText,RtlHardcoded" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="8dp"
        android:layout_marginRight="24dp"
        android:layout_marginTop="8dp"
        android:focusable="false"
        android:text="Button"
        app:layout_constraintBottom_toTopOf="@+id/guideline"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.511"
        tools:ignore="HardcodedText,RtlHardcoded" />

    <android.support.constraint.Guideline
        android:id="@+id/guideline2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_constraintGuide_end="277dp" />
</android.support.constraint.ConstraintLayout>
```

## \[注意\]

那這邊先提一個特別需要注意的地方是Button或是imageButton都會與OnItemClickListener搶焦點，你可能會發現怎麼點擊這Item都沒反應，這時就在物件內加入下面這行程式碼即可。

```java
android:focusable="false"
android:clickable="true"
```

或者你也可以在code中setFocusable\(false\)，像是下面這樣。

```Java
button.setFocusable(false);
```

# 建立Data

這裡先建立處理資料的class，處理像是Title，text，image等要置換的資料。將資料從MainActivity傳進StoreData內藉由StoreData傳至Adapter內，這裡先有個初步概念。

這裡這設計會傳入標題、內文及圖示，那如果有不同狀況可以依據進行調整。

```java
public class StroeData
{
    private String mTitle,mText;
    private int mIcon;

    public StroeData(String title, String text, int icon) {
        setTitle(title);
        setText(text);
        setIcon(icon);
    }

    //region ================================ GetMethod ============================================
    public String getTitle() {
        return mTitle;
    }

    public String getText() {
        return mText;
    }

    public int getIcon() {
        return mIcon;
    }
    //endregion

    //region ================================ SetMethod ============================================
    public void setTitle(String title) {
        this.mTitle = title;
    }

    public void setText(String text) {
        this.mText = text;
    }

    public void setIcon(int icon) {
        this.mIcon = icon;
    }
    //endregion
}
```






