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

**資料來源：**[**https://cowmanchiang.me/gitbook/gitbook/contents/how/emphasis.html**](https://cowmanchiang.me/gitbook/gitbook/contents/how/emphasis.html)

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

```HTML
<center>
    <img src="/assets/螢幕快照 2017-09-06 下午2.34.27.png"   alt="Cowman" style="border-radius:5px" width="240" height="180" border="10"/>
</center>
```

<center>
  <img src="/assets/螢幕快照 2017-09-06 下午2.34.27.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 3px rgba(0, 0, 0, 0.8)" width="240" height="180" border="10"/>
</center>



