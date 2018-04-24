# 其他

---

## TextView動態宣告

```java
public class StoreInformationFragment extends Fragment {

    private String[] id;
    private TextView[] textViews = new TextView[2];

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        view = inflater.inflate(R.layout.fragment_store_information, container, false);

        int temp;
        id = new String[]{"name", "address"};

        for(int i=0; i<id.length; i++){
           temp = getResources().getIdentifier(id[i], "id", getActivity().getPackageName());
           textViews[i] = (TextView)findViewById(temp);        
           textViews[i].setText("Text Changed");
        }

        return view;
        } 
    }
```

## 生成按鈕漸層設定Code

[連結請點我](http://angrytools.com/android/button/)



