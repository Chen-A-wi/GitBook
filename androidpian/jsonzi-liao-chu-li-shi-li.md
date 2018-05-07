# Json資料處理實例

---

## 連續取得Key值

接下來要教大家連續取得JsonObject如下方的數字Key值。

<center>
  <img src="/assets/JsonKeyValue.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 10px rgba(0, 0, 0, 0.4)" width="800" height="880" border="10"/>
</center>

主要是使用Interator，又可稱為"迭代器"，有點類似於ArrayList但又與ArrayList有些微上的不同，利用Interator的hasNext方法不斷地取得下一筆的Key值，但因為JsonObject必須使用try/catch防止例外狀況發生，所以就會寫成如下方的code。

但是這時你可能會想"instanceof"這是代表什麼意思呢？因為code不知道你必須取得多少筆資料，也不知道取得下一筆的資料是否為所需的這時可使用"instanceof"來比對是否為先前的資料型態，詳細內容可以參考此[**[連結]**](https://teakki.com/p/57df75c31201d4c1629b8845)


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
                Log.e("Json_ErrorMessage", String.valueOf(e));
            }
        }
    }
```



