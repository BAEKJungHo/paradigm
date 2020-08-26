# 다형성(Polymorphism)

다형성이란 여러 객체에게 동일한 명령을 내렸을 때 서로 다르게 반응하는 현상을 의미한다.

예를들어 동물이라는 상위클래스가 있고, 상위클래스에는 “짖다” 라는 추상메서드를 가지고 있으며 하위 클래스(강아지, 고양이)는 추상메서드를 오버라이딩 하여 
강아지 객체에게 명령을 내렸을 때에는 “멍멍”, 고양이 객체에게 명령을 내렸을 때에는 “야옹” 처럼 각자 다른 반응을 나타내는것을 다형성이라고 한다.

다형성을 구현하는 방법은 크게 4가지가 있다.

- 인터페이스
- 추상클래스
- 오버로딩
- 오버라이딩

```java
/**
* 동물 추상 클래스
*/
@Getter @Setter
public abstract class Animal {
	  private String name;
	  private String leg;

	  /* Abstract method */
	  abstract void run();
}

/**
* 탈 수 있는(Ridable) 인터페이스
*/
public interface Ridable {

	  /**
	  * Abstract method 
	  * @riderName
	  */
	void ridable(String riderName);
}

/**
* 추상클래스를 상속 받고 인터페이스를 구현한 Horse 클래스
*/
public class Horse extends Animal implements Ridable {

	@Override
	public void run() {
		System.out.println(this.getName()+"은(는) 네 발로 뛴다.");
	}
  
	@Override
	public void ridable(String riderName) {
		System.out.println(this.getName()+"은(는) "+riderName+"을(를) 태울 수 있다.");
	}
  
}

/**
* 추상클래스를 상속 받은 Kangaroo 클래스
*/
public class Kangaroo extends Animal {

	@Override
	public void run() {
		System.out.println(this.getName()+"은(는) 네 발로 뛴다.");
	}
  
}

public class MainClass {
	public static void main(String[] args) {
		Horse horse = new Horse();
    		Kangaroo kangol = new Kangaroo();
    
		/* 상속받은 말의 속성 */
		horse.setName("얼룩말");
		horse.setLeg("다리 4개");
    
   		 /* 상속받은 캥거루의 속성 */
		kangol.setName("캥거루");
		kangol.setLeg("다리 4개");
    
		/* 말 구현체의 메서드 호출 */
		horse.run();
		horse.ridable("BAEKJH");
    
	        /*  구현체의 메서드 호출 */
		kangol.run();
	}
}
```

이전 상속에서 배웠듯이 상속을 사용하기 위해 알아둬야하는 중요한 숙어는 `is a kind of(~ 의 한 종류)` 라고 배웠다. 인터페이스에서도 알아둬야하는 숙어가 있는데 바로 `be able to(~ 할 수 있는)` 이다.

숙어를 토대로 위 코드를 나타내자면 다음과 같다.

- 말 is kind of 동물
- 캥거루 is kind of 동물
- 말 is able to 탈 수있는

자바의 인터페이스는 무척이나 중요하다.

인터페이를 통한 프로그래밍시 얻 이점은 다음과 같다.

인터페이스를 두어서 얻는 이점은 세부 구현체를 숨기고 인터페이스를 바라보게 함으로써 클래스 간의 의존관계를 줄이는 것, 결합도를 낮추고, 다형성을 위해서이다. 즉, `decoupling` 과 `polymorphism` 때문이다.

캡슐화에서 배웠듯이 결합도를 낮추면 좋은점은 변경에 용이해지기 때문에 유지보수성을 높일 수 있다는 것이다.

> 스프링을 배우게 되면 `DI(Dependency Injection)` 원칙이 등장하는데, 이 원칙의 기본 아이디어는 실제 사용할 세부 구현체를 숨기고 추상화된 인터페이스를 통해 간접적으로 접근하는 것이다. DI 원칙을 따르면 장점이 클래스 간의 의존관계가 줄어들기 때문에 decoupling 할 수 있다.

