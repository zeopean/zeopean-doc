### 时间控件

```

clickFun="laydate({istime: true, format: 'YYYY-MM-DD hh:mm:ss'})"

```


### 图片上传

```


    // 初始化头像上传
    var listPicture = new $WebUpload("listPicture");
    listPicture.setUploadBarId("progressBar");
    listPicture.init();

    var bannerPicture = new $WebUpload("bannerPicture");
    bannerPicture.setUploadBarId("progressBar");
    bannerPicture.init();

```