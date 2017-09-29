# Map

---

Map又稱關聯式陣列\(Associative Array\)是一種使用key-value pair的方式來存取資料的資料結構。

## **HashMap**

基本上在使用map時，若無其它考量，則應該優先使用HashMap，因其存取資料的時間複雜度可以達到常數時間，非常地快。

另外較特別的是HashMap允許鍵值\(key\)為null。

```java
Map<String,String> hashMap = new HashMap<String, String>();

hashMap.put("2","Tue");
hashMap.put("3","Wed");
hashMap.put("1","Mon");
hashMap.put("4","Thu");
hashMap.put("5","Fri");

for (Map.Entry<String,String> entry:hashMap.entrySet()) {
    System.out.println(entry.getKey()+"   "+entry.getValue());
}
```

從輸出結果中我們可以看到，hashMap輸出key時，並沒有依照插入時的順序，也沒有依照Key或是Value所排序，所以我們若需要有排序功能的map時，不能選擇HashMap。

<center>
  <img src="/assets/HashMap Log.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 10px rgba(0, 0, 0, 0.4)" width="400" height="100" border="10"/>
</center>


