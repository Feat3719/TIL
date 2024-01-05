## Lombok Annotation
### @NoArgsConstructor
> 매개변수가 없는 기본 생성자를 생성한다.

<br>
🗒️example

<br>

* 사용하지 않았을 때

```java
public class Person {
    private String name;
    private int age;

    // 생성자
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class Main {
    public static void main(String[] args) {
        // 매개변수가 없는 기본 생성자 생성 시 => 오류 발생
        // @NoArgsConstructor 어노테이션 사용 혹은 매개변수가 없는 생성자 직접 생성 수행해야 된다. 
        Person person = new Person();
    }
}
```


* 사용했을 때

```java
import lombok.NoArgsConstructor;

@NoArgsConstructor
public class Person {
    private String name;
    private int age;

    // 생성자
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 매개 변수가 없는 기본 생성자가 자동으로 생성됨
}

public class Main {
    public static void main(String[] args) {
        // 정상 실행 된다.
        Person person = new Person();
    }
}
```

<br><br>

### @RequiredArgsConstructor
> @NonNull, final 로 선언된 필드 값만 매개변수로 받는 생성자를 생성한다.

🗒️example 
* 사용하지 않았을 때(직접 생성자 주입 코드 작성)

```java
import lombok.NonNull;

public class Person {
    @NonNull
    private String name;
    private int age;
    private final String sex;

    // 생성자 직접 작성
    public Person(@NonNull String name, String sex) {
        this.name = name;
        this.sex = sex;
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person("김이박", "남자");
    }
}
```


* 사용했을 때

```java
import lombok.RequiredArgsConstructor;

@RequiredArgsConstructor
public class Person {
    @NonNull
    private String name;
    private int age;
    private final String sex;

    // @NonNull, final 필드의 생성자를 자동 생성

}

public class Main {
    public static void main(String[] args) {
        Person person =  new Person("김이박","남자");
    }
}
```

<br><br>

### @AllArgsConstructor
> 모든 필드 값을 매개변수로 받는 생성자를 생성한다.

* 사용하지 않았을 때(직접 생성자 주입 코드 작성)
🗒️example 
```java
public class Person {

    private String name;
    private int age;
    private String sex;

    // 생성자 직접 작성
    public Person(String name, int age, String sex) {
        this.name = name;
        this.age = age;
        this.sex = sex;
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person("김이박", 20, "남자");
    }
}
```


* 사용했을 때

```java
import lombok.AllArgsConstructor;

@AllArgsConstructor
public class Person {

    private String name;
    private int age;
    private final String sex;

    // 모든 필드의 매개변수 생성자를 자동 생성

}

public class Main {
    public static void main(String[] args) {
        Person person =  new Person("김이박", 20, "남자");
    }
}
```
<br><br>


### @Getter
> 해당 값을 반환해주는 역할을 하는 Getter 메소드를 자동으로 생성해준다. 

* 클래스에 적용하면 해당 클래스 내부 모든 필드에 대한 Getter 가 생성되고, 각각의 필드에 적용하면 해당하는 필드 값의 Getter 가 생성된다.

🗒️example 
- @Getter 를 사용하지 않았을 때 -> 직접 Getter 생성
```java
@NoArgsConstructor
public class Person {

    private String name;
    private int age;
    private String sex;

    // 직접 getter 작성
    public String getName() {
        return name;
    }

}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        System.out.println(person.getName());
    }
}
```
- @Getter 사용
```java
@NoArgsConstructor
public class Person {
    @Getter // @Getter 사용
    private String name;

    private int age;
    private String sex;


}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        System.out.println(person.getName());
    }
}
```
<br><br>

### @Setter
> 해당 값을 반환해주는 역할을 하는 Setter 메소드를 자동으로 생성해준다. 

* 클래스에 적용하면 해당 클래스 내부 모든 필드에 대한 Setter 가 생성되고, 각각의 필드에 적용하면 해당하는 필드 값의 Setter 가 생성된다.

🗒️example 
- @Setter 를 사용하지 않았을 때 -> 직접 Setter 생성
```java
@NoArgsConstructor
public class Person {

    private String name;
    private int age;
    private String sex;

    public void setName(String name) {
    this.name = name;
    }

}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        person.setName("아무개");
    }
}
```
- @Setter 사용
```java
@NoArgsConstructor
@Setter
public class Person {
    private String name;
    private int age;
    private String sex;
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        person.setName("아무개",10,"남");
    }
}
```
<br><br>

### @Data
> @Getter, @Setter, @ToString, @EqualsAndHashCode, @RequiredArgsConstructor 5가지 어노테이션 기능을 전부 수행

* 반복적인 작업을 단순화 => 간결성을 높힘
* ❗다만 @Setter 의 무분별한 남용, @ToString 의 양방향 연관관계 시 순환 참조 등 다양한 보안/성능 문제가 일어날 수 있으므로 각각의 어노테이션의 기능을 사용해야되는 경우를 제외하고는 지양하거나 따로 명시해서 작성할 수 있도록 한다.

🗒️example 

```java
@Data
public class Person {

    private String name;
    private int age;
    private String sex;

}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        person.setName("아무개");
    }
}
```
<br><br>

### @Builder
> immutable 한 객체를 생성하기 위한 빌더 패턴을 자동으로 생성한다.

* 주로 객체를 생성할 때 특정 필드만 설정하고자 할 때 사용된다.

🗒️example 

```java

```
<br><br>