여기서 조금 더 나아가서 자바 형변환에 대해 알아보자. (JVM 지식이 약간 필요하며, 동적 바인딩과 정적 바인딩에 대한 개념이 등장한다.)

## 자바 형변환(묵시적 형변환(promotion), 명시적 형변환(casting))

### 묵시적 형변환(promotion)

묵시적 형변환은 작은타입이 큰 타입으로 변경되는 것을 말한다. 작은 타입이 큰 타입으로 변경될 때 앞에 따로 타입을 명시하지 않아도 된다.

```java
int a = 10;
float b;

b = a;
```

다음은 객체간의 묵시적 형변환에 대해서 알아보자.

```java
class Polymorphism {
    public static void main(String[] args) {
      /**
       * var 는 메모리의 Stack Area 에 저장되며 Subclass 는 Heap Area 에 저장됩니다. 그리고 스택 영역에 저장된 var 는 힙 영역의 Subclass 를 가리킨다.
       * 하지만 var 변수로 접근가능한 멤버는 Superclass 이다.
       */
      SuperClass var = new SubClass(); // Promotion : 자동 타입변환, Pholymorphism
      // 동적 바인딩(Dynamic Binding)
      var.methodA(); // Runtime 시에 결정된다. SubClass의 메서드 호출
      // 정적 바인딩(Static Binding)
      var.staticMethodA(); // static 메서드는 compile 시에 결정, SuperClass의 메서드 호출
   }
}

class SuperClass {
    public void methodA();
    public static void staticMethodA();
}

class SubClass extends SuperClass {
    @Override
    void methodA() { 
      System.out.println("SubClass");
    }
  
    /*
     * 아래 코드는 Error 발생
     * static 으로 선언된 메서드는 오버라이딩 불가능
     */
    @Override
    static void staticMethodA() { 
      System.out.println("SubClass"); 
    }
}
```

SubClass 는 SuperClass 를 상속 받고있다. 슈퍼 클래스로부터 상속받은 메서드를 하위 클래스에서 오버라이딩한 경우, var 변수로 methodA() 를 호출할 때 오버라이딩한 하위 클래스에 있는
메서드를 호출하게 된다. 즉, Runtime 시에 어떤 메서드를 실행할지 결정하는데 이걸 `동적 바인딩(dynamic binding)` 이라고 한다.

반면 슈퍼 클래스에 있던 static 메서드는 JVM 의 클래스 로더에서 로딩과정에서(컴파일 시점에) 메서드 영역(method area) 에 생성되기 때문에, 하위 클래스에서 상속받을 수 없게 되는 것이다.
즉, static 메서드는 new Subclass() 가 메모리에 등록되기 전에 생성되기 때문에 오버라이딩 자체가 불가능한것이다.
이걸 `정적 바인딩(static binding)` 이라고 한다. 

동적 바인딩(Dynamic Binding) 은 실행시에 성격이 결정되고 정적 바인딩(Static Binding) 은 컴파일시에 성격이 결정되는데, static 키워드가 붙은 애들은 JVM 에서 객체가 생성되기 전에 먼저 메모리에 올리기 때문에, 객체가 생성되지않아도 클래스명.변수명 혹은 클래스명.메서드명 으로 접근이 가능했던이유가 여기에 있다.

> 동적 바인딩은 런타임(Runtime, 실행)시점에 객체 타입을 기준으로 실행될 함수를 호출하는 것을 의미하고 정적 바인딩은 컴파일(Compile)시점에 객체 타입을 기준으로 실행될 함수를 호출하는것을 의미한다.

### 명시적 형변환(casting)

명시적 형변환은 큰타입이 작은 타입으로 변경될때 앞에 타입을 명시해줌으로써 가능하다.

```java
int a;
float b = 1.1;

a = (int) b;
```

- 객체간의 Casting

```java
public void casting(Parent parent){
	if(parent instanceof Child) {
		Child child = (Child) parent; // Casting
	}
}
```

객체간 Casting 을 하기 위해서는 항상 instanceof 를 사용하여 상속 관계에 있는지 확인해야 한다. 상속관계에 있는 않은 객체를 형변환 하려면 에러가 발생할 것이다.
