# 목차
- [의도를 분명히 밝혀라](#의도를-분명히-밝혀라)


---

# 의도를 분명히 밝혀라

좋은 이름을 짓기 위해서는 시간이 많이 들지만 좋은 이름으로 절약하는 시간은 훨씬 더 많다.

**변수, 함수나 클래스와 같이 존재 이유, 수행 기능을 따로 주석처리 해야한다면 의도를 분명히 드러내지 않았다는 것이다.** 

```java
int d;
```

이것은 무엇을 의미할까? 

시간?거리? 위에 설명한 것처럼 주석이 없으면 변수의 의도와 의미는 알아채기 힘들다. 


따라서 변수는 다음과 같이 의미있는 이름으로 지어야 한다.

```java
int fileAgeInDays;
```



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



위 코드에는 주석 없이 정보 제공이 가능했음에도 불구하고 어떠한 정보도 들어있지 않다.

위 코드와 같은 코드로 지뢰찾기 게임을 만든다고 가정한다. 


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