# 객체

## 절차지향 vs 객체지향

다음 코드를 살펴보자

```javascript
// get user name API
if (account.getState() !== "DELETED") {
  return account.name;
} else {
  // do something
}

// check account status
if (account.getState() !== "DELETED") {
  return true;
} else {
  return false;
}
```

account 객체의 메소드를 이용해 API에서 check logic을 수행한다.

만약 현재까지 유저의 uuid의 자리수가 변경되거나 해서 유효한 유저임을 검사할 때 요소가 하나 더 늘어난다고 하자.

```javascript
account.getUUID().length > 16; // uuid가 16자리 이하는 가짜다!
```

이와 같이 로직이 변경되는 경우 상단의 check logic에는 다음 내용들이 들어가야한다.

```javascript
if (account.getState() !== "DELETED" && account.getUUID().length > 16)
```

다음 경우들을 생각해보자

- 유효한 유저의 조건이 추가되는 경우
- 유저 객채의 형태가 바뀌는경우
- 기타 등등...

이러한 절차지향적인 방법으로는 변화에 유연하게 대처하기 어려워진다.

**즉, 시간이 지날수록 유지보수하기 어려워 지는 코드이다!**

그렇다면 위 코드를 어떻게 리팩토링 할 수 있을까?

아래의 코드를 살펴보자

```javascript
// 정수판별에 따라 바뀌는 로직
if(n % 1 === 0)

if(isInt(n))
```

[출처 - 코드스피츠 - [특강] Code Squad 윤지수 마스터님](https://youtu.be/25Si0Sq3Vbs)

두 로직은 같다. 그러나 아래 함수를 이용해 정수 여부를 판별하는 경우가 훨씬 더 보기좋고 간결하다.

만약 'n % 1 === 0' 이라는 로직이 잘못된 경우, (n의 제한등이 생기거나) 에도 모든 코드를 변경하지 않고 isInt 부분만 변경하면 된다.

위와 같은 아이디어를 객체에 담아보자.

```javascript
if (account.isValid()) {
  // do something
}
```

훨씬 더 다양한 변화에 효과적으로 대처할 수 있게되었다.

## 객체란

객체의 핵심은 **기능을 제공하는 것** 이다.

객체는 제공하는 기능으로 정의된다. 단순한 데이터의 묶음만으로 정의하지 않는다.

객체는 데이터와 메소드(프로시저)가 적절히 묶인 형태여야한다.

그렇기 때문에 크기가 적절하게 나뉜 객체는 다음과 같은 장점을 가진다.

- 코드를 재사용하기 쉬워진다.
- 유지 보수가 쉽다.

객체 하나만으로는 많은 작업을 할 수 없다. 객체들 간의 유기적인 상호작용을 통해 모든 것들이 이루어질수 있다.

다음 객체를 살펴보자.

```javascript
const object = {
  a: 10,
  b: "b",
};
```

위 코드에서 object는 데이터에 접근만 하고 부가적인 기능이 없다.

따라서 이는 객체라기 보다는 **구조체**에 가깝다.

## 객체끼리의 연결

객체와 객체는 기능을 이용해 연결된다.

객체와 객체의 상호작용은 **메시지**를 주고받는다고 표현한다.

![object sequence diagram](https://user-images.githubusercontent.com/38618187/103642489-8c273300-4f96-11eb-8f35-7c62260dd35a.png)

위 그림은 시간별로 message를 주고받는것을 나타낸 다이어그램이다.

---

## 참고

- [인프런 - 객체 지향 프로그래밍 입문](https://www.inflearn.com/course/%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9E%85%EB%AC%B8)
- [코드스피츠 - [특강] Code Squad 윤지수 마스터님](https://youtu.be/25Si0Sq3Vbs)
