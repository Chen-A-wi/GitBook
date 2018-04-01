# 物件相關設定

---

## ImageView

* ScaleType：可設定圖片置於imageView的狀態分為下列這五種。

  * center：

    以圖片中心點為中心設置於imageView中。

  * centerCrop：

    當圖片比imageView大/小時，會依圖片等比例縮放，並將其放在框的中間顯示，即大的圖會縮小，小的圖放大。但是，如果該圖非正方形者，會依其短邊來與ImageView的邊相等，因此其會將ImageView完全的填滿。

  * centerInside：

    當圖片比imageView大時，會依圖片之等比例縮小，並將其放在框的中間顯示。反之，當圖片比imageView小時，則該圖片不縮放，但將其以居中的方式呈現。

  * fitCenter：

    當圖片比imageView大/小時，會依圖片之等比例縮放，並將其放在框的中間顯示，即大的圖縮小，小的圖放大。而fitStart則靠上顯示；fitEnd為靠下顯示。
    
  * fitXY：

    圖片按照指定的大小在imageView中顯示，延展顯示圖片，不保持原有之比例，全部顯示圖片並填滿imageView。

