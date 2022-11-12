# 클래스와 객체

## 객체(Object)란?

- “의사나 행위가 미치는 대상” - 사전적 의미
- 구체적, 추상적 데이터 단위

## 클래스란?

- 객체에 대한 속성과 기능을 코드로 구현한 것
- “클래스를 정의 한다”라고 함
- 클래스 이름은 대문자로 시작해야 됨!

ex)

```java
public classs Student{
	int studentID;
	String studentName;
	int grade;
	String address;

	public void showStudentInfo(){ //메서드
		system.out.println(studentName + "," + address);
	}

	public static void main(String[] args){
		Student studentLee = new Student();
		studentLee.studentName = "이순신";
		studendLee.address = "서울시";
		
		studentLee.showStudentInfo();
	}
}
```

## 메서드란?

- 함수의 일종
- 객체의 기능을 제공하기 위해 클래스 내부에 구현되는 함수

## 함수란?

- 하나의 기능을 수행하는 일련의 코드
- 중복되는 기능은 함수로 구현하여 함수를 호출하여 사용함

![1](https://user-images.githubusercontent.com/48826098/201466099-3a7c4964-bf27-4106-8e1f-f731a7ee1065.jpg)

## 함수와 스택 메모리

- 함수가 호출될 때 사용하는 메모리 → 스택(stack)

![메모리 구조](https://user-images.githubusercontent.com/48826098/201466106-0893451c-ea19-4901-9d0c-f51e4de731fb.png)

메모리 구조

## class & instance

### class 생성 방법

- 클래스를 사용하기 위해서는 클래스를 생성해야 됨
- new 예약어를 이용하여 클래스 생성

```java
Student studentA = new Student();
```

### 인스턴스와 힙 메모리

- 하나의 클래스 코드로부터 여러 개의 인스턴스를 생성
- 인스턴스는 힙메모리에 생성됨
- 각각의 인스턴스는 다른 메모리에 다른 값을 가짐
- 힙 메모리는 동적으로 할당 됨 (new 라는 키워드로 생성됨)

![2](https://user-images.githubusercontent.com/48826098/201466101-29d6fa46-9c23-46a6-aa9a-7949dc00fade.jpg)

## 생성자

- 기본 생성자는 JVM이 넣어줌
- 생성자가 하나라도 있으면 제공안해줌
- 생성자 오버로드 → 같은 이름의 생성자가 여러개 있을 수도 있음

```java
publc class Student{
	int studentID;
	String studentName;
	int grade;
	String address;

	public Student(){} // 기본 생성자

	public Student(int id, String name){ //생성자 : 처음 생성할 때 무조건 id랑 name값 지정해줘야 됨
		studentID = id;
		studentName = name;
	}
}
```

## 참조 자료형

### 변수의 자료형

[변수 자료형]

1. 기본 자료형
- int
- long
- float
- double …

1. 참조 자료형
- String
- Date
- Student …

```java
public class Student{
	int studentID;
	String studentName;

	Subject korea; // 이렇게 하는게 참조 자료형!
	Subject math;

	public Student(){
		korea = new Subject();
		math = new Subject(); // 각 과목에 대한 인스턴스 생성
	}

}

public class Subject{
	String subjectName;
	int score;
}
```

## 정보 은닉

### private 접근 제어자

- 클래스의 외부에서 클래스 내부의 멤버 변수나 메서드에 접근하지 못하게 하는 경우 사용
- 멤버 변수나 메서드를 외부에서 사용하지 못하도록 하여 오류를 줄일 수 있음
- 변수에 대해서는 필요한 경우 get(), set() 메서드를 제공 → getter, setter는 public으로 열어줘서 접근 할 수 있게 함.

## this

- 자신의 메모리를 가리킴
- 생성자에서 다른 생성자를 호출
- 자신의 주소를 반환 함

```java
class Birthday{
	int day;
	
	public void setDay(int day){
		this.day = day;
	}
}
```

## static 변수

```java
**static** int serialNum;
```

- 여러 개의 인스턴스가 같은 메모리의 값을 공유하기 위해 사용
- 인스턴스가 생성될 때마다 다른 메모리를 가지는 것이 아니라 프로그램이 메모리에 적재될 때 데이터 영역의 메모리에 생성됨
- 따라서 인스턴스의 생성과 관계없이 클래스 이름으로 직접 참조 함
- 클래스 변수라고도 함
- 멤버변수는 다른 말로 인스턴스 변수라고 함

![3](https://user-images.githubusercontent.com/48826098/201466102-93891339-60ef-4ed8-a857-ae3803975dca.jpg)

## singleton 패턴

```java
public class Company {
	private static Company instance = new Company(); 

	private Company(){}

	public static Company getInstance(){
		return instance;		
	}
}
```

```java
public class CompanyTest{
	public static void main(String[] args){

		Company c = new Company(); --> ERROR!!!!!

		Company c1 = company.getInstance();
	}
}
```

# 배열 & ArrayList

## 배열

- 배열은 동일한 자료형의 변수를 한꺼번에 순차적으로 관리할 수 있다.

```java
자료형[] 배열이름 = new 자료형[개수];

int[] arr = new int[10]; ->총 40

//선언과 동시에 초기화
int[] arr = new int[]{0,1,2};
int[] arr = {0,1,2}; // JAVA에서 자주 쓰는 문법은 아님
```

### 객체배열

- 참조 자료형을 선언하는 객체 배열
- 배열만 생성 한 경우 요소는 null로 초기화 됨
- 각 요소를 new를 활용하여 생성하여 저장함

```java
// Book 클래스를 미리 만들었다고 가정, 책 제목하고 저자가 들어있음

public class BookArray{
	public static void main(String[] args){
		Book[]  library = new Book[2];

		library[0] = new Book("어린왕자", "생텍쥐페리");
		library[1] = new Book("토지", "박경리");
	}
}
```

![4](https://user-images.githubusercontent.com/48826098/201466103-9f993c2c-3073-47c8-a772-e24d16a7ec17.jpg)

얕은 복사

## 다차원 배열

- 2차원 이상의 배열
- 지도, 게임 등 평면이나 공간을 구현할 때 많이 사용 됨

```java
int[][] arr = new int[2][3]; // 2차원 배열 선언

int[][] arr = {{1,2,3},{4,5,6}}; //선언과 동시에 초기화
```

## ArrayList

- 기존 배열은 길이를 정하여 선언하므로 사용 중 부족한 경우 다른 배열로 복사하는 코드를 직접 구현해야 함
- 중간의 요소가 삭제되거나 삽입되는 경우도 나머지 요소에 대한 조정하는 코드를 구현해야 함
- ArrayList 클래스는 자바에서 제공되는 객체 배열이 구현된 클래스
- 여러 메서드와 속성등 사용하여 객체 배열을 편리하게 관리할 수 있음
- 가장 많이 사용하는 객체 배열 클래스

```java
ArrayList<String> slist = new ArrayList<String>();
```