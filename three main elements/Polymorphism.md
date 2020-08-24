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

이전 상속에서 배웠듯이 상속을 사용하기 위해 알아둬야하는 중요한 숙어는 `is a kind of` 라고 배웠다. 인터페이스에서도 알아둬야하는 숙어가 있는데 바로 `be able to(~ 할 수 있는)` 이다.
숙어를 토대로 위 코드를 나타내자면 다음과 같다.

- 말 is kind of 동물
- 캥거루 is kind of 동물
- 말 is able to 탈 수있는

자바의 인터페이스는 무척이나 중요하다.

인터페이를 통한 프로그래밍시 얻은 이점은 다음과 같다.

인터페이스를 두어서 얻는 이점은 세부 구현체를 숨기고 인터페이스를 바라보게 함으로써 클래스 간의 의존관계를 줄이는 것, 결합도를 낮추고, 다형성을 위해서이다. 즉, `decoupling` 과 `polymorphism` 때문입니다.

캡슐화에서 배웠듯이 결합도를 낮추면 좋은점은 변경에 용이해지기 때문에 유지보수성을 높일 수 있다는 것이다.


