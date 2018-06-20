# 取得經緯度

---

取得經緯度分為兩種方式一種為透過網路取得`NETWORK_PROVIDER`另一種則是透過GPS`GPS_PROVIDER`取得，稍等會詳加介紹。

首先必須先進行權限的宣告分為下列兩點，讀者可以選擇自身適宜的或是保險些全加入AndroidManifest。
*  **ACCESS_COARSE_LOCATION：**使用基地台訊號強弱進行三角定位，因此很容易受到建築物折射等外在的訊號干擾，所以僅能進行粗略的定位。

* **ACCESS_FINE_LOCATION：**使用GPS進行精確的定位，因此手機必須有GPS功能，也由於藉由衛星定位準度也高出許多。

```java
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

```java
public class LocationUtils {
    private volatile static LocationUtils uniqueInstance;
    private LocationManager locationManager;
    private String locationProvider;
    private Location location;
    private Context mContext;

    private LocationUtils(Context context) {
        mContext = context;
        getLocation();
    }

    public static LocationUtils getInstance(Context context) {
        if (uniqueInstance == null) {
            synchronized (LocationUtils.class) {
                if (uniqueInstance == null) {
                    uniqueInstance = new LocationUtils(context);
                }
            }
        }
        return uniqueInstance;
    }

    private void getLocation() {
        locationManager = (LocationManager) mContext.getSystemService(Context.LOCATION_SERVICE);
        List<String> providers = locationManager.getProviders(true);
        if (providers.contains(LocationManager.NETWORK_PROVIDER)) {
            Log.d("LocationUtils", "網路定位");
            locationProvider = LocationManager.NETWORK_PROVIDER;
        } else if (providers.contains(LocationManager.GPS_PROVIDER)) {
            Log.d("LocationUtils", "GPS定位");
            locationProvider = LocationManager.GPS_PROVIDER;
        } else {
            Log.d("LocationUtils", "没有可用的定位");
            return;
        }
        if (Build.VERSION.SDK_INT >= 23 && 
        ActivityCompat.checkSelfPermission(mContext, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED && 
        ActivityCompat.checkSelfPermission(mContext, Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
            return;
        }
        if (ActivityCompat.checkSelfPermission(mContext, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED && 
        ActivityCompat.checkSelfPermission(mContext, Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
            return;
        }
        Location location = locationManager.getLastKnownLocation(locationProvider);
        if (location != null) {
            setLocation(location);
        }
        // 監聽位置，第二和第三參數分別為更新的最短時間minTime和最短距離minDistace
        locationManager.requestLocationUpdates(locationProvider, 0, 0, locationListener);
    }

    private void setLocation(Location location) {
        this.location = location;
        String address = "緯度：" + location.getLatitude() + "經度：" + location.getLongitude();
        Log.d("LocationUtils", address);
    }

    public Location showLocation() {
        return location;
    }

    public void removeLocationUpdatesListener() {
        if (Build.VERSION.SDK_INT >= 23 && 
        ActivityCompat.checkSelfPermission(mContext, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED && 
        ActivityCompat.checkSelfPermission(mContext, Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
            return;
        }
        if (locationManager != null) {
            uniqueInstance = null;
            locationManager.removeUpdates(locationListener);
        }
    }

    LocationListener locationListener = new LocationListener() {
        @Override
        public void onStatusChanged(String provider, int status, Bundle arg2) {
        }

        @Override
        public void onProviderEnabled(String provider) {
        }

        @Override
        public void onProviderDisabled(String provider) {
        }

        @Override
        public void onLocationChanged(Location location) {
            location.getAccuracy();
            setLocation(location);
        }
    };
}
```

可以在mainActivity如下運用，因為有設立監聽事件所以在Activity生命週期onDestroy時必須取消衛星監聽事件。

```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button btn = (Button) findViewById(R.id.btn);
        final TextView text = (TextView) findViewById(R.id.text);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Location location = LocationUtils.getInstance(MainActivity.this).showLocation();
                if (location != null) {
                    String address = "緯度：" + location.getLatitude() + "經度：" + location.getLongitude();
                    Log.d("FLY.LocationUtils", address);
                    text.setText(address);
                }
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        LocationUtils.getInstance(this).removeLocationUpdatesListener();
    }
}
```

參考資料：  
[**Android通过原生APi获取经纬度**](https://www.jianshu.com/p/7ebbd2db749d)  
[**GPS定位經緯度**](https://my.oschina.net/JiangTun/blog/897650)

