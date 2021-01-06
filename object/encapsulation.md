# Encapsulation (캡슐화)

> 객체가 어떻게 구현했는지를 외부에 감추는 것을 의미한다.

(데이터 + 관련 기능 묶기)

캡슐화는 기능의 구현을 외부에 감추는 것이다. (구현된 상세한 내용을 감춘다. 외부 사용자 입장에서는 로직을 몰라도 됨)

정보 은닉 의미를 포함한다.

## 캡슐화를 하지 않는 경우

```javascript
if(account.getMembership === 'PREMIUM' && account.getExpireDate() > new Date())
```

위와 같은 코드에서 서비스가 계속되면서 이벤트를 위해 조건을 변경한다고 하자.

```javascript
if(account.getMembership === 'PREMIUM' && account.getExpireDate() > new Date() - 20 && account.getEnterDate() < new Date() - FIVE_YEAR && /* ... */ )
```

대부분의 서비스에서 위와같은 로직이 변경되는 부분은 한곳뿐이 아닐것이다.

요구사항의 변화가 데이터의 구조와 사용에 변화를 만든다.

ex) 언어의 spec 변경에 따른 로직 변경 등

## 캡슐화를 하는 경우

```javascript
if(account.hasPremiumPermission())
```

account 객체를 사용하는 외부에서는 내부적으로 어떻게 동작하는지 모른다.

내부의 코드가 변경되어도 외부에선 몰라도 됨!

캡슐화는 **연쇄적인 변경이 전파되는 것**을 최소화 한다.

요구사항의 변화가 내부 구현을 변경 > 코드 영향 최소화

캡슐화의 시도 : 기능에 대한 이해도를 높일 수 있다.

(메소드, 프로퍼티 명으로 기능 유추 가능)

## 캡슐화를 위한 규칙

### Tell, Don't Ask

```javascript
// do not
if (account.getMembership() === "REGULAR") {
}
// do
if (account.hasRegularPermission()) {
}
```

데이터를 요청하지 않고, 판단 해달라고 하는 것

### Demeter's Law

데미테르의 법칙

- 메소드에서 생성한 객체의 메소드만 호출
- 파라미터로 받은 객체의 메소드만 호출
- 필드로 참조하는 객체의 메소드만 호출

```javascript
// do not
account.getExpireDate().isAfter(now);

// do
account.isExpired();
```

```javascript
// do not
const date = account.getExpireDate();
date.isAfter(now);

// do
account.isValid(now);
```

캡슐화는 기능의 구현을 외부에 감추는것

캡슐화를 통해 기능을 사용하는 코드에 영향을 주지 않고 (또는 최소화하고) 내부 구현을 변경할 수 있는 유연함을 가질 수 있다.
