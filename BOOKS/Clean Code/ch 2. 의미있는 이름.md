# 목차
- [의도를 분명히 밝혀라](#의도를-분명히-밝혀라)
- [그릇된 정보를 피하라](#그릇된-정보를-피하라)
- [의미있게 구분하라](#의미-있게-구분하라)
- [발음하기 쉬운 이름을 사용하라](#발음하기-쉬운-이름을-사용하라)
- [검색하기 쉬운 이름을 사용하라](#검색하기-쉬운-이름을-사용하라)
- [인코딩을 피해라](#인코딩을-피해라)
	- [헝가리식 표기법](#헝가리식-표기법)
	- [멤버 변수 접두어](#멤버-변수-접두어)
	- [인터페이스 클래스와 구현 클래스](#인터페이스-클래스와-구현-클래스)
- [자신의 기억력을 자랑하지 마라](#자신의-기억력을-자랑하지-마라)
- [클래스 이름](#클래스-이름)
- [메서드 이름](#메서드-이름)
- [기발한 이름은 피하라](#기발한-이름은-피하라)
- [한 개념에 한 단어를 사용하라](#한-개념에-한-단어를-사용하라)
- [말장난을 하지 마라](#말장난을-하지-마라)
- [해법 영역에서 가져온 이름을 사용하라](#해법-영역에서-가져온-이름을-사용하라)
- [문제 영역에서 가져온 이름을 사용하라](#문제-영역에서-가져온-이름을-사용하라)
- [의미 있는 맥락을 추가하라](#의미-있는-맥락을-추가하라)
- [불필요한 맥락을 없애라](#불필요한-맥락을-없애라)

---


# 의도를 분명히 밝혀라

좋은 이름을 짓기 위해서는 시간이 많이 들지만 좋은 이름으로 절약하는 시간은 훨씬 더 많다.

**변수, 함수나 클래스와 같이 존재 이유, 수행 기능을 따로 주석처리 해야한다면 의도를 분명히 드러내지 않았다는 것이다.** 

```java
int d;
```

이것은 무엇을 의미할까? 

시간?거리? 위에 설명한 것처럼 주석이 없으면 변수의 의도와 의미는 알아채기 힘들다. 

<br>
따라서 변수는 다음과 같이 의미있는 이름으로 지어야 한다.

```java
int fileAgeInDays;
```

<br><br>

그럼 다음과 같은 코드가 있다고 하자. 

```java
public list<int[]> getThem(){
	List<int[]> list1 = new ArrayList<int[]>();
	for (int[] x : theList)
		if (x[0] == 4)
			list1.add(x);
	return list1;
}
```

겨우 6줄밖에 안되는 코드를 이해하는 것은 어렵다.

이 코드의 문제점은 단순성이 아니라 코드의 `함축성`이다. 

**👉 코드의 맥락이 코드 자체에 명시적으로 드러나지 않는다.**

<br><br>

위 코드에는 주석 없이 정보 제공이 가능했음에도 불구하고 어떠한 정보도 들어있지 않다.

위 코드와 같은 코드로 지뢰찾기 게임을 만든다고 가정한다. 
<br>

그럼 theList는 게임판이며, 이 변수를 gameBoard라고 바꿔보자.

```java
public List<int[]> gatFlaggedCells(){
	List<int[]> flaggedCells = new ArrayList<int[]>();
	for (int[] cell : gameBoard)
		if (cell [STATUS_VALUE] == FLAGGED)
			flaggedCells.add(cell);
	return flaggedCells;
} 
```

> 처음 코드와 비교해서 0번째 값은 칸 상태를 뜻하며, 4는 깃발이 꽂힌 상태를 가리킨다.
> 

**코드의 단순성은 변하지 않았지만 개념에 이름을 붙임으로써 코드는 더욱 명확해졌다.**

<br><br>

➕ 배열을 사용하지 않고 함수를 사용해서 더 명시적으로 바꿀 수도 있다.

```java
public List<int[]> gatFlaggedCells(){
	List<int[]> flaggedCells = new ArrayList<int[]>();
	for (int[] cell : gameBoard)
		if (cell.isFlagged())
			flaggedCells.add(cell);
	return flaggedCells;
} 
```

> 깃발이 꽂혔는지 여부를 함수로 나타낸다면 더 명시적으로 바꿀 수 있다.
>

<br><br>

# 그릇된 정보를 피하라

✏️ **그릇되다**는 ‘어떤 일이 사리에 맞지 아니하다’라는 뜻이다. 
<br>
- 프로그래머는 코드에 그릇된 단서를 남겨서는 안된다.
- 널리 쓰이는 의미가 있는 단어를 다른 의미로 사용해도 안된다.

> **EX)** hp, aix, sco는 변수 이름으로 적합하지 않다.
유닉스 플랫폼이나 유닉스 변종을 가리키는 이름이기 때문이다.
직각 삼각형의 빗변(hypotenuse)을 구현할 때는 hp가 훌륭한 약어처럼 보이지만 그릇된 정보를 제공하는 것이다.
> 
- 여러 계정을 묶을 때 실제 List가 아니라면 List라는 이름을 사용해서도 안된다.
- 서로 흡사한 이름을 사용하지 않도록 주의한다.
- 유사한 개념은 유사한 표기법을 사용한다. → 일관성이 떨어지는 표기법은 `그릇된 정보`이다.
<br>

🌱 이름으로 그릇된 정보를 제공하는 끔찍한 예가 소문자 L이나 대문자 O이다. 

**why? 소문자 L은 숫자 1처럼 보이고, 대문자 O는 숫자 0처럼 보이기 때문이다.**

<br><br>

# 의미 있게 구분하라

**이름이 달라야 한다면 의미도 달라져야 한다.**

✏️ 불용어는 ‘의미가 없는 단어’를 의미한다.

- 불용어 사용을 지양한다.

> ProductInfo랑 ProductData는 어떤 의미의 차이가 있는가. 개념을 딱히 구분하지 않은채 불용어인 Info, Data를 붙인 것이다. 

> `getActiveAccount()`, `getActiveAccounts()`, `getActiveAccountInfo()` 중에 이 프로젝트에 참여한 프로그래머는 어느 함수를 호출할지 어떻게 알까? 

**⭐ 읽는 사람이 차이를 알도록 이름을 지어라**


<br><br>

# 발음하기 쉬운 이름을 사용하라

```java
class DtaRcrd102{
	private Date genymdhms;
	private Date modymdhms;
	private final String qszqint = "102";
};
```

```java
class Customer{
	private Date generationTimestamp;
	private Date modificationTimestamp;
	private final String recordId = "102";
};
```

둘 중 비교해보자. 무엇이 더 좋은 코드이겠는가?

첫 번째도 충분히 사용가능 할 수 있다. 

실제로 어느 회사는 genymdhms(generate date, year, month, day, hour, minute, second)라는 단어를 사용한다. 이 단어를 말하기 쉽게 “젠 와이 엠 디 에이취 엠 에스”라고 발음하거나 “젠 야 무다 힘즈”라고 발음 할 수도 있다. 

하지만 이 단어는 새로운 직원이 온다면 일일이 설명을 해주어야 한다.

**따라서, 지적인 대화가 가능하게 하려면 두 번째 처럼 generationTimestamp같은 단어를 사용하자.**

<br><br>

# 검색하기 쉬운 이름을 사용하라

문자 하나를 사용하는 이름과 상수는 텍스트 코드에서 쉽게 눈에 띄지 않는다는 문제점이 있다.

🌱 `e` 라는 문자는 변수 이름으로 적절하지 않다. 영어에서 가장 많이 쓰이는 문자이다. 

따라서 검색이 어렵다. **이런 관점에서는긴 이름이 짧은 이름보다 좋다.**
<br>

**즉 검색하기 쉬운 이름이 상수보다 좋다.**

```java
for (int j = 0; j <34; j++){
	s += (t[j]*4)/5;
}
```

```java
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEKS = 5;
int sum = 0;
for (int j = 0; j <NUMBER_OF_TASKS; j++){
	int realTaskDays = taskEsimate[j] + realDaysPerIdealDay;
	int realTaskWeeks = (realTaskDays / WORK_DAYS_PER_WEEKS);
	sum += realTaskWeeks;
}
```

> 위 두 코드를 비교해보자. s대신 사용한 sum은 유용한 기능은 아니지만 최소한 검색은 가능하다.
하지만, WORK_DAYS_PER_WEEK를 찾기는 얼마나 쉬운가
> 
<br>

**⭐변수나 상수를 코드 여러 곳에서 사용한다면 검색하기 쉬운 이름을 사용하는 것이 바람직하다.**

<br><br>

# 인코딩을 피해라

✏️ **인코딩은** 문자를 컴퓨터가 이해할 수 있는 이진법으로 변환하는 것을 말한다.

(여기서는 뭔가..문자에 어떤 타입인지 어떤 유형인지 암호화하는 느낌인 듯하다.)

이름에도 인코딩할 정보가 아주 많은데 유형이나 범위 정보까지 인코딩하면 그만큼 이름을 해독하기 어려워진다. 

또한, 인코딩 `언어` 까지 익히라는 요구는 매우 비합리적이다.

<br>

### 헝가리식 표기법

→ 프로그래밍 언어에서 변수 및 함수의 인자 이름 앞에 데이터 타입을 명시하는 코딩 규칙이다.

- 포트란은 첫 글자로 유형을 표현했다.
- 초창기 베이식은 글자 하나에 숫자 하나만 허용했다.

과거에는 헝가리식 표기법을 굉장히 중요하게 생각했다.

👉 why? 과거에는 컴파일러가 타입을 점검하지 않았으므로 프로그래머에게 타입을 기억할 단서가 필요했다.
<br>

🌱 하지만 요즘 나오는 프로그래밍 언어는 훨씬 많은 타입을 지원할 뿐더러 컴파일러가 타입을 기억하고 강제한다. 

**따라서, 프로그래머는 변수 이름에 타입을 인코딩할 필요가 없어졌다.**

<br>

### 멤버 변수 접두어

이제는 멤버 변수에 m_이라는 접두어를 붙일 필요가 없다.

- 클래스와 함수는 접두어가 필요없을 정도로 작아야 한다.
- 멤버 변수를 다른 색상으로 표시하거나 눈에 띄게 보여주는 IDE를 사용해야 마땅하다.

<br>

### 인터페이스 클래스와 구현 클래스

때로는 인코딩이 필요한 경우가 있다.

> 도형을 생성하는 ABSTRACT FACTORY를 구현하기 위해서는 인터페이스 클래스와 구체 클래스가 필요하다.
> 

→ 두 클래스 이름을 어떻게 짓는게 좋을까?

🌱 인터페이스 클래스에 접두어 I를 붙이는 것은 주의를 흐트리고 과도한 정보를 제공한다. 

인터페이스 클래스 이름과 구현 클래스 이름 중 하나를 인코딩 해야 한다면 구현클래스 이름을 인코딩한다. 

**how?** `ShapeFactoryImp` 또는 `CShapeFactory`가 `IShapeFactory`보다 좋다.

<br><br>

# 자신의 기억력을 자랑하지 마라

> 독자가 코드를 읽으면서 변수 이름을 본인이 아는 이름으로 바꾸고 싶은 마음이 든다면 그 변수 이름은 바람직하지 못하다.
> 

**🌱 문자 하나만 사용하는 변수 이름은 문제가 있다. (but, 루프에서 반복 횟수를 세는 변수 i,k,j는 괜찮다.)**

⭐ **변수 r이 무엇인지 기억하는 프로그래머는 아주 똑똑하다.** 

**하지만 전문가 프로그래머는 남들이 이해하는 코드를 내놓는다.**

<br><br>

# 클래스 이름

**⭐ 클래스 이름과 객체 이름은 명사나 명사구가 적합하다.**

> **ex)** `Customer`, `WiKiPage`, `Account`, `AddressParser`


<br><br>

# 메서드 이름

**⭐메서드 이름은 동사나 동사구가 적합하다.**

> **ex)** `postPayment` , `deletePage` , `save`
> 

```java
Stirng name = employee.getName();
customer.setName("mike");
if (paycheck.isPost()) ...
```

> 접근자 → get <br>
변경자 → set <br>
조건자 → is <br>
> 

**🌱 생성자를 중복정의할 때는 정적 팩토리 메서드를 사용한다.**

```java
Complex fulcrumPoint = Complex.FromRealNumber(23.0); -> good
Complex fulcrumPoint = new Complex(23.0);

// 생성자 사용을 제한하려면 private로 선언하기!
```

<br><br>

# 기발한 이름은 피하라

**⭐ 재미난 이름보다 명료한 이름을 선택하라**

<br><br>

# 한 개념에 한 단어를 사용하라

똑같은 메서드를 클래스마다 각각 다르게 부르면 혼란스럽다.

각각의 이름을 기억하지 못하면 과거의 코드 예제나 헤더를 살피는데 시간이 많이 들게 된다.

이클립스나 인텔리제이 등 최신 IDE는 문맥에 맞는 단서를 제공해준다. 

하지만 어느 정도만 힌트를 줄 뿐 주석은 보여주지 않는다. 

> `DeviceManager` 와 `ProtocolController` 는 근본적으로 어떻게 다른가. 둘 다 controller? 둘 다 Manager? 이름이 다르면 당연히 타입과 역할이 다르다고 생각한다.
> 

<br>

**⭐주석을 뒤져보지 않고도 프로그래머가 올바른 메서드를 선택하기 위해서는 메서드 이름이 독자적이고 일관적이어야 한다.**

<br><br>

# 말장난을 하지 마라

프로그래머가 일관성을 위해 add라는 메서드를 통일해서 사용한다고 치자.

기존의 add는 두 개의 값을 더해 새로운 값을 도출해내는 용도로 사용했다.

하지만 중간에 갑자기 새로운 값이 더해진다면 이 메서드를 add라고 부를 수 있을까?

**NO! 이것은 일관성이 있는 것이 아니라 말장난이다.**

👉 이럴 경우에는 insert나 append라고 불러야 한다.

<br>

**⭐ 다른 개념에 같은 단어를 사용하지 말아라. 또한 한 단어를 두 가지 목적으로 사용하지 말아라.**

<br><br>

# 해법 영역에서 가져온 이름을 사용하라

코드를 짜는 사람도 읽는 사람도 프로그래머이다. 

따라서 `전산 용어`, `알고리즘 이름`, `패턴 이름` 등등을 사용하는 것은 문제가 되지 않는다. 

하지만 모든 이름을 문제 영역에서 가져오는 것은 현명하지 못하다. 

**⭐ 따라서, 프로그래머에게 익숙한 기술 개념을 사용하자.**

<br><br>

# 문제 영역에서 가져온 이름을 사용하라

**적절한 `프로그래머 용어` 가 없다면 문제 영역에서 이름을 가져온다.**

> 우수한 프로그래머와 설계자라면 해법 영역과 문제 영역은 구분할 줄 알아야 한다. 
문제 영역과 관련된 코드라면 문제 영역에서 이름을 가져온다.
>


<br><br>

# 의미 있는 맥락을 추가하라

firstName, lastName, street, houseNumber를 쭉 훑어보면 주소 변수를 의미한다는 것을 알 수 있다. 하지만 firstName만 사용한다면 무슨 의미인지 알 수 있을까?

이럴 때는 addr라는 접두어를 추가하면 무슨 의미인지 알 수 있다.

이렇게 맥락을 추가하는 것이 좋다.

```java
private void printGuessStatistics(char candidate, int count){
	String number;
	String verb;
	String pluralModifier;
	if (count == 0){
		number = "no";
		verb = "are";
		pluralModifier = "s";
	} else if (count == 1){
		number = "1";
		verb = "is";
		pluralModifier = "";
	} else{
		number = Integer.toString(count);
		verb = "are";
		pluralModifier = "s";
	}
	String guessMessage = String.format("There %s %s %s%s", verb, number, candidate, pluralModifier);
	print(guessMessage);
}
```

> 이 코드에서 함수는 맥락 일부만을 제공하며 알고리즘이 나머지 맥락을 제공한다. 
다 읽고 나서야 `number`, `verb`, `pluralModifier` 라는 변수가 `통계 추측` 에 사용된다는 것을 알 수 있다. 독자가 맥락을 유추해야 한다는 뜻이다.
> 

<br>

맥락이 분명해지게 만들어보자.

GuessStaticsMessage라는 클래스를 만들고 변수를 클래스에 넣어서 맥락을 분명하게 만든다.

```java
public class GuessStaticsMessage{
	private String number;
	private String verb;
	private String pluralModifier;

	public String make(char candidate, int count){
		createPluralDependentMessage(count);
		return String.format("There %s %s %s%s", verb, number, candidate, pluralModifier);
	}

	private void createPluralDependentMessageParts(int count){
		if (count == 0){
			threrAreNoLetters();
		}else if (count == 1){
			thereIsOneLetter();
		}else{
			thereAreManyLetters();
		}
	}

	private void thereAreManyLetters(int count){
		number = Integer.toString(count);
		verb = "are";
		pluralModifier = "s";
	}
	
	private void thereIsOneLetter(){
		number = "1";
		verb = "is";
		pluralModifier = "";
	}

	private void thereNoLetters(){
		number = "no";
		verb = "are";
		pluralModifier = "s";
	}
}
```
<br>

**⭐ 대다수의 이름은 스스로 의미가 분명하지 않다. 따라서 클래스, 함수, 이름 공간에 넣어 맥락을 부여한다. 모든 방법이 실패하면 마지막 수단으로 접두어를 붙인다.**

<br><br>

# 불필요한 맥락을 없애라

`accountAddress` 와 `customerAddress` 는 Address 클래스 인스턴스로는 좋은 이름이지만 클래스 인스턴스로는 적합하지 못하다. 

`Address`는 클래스 이름으로 적합하다.

만약 포트 주소, MAC 주소, 웹 주소를 구분해야 한다면 `PostalAddress`, `MAC`, `URI`라는 이름이 적합할 것이다.

**⭐ 일반적으로는 짧은 이름이 긴 이름보다 좋다. 단, 의미가 분명한 경우에 한해서다. 이름에 불필요한 맥락을 추가하지 않도록 주의한다.**
