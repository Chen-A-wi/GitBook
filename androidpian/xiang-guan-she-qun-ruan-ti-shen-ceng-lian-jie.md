# 社群軟體深層連接

---

* ## Line

  利用intent帶文字進入Line選擇好友列表。

  ```java
  Intent intent = new Intent();
  intent.setAction(Intent.ACTION_VIEW);
  intent.setData(Uri.parse("line://msg/text/?" + "你想帶入的文字"));
  startActivity(intent);
  ```

  可直接跳入搜尋Line ID，userId帶入則可直接搜尋至指定好友。

  ```java
  String userId = findUserId();
  String sendText = "line://ti/p/~" + userId;
  Intent intent = null;
  try {
    intent = Intent.parseUri(sendText, Intent.URI_INTENT_SCHEME);
  } catch (URISyntaxException e) {
    e.printStackTrace();
  }
  startActivity(intent);
  ```



