# 목차
- [작게 만들어라!](#작게-만들어라!)
  - [블록과 들여쓰기](#블록과-들여쓰기)


<br>

# 작게 만들어라!

함수를 만드는 첫째 규칙은 `작게` 이다.

둘째 규칙은 `더 작게` 이다.

그렇다면 열마나 짧아야 좋을까?

→ 일반적으로 아래와 같이 짧아야 한다.

```java
public statis String renderPageWithSetupsAndTearDowns(
	PageData pageData, boolean isSuite) throws Exception{
	if (isTestPage(pageData))
		includeSetupAndTeardownPage(pageData, isSuite);
	return pageData.getHtml();
}
```

### 블록과 들여쓰기

if문, else문, while믄 등 들어가는 블록은 한 줄이어야 한다. → 여기서 함수 호출한다. 

⭐ **함수는 중첩 구조가 생길만큼 커지면 안되며 들여쓰기는 1단이나 2단을 넘어서면 안된다.**

**➕ 블록안에서 적절한 이름의 함수를 호출한다면 good**
