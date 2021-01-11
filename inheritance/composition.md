# 조립 (Composition)

상속의 단점을 해결하는 방법 중 하나이다.

- 여러 객체를 묶어서 더 복잡한 기능을 제공한다.
- 보통 필드로 다른 객체를 참조하는 방식으로 조립한다.
- 또는 객체를 필요한 시점에서 생성하거나 구한다.

```javascript
class FlowController {
  constructor() {
    this.encryptor = new Encryptor();
  }
  process() {
    encryptedData = this.encryptor.encrypt(data);
  }
}
```

위 코드는 상속이 아닌 조합을 통해 내부적으로 encrypt 기능을 구현했다.

또한 상속을 사용하지 않기 때문에 상위 class의 메소드 등을 오용하는 문제를 막을 수 있다.

## 상속 보다는 조립 (Composition over Inheritance)

상속하기에 앞서 조립으로 풀 수 있는 문제인지 검토한다.

진짜 하위 타입인 경우에만 상속을 사용한다.
