toString()과valueOf()에 대해 찾아봤다.
두 개다 string을 반환을 해준다.

두 개의 차이점은 NPE(null point exception)발생기는 것이다.
toString에 경우 object가 null이면 NPE이를 발생시키지만
valueOf는 NP가 발생하지 않는다.

코드를 사용할 떄 NPE 방지를 위해 valueOf를 쓰는게 좋다.

```java
destItemMap.get("LOWER_VAL") 이 null 일 경우
String lowerCoatingVal1 = String.valueOf(destItemMap.get("LOWER_VAL"));
String lowerCoatingVal2 = destItemMap.get("LOWER_VAL").toString();

lowerCoatingVal1 = "null"
lowerCoatingVal2 = NullPointerException 발생

String.valueOf()의 null 체크
String lowerCoatingVal1 = String.valueOf(destItemMap.get("LOWER_VAL"));
if("null".equals(lowerCoatingVal1)) {
    // To do Somting....
}

// equals함수를 사용할때 왼쪽에 있는 것을 기준으로 비교하기 때문에 변수보다는 문자열을 왼쪽에 두는 것을 추천한다.
// 즉 strTestVal이 null인 경우 ret = "1"인 if문은 NPE를 발생시킨다.
String strTestVal = null;
String ret = "";

/* Exception 발생 */
if( !(strTestVal .equals("")) ) ret = "1";

/* 정상 */
if( !("".equals(strTestVal)) ) ret = "2";
```
