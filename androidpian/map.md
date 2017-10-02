# Map

---

Map又稱關聯式陣列\(Associative Array\)是一種使用key-value pair的方式來存取資料的資料結構。

## **HashMap**

基本上在使用map時，若無其它考量，則應該優先使用HashMap，因其存取資料的時間複雜度可以達到常數時間，非常地快。

特色：

1. HashMap允許鍵值(key)為null。

2. 排序不會依照放入順序或者自然排序(Natural Ordering)，採用系統自動放入，所以不保證其順序。

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
  <img src="/assets/HashMap Log.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 10px rgba(0, 0, 0, 0.4)" width="500" height="100" border="10"/>
</center>

##LinkedHashMap

LinkedHashMap內部是用linked list來維護其順序性，所以在iterate時其結果乃是依照元素的插入順序或最近最少使用(least-recently-used)順序。在使用上其與hashmap相似，速度只稍差些；但在iterate時卻是比hashmap還來得快。

特色：

1. 其放入順序是依Code所put的順序進行排列。

```java
Map<String, String> linkedHashMap = new LinkedHashMap<String, String>();

linkedHashMap.put("2", "Tue");
linkedHashMap.put("3", "Wed");
linkedHashMap.put("1", "Mon");
linkedHashMap.put("4", "Thu");
linkedHashMap.put("5", "Fri");

for (Map.Entry<String, String> entry : linkedHashMap.entrySet()) {
    System.out.println(entry.getKey() + "   " + entry.getValue());
}
```

可以看到輸出結果與code所put順序一樣。

<center>
  <img src="/assets/LinkedHashMap Log.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 10px rgba(0, 0, 0, 0.4)" width="400" height="100" border="10"/>
</center>

##TreeMap

其特點是其key set或key-value pair是有順序性的，而順序為自然排序(Natural Ordering)或是由所傳入的comparator來決定。另外TreeMap也是唯一提供submap()函式的map。

```java
Map<String, String> treeMap= new TreeMap<String,String> ();

treeMap.put("2", "Tue");
treeMap.put("3", "Wed");
treeMap.put("1", "Mon");
treeMap.put("4", "Thu");
treeMap.put("5", "Fri");

for (Map.Entry<String, String> entry : treeMap.entrySet()) {
    System.out.println(entry.getKey() + "   " + entry.getValue());
}

System.out.println("----------by comparator");

treeMap = new TreeMap<String,String> (new Comparator<String>() {
    public int compare(String o1, String o2) {
        return o2.compareTo(o1);
    }
});

treeMap.put("2", "Tue");
treeMap.put("3", "Wed");
treeMap.put("1", "Mon");
treeMap.put("4", "Thu");
treeMap.put("5", "Fri");

for (Map.Entry<String, String> entry : treeMap.entrySet()) {
    System.out.println(entry.getKey() + "   " + entry.getValue());
}
```
<center>
  <img src="/assets/TreeMap Log.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 10px rgba(0, 0, 0, 0.4)" width="550" height="300" border="10"/>
</center>

##EnumMap

特別之處在於只接受列舉(Enumeration)為Key，也因其只接受列舉為key，不像HashMap能接受各種型態的物件作為key，故在實作上能特地為此種情況最佳化。

EnumMap的好處可以從效率上及使用上來描述：技術上，由於EnumMap內部使用Array來實作；另外因不需用呼叫hashcode函式，故其也不會產生collision的問題；所以在同是key為enum的情況下，EnumMap的效能是好過HashMap的。

特色：

1. 不接受null為key。

2. 以Natural Ordering的方式來儲存Key。

3. 效能比HashMap稍好些。

```java
private Map<Keys, String> enumMap = new EnumMap<Keys, String>(Keys.class);

enum Keys {
    A(1), B(2), C(3), D(4), E(5);

    private int code;

    private Keys(int code) {
        this.code = code;
    }

    public int getCode() {
        return this.code;
    }
}

private void enumMap() {
    System.out.println("======= EnumMap =======");

    enumMap.put(Keys.B, "Tue");
    enumMap.put(Keys.C, "Wed");
    enumMap.put(Keys.A, "Mon");
    enumMap.put(Keys.D, "Thu");
    enumMap.put(Keys.E, "Fri");

    for (Map.Entry<Keys, String> entry: enumMap.entrySet()) {
        System.out.println(entry.getKey()+" "+entry.getKey().getCode()+" "+entry.getValue());
    }
}
```

可看到輸出的順序為key按照自然排序法(Natural Ordering)排序。

<center>
  <img src="/assets/EnumMap Log.png" alt="Cowman" style="border-radius:5px; box-shadow:5px 5px 10px rgba(0, 0, 0, 0.4)" width="400" height="150" border="10"/>
</center>
