# 상속 (Inheritance)

상위 클래스의 기능을 재사용, 확장하는 방법으로 사용

```javascript
class Controller {
  // ...
}

class AbstractController extends Controller {
  // ...
  handleRequest() {}
}

class BaseCommandController extends AbstractController {
  // ...
}

class AbstractFormController extends BaseCommandController {
  // ...
  handleRequestInternal() {}
  showForm() {}
}
```

위와 같은 예시를 들 수 있다.

점점 기능이 확장되면서 상위 클래스를 상속하며 재사용하고 확장한다.

## 상속을 통한 기능 재사용시 발생할 수 있는 단점

- 상위 클래스 변경이 어려워진다.
- 클래스가 증가한다.
- 상속을 오용할 수 있다.

### 상위 클래스 변경이 어렵다

상위 클래스의 변경의 여파가 계층 구조를 따라 전파된다.

변경시에 하위 클래스에 끼치는 영향을 고려해야된다.

하위 클래스가 많은 경우 변경하기 어려워진다.

### 클래스가 증가한다

다음과 같은 구조를 생각해보자

```javascript
class Storage {}

class CompressedStorage extends Storage {}

class EncryptedStorage extends Storage {}

class CacheableStorage extends Storage {}
```

위와 같은 상황에서 해당 요소들을 조합한 클래스를 만들고자 하는 경우, 하위 클래스들이 매우 많이 생성된다.

### 상속 오용

상속 자체를 오용할 수 있다.

```javascript
class Container extends List<Data> {
  push(data: Data) {
    super();
    this.add(Data);
  }
  doSomething() {}
}
```

Container 클래스는 List 객체를 상속해 push등의 메소드를 사용한다.

이러한 class는 실제 IDE에서 작업할 때, Container의 메소드만 보이는 것이 아닌 List의 메소드 또한 나타나게된다.

그렇기 때문에 List의 메소드를 사용해 의도치 않은 동작을 수행할 수 있다.
