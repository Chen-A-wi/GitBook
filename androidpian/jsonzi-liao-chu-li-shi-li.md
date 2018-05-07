# Json資料處理實例

---

## 連續取得Key值

接下來要教大家連續取得JsonObject如下方的數字Key值。

<center>
  <img src="/assets/JsonKeyValue.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 10px rgba(0, 0, 0, 0.4)" width="800" height="880" border="10"/>
</center>

```Java
Iterator <String> iterator = obj.keys();
        while (iterator.hasNext()) {
            String position = iterator.next();
            if(obj.get(position) instanceof JSONObject ){
                dialogQuestion.add(obj.getJSONObject(position).getString("name") + " " +
                        obj.getJSONObject(position).getString("code"));
            }

        }
```



