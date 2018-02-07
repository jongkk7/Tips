### spannable

1. SpannableString 생성
``` java
public static SpannableString getUnderLineColorText(String string, String targetString, int color) {
    SpannableString spannableString = new SpannableString(string);
    int targetStartIndex = string.indexOf(targetString);
    int targetEndIndex = targetStartIndex + targetString.length();
    spannableString.setSpan(new ForegroundColorSpan(color), targetStartIndex, targetEndIndex, Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
    spannableString.setSpan(new nderlineSpan(), targetStartIndex, targetEndIndex, Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);

    return spannableString;
}

```

2. 텍스트뷰에 삽입
``` java
  TextView textView = (TextView) findViewById(R.id.text);
  String string = "가격은 200원 입니다.";
  String targetString = "200원";
  textView.setText(TextFormatUtils.getUnderLineColorText(string, targetString, getResources().getColor(R.color.colorAccent)));
```

3. 완성
![res-xml](Source/images/spannable.png)
> 출처: http://sub-dev.tistory.com/10 [김형섭의 개발공간]
