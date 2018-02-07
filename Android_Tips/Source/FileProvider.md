### FileProvider
1. xml파일 생성
![res-xml](Source/images/fileprovider.png)
``` xml
  <?xml version="1.0" encoding="utf-8"?>
  <paths xmlns:android = "http://schemas.android.com/apk/res/android">
     <files-path
        name = "aaa"
        path = "img/"/>
  </paths>
```

2. manifests 설정
``` xml
<provider
     android:name = "android.support.v4.content.FileProvider"
     android:authorities = "<자신의 패키지 명>.fileprovider"
     android:exported = "false"
     android:grantUriPermissions = "true">
     <meta-data
        android:name = "android.support.FILE_PROVIDER_PATHS"
        android:resource = "@xml/<xml 명>"/>
</provider>
```

3. Uri 생성
``` java
private Uri getFileUri() {
   File dir = new File( getFilesDir(), "img" ); // xml에서 설정한 경로와 동일하게
   if ( !dir.exists() ) {
      dir.mkdirs();
   }
   File file = new File( dir, System.currentTimeMillis() + ".png" );
   String imgPath = file.getAbsolutePath();
   return FileProvider.getUriForFile( this, "<자신의 패키지 명>.fileprovider", file );
}
```
