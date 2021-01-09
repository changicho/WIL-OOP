# 추상화

데이터나 프로세스 등을 의미가 **비슷한 개념**이나 **의미있는 표현**으로 정의하는 과정

두 가지 방식의 추상화

- 특정한 성질
- 공통 성질 (일반화)

## 타입 추상화

여러 구현 class를 대표하는 상위 타입을 도출한다.

- 인터페이스 타입으로 추상화 한다.
- 추상화 타입과 구현은 타입 상속으로 연결한다.

다음과 같은 콘크리트(concrete) class들이 존재한다고 하자.

- EmailNotifier
- SMSNotifier
- KakaoNotifier

위 세가지 클래스는 모두 Notifier 기능을 수행한다고 볼 수 있다.

따라서 Notifier 인터페이스를 다음과 같이 정의하고 이를 상속해 위 3개의 class를 만들 수 있다.

```java
// 기능에 대한 의미를 제공한다.
// 구현은 Notifier를 상속한 객체에서 구현한다.
// 따라서 구현은 제공하지 않고, 어떻게 구현할지 알 수 없다.
public interface Notifier {
  notify(){}
}
```

구현을 제공하는 클래스를 콘크리트 클래스라고 한다.

## 추상 타입 사용

추상 타입은 구현을 감춘다.

이는 **변경이 유연**해지기 때문이다.

콘크리트 클래스를 직접 사용할 경우, 각 클래스마다 요구사항이 추가되었을 때 관련된 부분을 모두 직접 추가해야 한다.

추상 타입을 사용해 로직은 그대로 두고, 세부 내용만 변경한다.

예를 들어 factory pattern을 이용해서 객체를 생성하고 이용한다.

## 추상화의 시점

추상화는 의존 대상이 변경하는 시점에

추상화는 추상 타입의 증가를 의미한다. 이는 추상 타입이 늘어나기 때문에 복잡도가 증가하는 결과가 나온다.

- 아직 존재하지 않는 기능에 대한 이른 추상화는 주의한다.
- 잘못된 추상화의 가능성 & 복잡도 증가
- 실제 변경과 확장이 발생할 때 추상화를 시도한다.

다음 3 단계의 코드를 살펴보자

```javascript
class OrderService {
  constructor(){
    this.sender = new MailSender();
  }
  order(...) {
    sender.send(message);
  }
}
```

위 코드에서 SMS 서비스 로직이 추가된다고 하자

```javascript
class OrderService {
  constructor(){
    this.sender = new MailSender();
    this.smsService = new SmsService();
  }
  order(...) {
    sender.send(message);
    smsService.send(smsMsg);
  }
}
```

위와 같이 하나의 기능이 덧붙여지는 경우 해당 기능을 단순히 추가할 수도 있을것이다.

그러나 해당 기능이 자주 변경되거나 기능이 커질 경우 Notifier 클래스를 새로 만들어 이를 위임할 수 있다.

```javascript
class OrderService {
  constructor(){
    this.notifier = new Notifier();
  }
  order(...) {
    notifier.notify(noti);
  }
}
```

즉 추상화가 필요한 시점에 추상화를 사용해야 이점을 얻을 수 있다.

## 추상화를 잘 하려면?

- 구현을 한 이유가 무엇 때문인지 생각해야한다.
