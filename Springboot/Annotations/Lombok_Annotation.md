## Lombok Annotation
### @NoArgsConstructor
> 매개변수가 없는 기본 생성자를 생성한다.

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