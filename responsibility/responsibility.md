# 책임

## 기능

기능은 하위 기능으로 분해가 가능하다

ex) 암호 변경

- 변경 대상 확인
  - 변경 대상을 구함
  - 대상 없으면 오류 응답
- 대상 암호 변경
  - 암호 일치 여부 확인
  - 암호 데이터 변경

기능은 곧 책임이다.

따라서 분리한 각 기능을 알맞게 분배해야 한다. (객체에게)

### 큰 클래스, 큰 메소드

클래스나 메소드가 커지면 절차 지향의 문제가 발생한다.

- 큰 클래스 : 많은 필드를 많은 메소드가 공유
- 큰 메소드 : 많은 변수를 많은 코드가 공유
- 여러 기능이 하나의 클래스/메소드에 섞여있을 가능성

따라서 책임에 따라 코드를 분리할 필요가 있다.

## 몇 가지 책임 분배/ 분리 방법

- 패턴 적용
- 계산 기능 분리
- 외부 연동 분리
- 조건별 분기는 추상화

이 때 **의도가 잘 드러나는 이름**을 사용해야 한다.

## 패턴 적용

- 전형적인 역할 분리 (컨트롤러, 서비스, DAO)
- 복잡한 도메인 : (엔티티, 벨류, 엔티티, 레파지토리, 도메인)
- AOP
- GoF

## 계산 분리

계산을 담당하는 class를 나눈다.

계산이 필요한 경우 분리한 class의 계산 기능을 사용한다.

## 연동 분리

네트워크, 메시징, 파일 등 연동처리 코드를 분리한다.

## 조건 분기는 추상화

연속적인 if-else는 추상화를 고민한다.

(각 분기마다 하는 동작이 유사한 경우)

## 역할 분리와 테스트

역할 분리가 잘 되는 경우 테스트 하기 용이해진다.

다음 원본 코드와 역할 분리가 된 코드를 살펴보자

```javascript
const member = memberRepository.find(id);
const product = productRepository.fond(productId);

if (member.membership == "GOLD") {
  // ...
} else if (member.membership == "SILVER") {
  // ...
}
if (isDoubledPointTarget(product)) {
  // ...
}
```

```javascript
class PointCalculator {
  // membership, payAmount, productId;
  calculate() {
    if (member.membership == "GOLD") {
      // ...
    } else if (member.membership == "SILVER") {
      // ...
    }
    if (isDoubledPointTarget(product)) {
      // ...
    }
  }
}
```

아래 역할분리 된 코드의 경우 계산 로직을 테스트 하기 용이해진다.

즉 특정 기능만 테스트 하기 위해서 분리를 사용할 수 있다.

### 기능 분리 예시

회원 가입 기능을 만들 때 기능을 분리해보자

- 사용자 : 이메일, 이름, 암호를 입력한다.
- 암호 : 규칙 3가지를 통과하지 않으면 다시 입력한다.
- 중복체크 : 이메일이 중복되면 다시 입력한다.
- 메일 발송 : 이메일 인증을 위해 메일을 발송한다.
- 회원가입 완료 : 회원가입을 성공시킨다.

다음과 같은 방식으로 나눌 수 있다.

- 회원 가입 기능
  - 웹 요청 (RegisterController)
    - 필수 값 검증 (RegisterCommandValidator)
    - 회원 가입 처리
  - 회원 가입 (RegisterService)
    - 암호 규칙 검사 (PasswordPolicy)
      - 검사 여부
    - 이메일 중복 확인
      - 이메일 회원 조회 (MemberRepository)
      - 가입 실패
    - 인증 메일 발송 (AuthMailSender)
      - 토큰 생성 (AuthTokenGenerator)
      - 토큰 저장
      - 메일 전송
    - 회원 정보 저장 (MemberRepository)

다음과 같은 기능들로 세분화 하며 하위 기능을 도출할 수 있을것이다.
