# 캡슐화(Encapsulation)

캡슐화란 정보의 은닉이라고도 불리는데 내부 정보를 감춤으로써 외부 변경에 유연하게 대처하기 위해서 사용된다. 

`외부 변경에 유연하게 대처`라는 의미는 외부에서 캡슐화한 클래스의 내부 속성이나 메서드에 함부로 접근하지 못하게해서 값의 변경을 막는 것이다. 캡슐화가 제대로 되어있지 않아
외부에 의해 값이 변경된다면 경우에 따라서는 시스템 전체에 에러가 발생할 수도 있다.

- 캡슐화 하지 않은 경우

```java
public class Administrator {
  public String name; 
  public String id;
  public String age;

  public String getName() {
    return this.name;
  }
  
  public String getId() {
    return this.id;
  }
  
  public String getAge() {
    return this.age;
  }
}
```

접근 지시자(Access modifier)가 public 이므로 외부에서 Administrator 의 속성들의 값을 변경 시킬 수 있다. 따라서 값의 변경에 취약하다.

- 캡슐화 한 경우

```java
public class Administrator {
  private String name; 
  private String id;
  private String age;

  public String getName() {
    return this.name;
  }
  
  public String getId() {
    return this.id;
  }
  
  public String getAge() {
    return this.age;
  }
  
  public void setName(String name) {
    // 이름에 대한 검증 추가
    if(name.length() > 5) {
        System.out.println("이름은 5글자를 초과할 수 없습니다.");
    }
  }
  
  public void setId(String id) {
    this.id = id;
  }
  
  public void setAge(String age) {
    this.age = age;
  }
}
```

접근 지시자(Access modifier)를 private 선언하고 public 인 getter/setter 메서드를 사용해서 캡슐화를 하였다. 외부에서 Administrator 의 속성에 직접 접근해서 값을 변경할 수 없게되었다.

이렇게 캡슐화를 하면 외부에서 접근할 수 있는 대상이 제한되기 때문에 다른 코드들과의 결합도가 낮아진다.

결합도는 낮을 수록 좋은데(decoupling) 결합도가 낮다는건 클래스간의 의존관계가 낮다는 것이고, 이는 유지보수성을 좋게 만들고 향후 변경에 대해서 유연하게 대처할 수 있기 때문이다.



