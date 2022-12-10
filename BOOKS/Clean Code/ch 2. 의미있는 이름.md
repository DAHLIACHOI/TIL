# 목차
- [의도를 분명히 밝혀라](#의도를-분명히-밝혀라)
- [그릇된 정보를 피하라](#그릇된-정보를-피하라)
- [의미있게 구분하라](#의미-있게-구분하라)
- [발음하기 쉬운 이름을 사용하라](#발음하기-쉬운-이름을-사용하라)
- [검색하기 쉬운 이름을 사용하라](#검색하기-쉬운-이름을-사용하라)

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
