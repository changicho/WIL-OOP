# 다형성

polymorphism

여러(poly) 모습(morph)을 갖는것을 의미한다.

객체 지향에서는 한 객체가 여러 타입을 갖는 것을 의미한다.

- 즉 하나의 객체가 여러 타입의 기능을 제공한다.
- 타입 상속으로 다형성을 구현한다 (하위 타입은 상위 타입도 될 수 있다.)

다음 class와 interface 예제를 보자

```java
public class Timer {
  public void start(){}
  public void stop(){}
}

public interface Rechargeable {
  void charge();
}
```

위 class와 interface를 모두 상속하고 참조하는 객체를 생성하자

```java
public class IotTimer extends Timer implements Rechargeable {
  // ...
}

IotTimer it = new IotTimer();
it.start();
it.stop();

Timer t = it;
t.start();
t.stop();

Rechargeable r = it;
r.charge();
```

IotTimer는 Timer, Rechargeable 모두 될 수 있다.
