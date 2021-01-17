# 의존 주입 (Dependency Injection)

의존하는 대상을 직접 생성하지 않고, 생성자 or 메소드를 이용해 주입받는 방식이다.

```javascript
class ScheduleService {
  // 생성자에서 할당
  constructor(repository) {
    this.repository = repository;
  }
  // 메소드로 할당
  setCalculator(calculator) {
    this.calculator = calculator;
  }
}

// 초기화
const ss = new ScheduleService(repository);
ss.setCalculator(calculator);
```

## 조립기 (Assembler)

조립기가 객체 생성, 의존 주입을 처리한다.

예시로는 스프링 프레임워크가 존재한다.

```java
@Configuration
public class Config {
  @Bean
  public ScheduleService scheduleService() {
    ScheduleService svc = new ScheduleService(repo());
    svc.setCalculator(expCal());
    return svc;
  }

  @Bean
  public UserRepository repo() { /*...*/ }

  @Bean
  public Calculator expCal() { /*...*/ }
}
```

스프링은 객체를 생성하고 의존대상을 주입하는 코드를 설정으로 작성한다.

```java
// 초기화
ctx = new AnnotationConfigApplicationContext(Config.class);
// 사용할 객체 구함
ScheduleService svc = ctx.getBean(ScheduleService.class);
// 사용
svc.getSchedule(/*...*/);
```

## DI의 장점

### 의존 대상이 바뀌면 조립기만 변경

상위 타입을 사용할 경우 의존 대상이 바뀌면 조립기(Config)만 병경하면 된다.

```javascript
class OrderService {
  constructor(notifier) {
    this.notifier = notifier;
  }
}
```

```javascript
class Config {
  notifier() {
    return new EmailNotifier();
  }
  orderService() {
    return new OrderService(notifier());
  }
}
```

Spring의 경우에서 notifier는 OrderService에 의존성으로 설정되어 있는 상태이다.

위와 같은 코드에서 notifier를 EmailNotifier에서 변경하고 싶다면 notifier 부분을 변경하면 된다.

### 대역 객체를 사용해 테스트 가능

의존하는 객체의 실제 구현이 없더라고, 대역 객체(테스트 객체)를 이용해 테스트 가능하다.

```javascript
const tempDb = new MemoryRepository();
const svc = new ScheduleService();

svc.setMemoryRepository(tempDb);

tempDb.addUser("id", new User(/*...*/));
const user = svc.getUserById("id");
assert(EXPECTED, user.getType());
```

DI를 습관처럼 사용하자!

의존 객체는 주입받도록 코드를 작성하는 습관을 들이자.
