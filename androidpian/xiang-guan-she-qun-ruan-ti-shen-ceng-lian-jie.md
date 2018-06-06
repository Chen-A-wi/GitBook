# 社群軟體深層連接\(URL scheme\)

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

  更多資訊可以參考[**Line Developer**](https://developers.line.me/en/docs/messaging-api/using-line-url-scheme/#sending-text-messages)

* ## Facebook Messenger

  分享特定網址致朋友列表，`external-link`的部分可以自行替換成讀者所想分享的網址。

  ```java
  Intent intentFB = new Intent();
  intentFB.setAction(Intent.ACTION_VIEW);
  intentFB.setData(Uri.parse("fb-messenger://share?link=external-link&app_id=appid"));
  startActivity(intentFB);
  ```

  更多資訊可以參考[**The Simplest Way to Share Messages on Social Network from Web App**](https://medium.com/@balaji.sankar/the-simplest-way-to-share-messages-on-social-network-from-web-app-e349f5701e7f)



