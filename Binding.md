# Android Binding
######  데이터 바인딩에 관련된 간단한 앱 프로젝트<br>

### 1. 데이터 바인딩이란 ?
> 안드로이드 앱을 제작할 때 텍스트뷰, 버튼, 이미지뷰 등의 위젯에 추가 작업을 해야할 때 findViewById()를 하여 일일이 객체를 잡아주고 작업을 하고 id가 달라지면 앱이 죽는 등 귀찮고 지루한 작업을 경험했을 것이다.<br>
데이터 바인딩은 이런 작업을 줄여주고 소스를 직관적으로 만들어 줄 수 있다.<br>
또한 MVVM패턴 구현에 기여할 수 있다고 한다.

### 2. 사용법
> 예전에는 버터나이프라는 라이브러리를 사용하여 많이 구현했다.<br>
하지만 안드로이드에서 직접 라이브러리를 배포하여 보다 쉽게 사용할 수 있게 되었다.<br>
gradle에 한줄만 추가하면 사용할 수 있다.<br>
자세한 사용법은 아래에 기술한다.

### 3. 간단한 예제 프로그램
> 이름을 입력하고 Next 버튼을 클릭하면
다음 화면에서 이름 + "님 안녕하세요" 라는 글씨가 떠있는 화면을 보여준다.<br><br>
> EditText의 값을 가져오고, 버튼의 클릭 이벤트를 제어하고, 화면이동, 텍스트뷰의 값을 지정한다.

### 4. 최소사항
+ Android 2.1 (API 7) 이상
+ Android Plugin for Gradle 1.5.0-alpha1 이상
+ Android Studio 1.3 이상

### 5. Thinks
> 코드를 생각보다 많이 줄여준다. <br>
> 비 숙련자가 보기엔 이해하기 어려울 수 있다. <br>
> 잘 사용하면 개발시간을 굉장히 줄일 수 있을 것 같다. <br>
> 좀 더 세부적인 공부가 필요하다. <br>

### 6. 참조 문서

> + [Android Developer](https://developer.android.com/topic/libraries/data-binding/index.html?hl=ko)<br><br>
> + [박상권의 삽질 블로그](http://gun0912.tistory.com/71)<br>

----------------
----------------
----------------
----------------

#### Gradle 설정
``` javascript
  android{
    ......
    dataBinding {
        enabled = true
    }
  }
```

#### XML 구성
1. activity_main ( 첫 화면 )
> layout으로 감싸준다<br>
> 바인딩으로 연결한다면 바인딩.{id}로 접근이 가능하다.<br>
> Ex) binding.nameEditText.getText().toString();

``` xml
  <?xml version="1.0" encoding="utf-8"?>
  <layout xmlns:android="http://schemas.android.com/apk/res/android">

    <RelativeLayout
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <EditText
            android:id="@+id/nameEditText"
            android:hint="이름을 입력해주세요."
            android:layout_centerInParent="true"
            android:layout_width="200dp"
            android:layout_height="wrap_content" />

        <Button
            android:id="@+id/nextButton"
            android:text="Next"
            android:layout_marginTop="20dp"
            android:layout_below="@+id/nameEditText"
            android:layout_centerHorizontal="true"
            android:layout_width="200dp"
            android:layout_height="wrap_content" />

    </RelativeLayout>
  </layout>
```

2. activity_next.xml
> layout으로 감싸준다.<br>
> data부분이 추가되었는데 이 부분은 독특하다.<br>
> 우선 variable부분을 살펴보면 만들어둔 User클래스를 타입으로 삼고 name을 user로 정의해두었다.<br>
> TextView에 text값을 @{user.name}으로 해두었는데<br>
> NextActivity에서 binding.setUser(user)를 해주면<br>
> user객체의 getName()을 해주어서 TextView에 넣어주는 방식이다.<br>
> 살짝 불편해 보일수도 있지만 여러 위젯에 넣어주어야 한다면 상당히 편리할 듯 하다. <br>

``` xml
  <?xml version="1.0" encoding="utf-8"?>
  <layout xmlns:android="http://schemas.android.com/apk/res/android">

      <data>
          <variable
              name="user"
              type="com.nainfox.binding.vo.User"/>
      </data>

      <LinearLayout
          android:orientation="horizontal"
          android:layout_width="match_parent"
          android:layout_height="match_parent">

          <TextView
              android:text="@{user.name}"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content" />

          <TextView
              android:text="님 안녕하세요."
              android:layout_width="wrap_content"
              android:layout_height="wrap_content" />


      </LinearLayout>
  </layout>
```

#### VO
User.java
> 사용자 데이터 클래스<br>
> final을 사용하여 한번 값을 입력하면 값 수정이 불가능 하게 만들었다 <br>

``` java
public class User {
    private final String name;

    public User(String name){
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

#### Java
1. MainActivity
> activity_main과 연결되어있다. <br>
> ActivityMainBinding 객체가 자동으로 만들어져 있을 것이다.<br>
> 이 객체를 사용하여 위젯들을 사용 가능하다.<br>
> Ex) binding.nameEditText.getText().toString();

``` java

public class MainActivity extends AppCompatActivity {
    public static final String TAG = "### MainActivity";
    public static final String NAME = "name";

    // 데이터 바인딩 객체
    // 액티비티가 layout으로 감싸져 있을 경우 자동으로 생성
    private ActivityMainBinding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        binding = DataBindingUtil.setContentView(this, R.layout.activity_main);

        setButtonClickListener();
    }


    /**
     * Next Button 클릭 이벤트 제어
     */
    private void setButtonClickListener(){
        binding.nextButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                // binding.{id}로 위젯에 접근 가능
                String name = binding.nameEditText.getText().toString();
                Intent i = new Intent(getApplicationContext(), NextActivity.class);
                // intent에 값 전달
                i.putExtra(NAME, name);
                startActivity(i);
                finish();
            }
        });
    }
}
```

2. NextActivity
> activity_next와 연결<br>
> 마찬가지로 ActivityNextBinding 객체가 자동으로 생성되어 있다. <br>
> 이름을 동적으로 넣어주기 위해 MainActivity에서 받은 name값을 <br>
> setUser()메소드를 사용하여 TextView에 넣어준다.

``` java
public class NextActivity extends AppCompatActivity {
    public static final String TAG = "### NextActivity";
    public static final String NAME = "name";

    private ActivityNextBinding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        binding = DataBindingUtil.setContentView(this, R.layout.activity_next);
        binding.setUser(new User(getIntent().getStringExtra(NAME)));
    }

}
```
