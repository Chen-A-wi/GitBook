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

## 相機自動對焦

* FOCUS\_MODE\_CONTINUOUS\_PICTURE \(API level 14\)

  針對照相的連續自動對焦模式。  
  The speed of focus change is more aggressive than FOCUS\_MODE\_CONTINUOUS\_VIDEO.

* FOCUS\_MODE\_CONTINUOUS\_VIDEO \(API level 9\)

  針對錄影的連續自動對焦模式。  
  APP 仍然可以呼叫 takePicture\(\) 但不保證對焦已完成。

* FOCUS\_MODE\_AUTO \(API level 5\)

  APP 需要自己呼叫 autoFocus\(AutoFocusCallback\) 才會執行自動對焦。

由於是針對 Android 2.3 所寫的，所以不支援 FOCUS\_MODE\_CONTINUOUS\_PICTURE。

在 Android 4.0 以上的版本 FOCUS\_MODE\_CONTINUOUS\_PICTURE,FOCUS\_MODE\_CONTINUOUS\_VIDEO 模式下，APP 可以呼叫 autoFocus\(AutoFocusCallback\)，藉此可以得知是否對焦已完成。

```java
    @Override
    public void surfaceCreated(SurfaceHolder arg0) {
        try {
            mCamera = Camera.open();
            mCamera.setDisplayOrientation(90);
            mCamera.setPreviewDisplay(mSurfaceHolder);
        } catch (IOException e) {
            e.printStackTrace();
        } // set auto focus mode Camera.Parameters parameters = mCamera.getParameters();
        List<String> allFocus = parameters.getSupportedFocusModes();
        if (allFocus.contains(Camera.Parameters.FOCUS_MODE_CONTINUOUS_VIDEO)) {
            parameters.setFocusMode(Camera.Parameters.FOCUS_MODE_CONTINUOUS_VIDEO);
        } else if (allFocus.contains(Camera.Parameters.FLASH_MODE_AUTO)) {
            parameters.setFocusMode(Camera.Parameters.FOCUS_MODE_AUTO);
        }
        mCamera.setParameters(parameters);
        mCamera.startPreview();
    }
```

[參考連結](http://jyhshin.pixnet.net/blog/post/44014522-android-camera-demo-part-2-自動對焦)

