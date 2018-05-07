# Json資料處理實例

---

## 連續取得Key值

接下來要教大家連續取得JsonObject如下方的數字Key值。

<center>
  <img src="/assets/JsonKeyValue.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 10px rgba(0, 0, 0, 0.4)" width="800" height="880" border="10"/>
</center>


主要是使用Interator，又可稱為"迭代器"，有點類似於ArrayList但又與ArrayList有些微上的不同，利用Interator的hasNext方法不斷地取得下一筆的Key值，但因為JsonObject必須使用try/catch防止例外狀況發生，但是這時你可能會想"instanceof"


``` Java
    Iterator <String> iterator = obj.keys();
        while (iterator.hasNext()) {
            String position = iterator.next();
            try {
                if(obj.get(position) instanceof JSONObject ){
                    dialogQuestion.add(obj.getJSONObject(position).getString("name") + " " +
                            obj.getJSONObject(position).getString("code"));
                }
            } catch (JSONException e) {
                Log.d("Json_ErrorMessage", String.valueOf(e));
            }
        }
    }
```



