# Gitbook撰寫技巧

---

## 強調

* 斜體，使用 "\*" 或 "\_" 將文字包起起來強調，這是斜體

  ```
 *強調，這是斜體*

  _強調，這也是斜體_
  ```

  _強調，這是斜體_

  _強調，這也是斜體_

* 粗體，使用 "\*\*" 或 "\_\_" 將文字包起起來

  ```
  **強調，這是粗體**

  __強調，這也是粗體__
  ```

  **強調，這是粗體**

  **強調，這也是粗體**

* 粗斜體，使用 "_\*_" 或 "_\__" 將文字包起起來

  ```
  ***強調，這是粗斜體***

  ___強調，這也是粗斜體___
  ```

  _**強調，這是粗斜體**_

  _**強調，這也是粗斜體**_

##內崁HTML語法
可以在Markdown中使用HTML語法來輔助顯示效果，如下先置中再更改字體顏色。

```HTML
<center>
  <font color="red">aaa</font>
</center>
```
<center>
  <font color="red">aaa</font>
</center>

*  使用HTML內崁圖片，含置中及圓角設定。

** 陰影說明：**以上面的例子來說，參數的所有數值從左到右代表了：水平偏移，垂直偏移，陰影模糊距離（陰影顏色、明度）， **透明度：**0 →完全透明， 1 →完全不透明。

```HTML
<center>
  <img src="/assets/test.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 10px rgba(0, 0, 0, 0.4)" width="240" height="180" border="10"/>
</center>
```

<center>
  <img src="/assets/test.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 10px rgba(0, 0, 0, 0.4)" width="240" height="180" border="10"/>
</center>

參考資料：[**Cowman's Gitbook site**](https://cowmanchiang.me/gitbook/gitbook/contents/how/emphasis.html)
