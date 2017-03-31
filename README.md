# MPermissionUtils
GitHub上有很多解决AndroidM运行时权限的库，但是个人不想就因为一个权限问题而引入一个库，所以集各位库中的代码，简单封装了一个工具类。使用起来很简单。
由于时间匆忙，所以后期有时间会再继续进行优化。

# 使用
以拨打电话为例，首先在Manifest文件中定义好拨打电话权限：
```
  <uses-permission android:name="android.permission.CALL_PHONE"/>
```

* 第一步（当用户点击拨打电话按钮时执行如下代码）：
```
MPermissionUtils.requestPermissionsResult(this, 1, new String[]{Manifest.permission.CALL_PHONE}
                , new MPermissionUtils.OnPermissionListener() {
                    @Override
                    public void onPermissionGranted() {
                        Toast.makeText(MainActivity.this, "授权成功,执行拨打电话操作!", Toast.LENGTH_SHORT).show();
                    }

                    @Override
                    public void onPermissionDenied() {
                        MPermissionUtils.showTipsDialog(MainActivity.this);
                    }
                });
```

* 第二步（重写onRequestPermissionsResult()方法，使用MPermissionUtils类中的方法进行接管）：
```
@Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        MPermissionUtils.onRequestPermissionsResult(requestCode, permissions, grantResults);
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
    }
```
该步由于操作不会改变，所以可以直接放在BaseActivit和BaseFragment中。

# GIF
 ![image](https://github.com/Airsaid/MPermissionUtils/blob/master/gif/1.gif)
 
# 感谢
* https://github.com/HanderWei/PermissionBestPractice
* https://github.com/hongyangAndroid/MPermissions
* https://github.com/linglongxin24/MPermissions
