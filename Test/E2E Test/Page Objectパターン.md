# Page Objectパターン
E2Eテストでウェブページを1:1でオブジェクト化してテストする方法
- マーティン・ファウラーのPage Object
    - https://martinfowler.com/bliki/PageObject.html
- Selenium githubのPage Object 
    - https://github.com/SeleniumHQ/selenium/wiki/PageObjects
- ページオブジェクトパターンとマッパーを使ったメンテナンスしやすいSeleniumテストケース
    - https://jappy.hatenablog.com/entry/20130525/1369490309

## メリット
- テストコードがシンプルになって可読性が上がる。
- WebElementの操作（「By.name("q")」や「sendKeys()」）がページクラス側に閉じるので、メンテナンス性が高くなる。
- アプリケーションの画面を修正した時に、テストメソッドを１個１個直していくのではなく、ページクラスの該当箇所を修正するだけになる。
- テストコード側でリファクタリングが使える。Theoriesランナーを使ったデータ駆動テストとも、相性がよい。

## 例
Googleで ストアクリエイターpro を検索し、結果ページの結果が 10個ということと一番目のタイトルが ストアクリエイターPro - Yahoo! JAPANということをチェックする。

### ページオブジェクトパターン適用前
#### Selenium
```Java
@Test
public void testGoogleSearch() {
    WebDriver driver = new FirefoxDriver();
    driver.get("http://www.google.com");
  
    WebElement element = driver.findElement(By.name("q"));
    element.sendKeys("ストアクリエイターPro\n");
    element.submit();
  
    List<WebElement> findElements = driver.findElements(By.xpath("//*[@id='rso']//h3/a"));
  
    assertEquals(10, webElement.size());
    assertEquals("ストアクリエイターPro - Yahoo! JAPAN", webElement.get(0).getText());
}
```

### ページオブジェクトパターン適用前
#### Selenium
```Java
@Test
public void testGoogleSearchWithPageObjectPattern() {
    WebDriver driver = new FirefoxDriver();
    driver.get("http://www.google.com");
  
    GoogleSearch searchPage = new GoogleSearch(driver);
    searchPage.setKeywords("ストアクリエイターPro");
  
    GoogleSearchResult resultPage = searchPage.search();
  
    assertEquals(10, resultPage.total());
    assertEquals("ストアクリエイターPro - Yahoo! JAPAN", resultPage.firstSectionTitle());
}
```

#### Selenide
```Java
@Test
public void selenidePageObjectModelPattern() {
    GoogleSearch searchPage = open("http://www.google.com", GoogleSearch.class);
    GoogleResults resultPage = searchPage.keywordSearchBy("selenide");
  
    resultPage.firstSectionTitle().shouldBe(text("ストアクリエイターPro - Yahoo! JAPAN"));
    resultPage.getResult().shouldHave(sizeGreaterThan(0));
    resultPage.getResult().shouldHaveSize(10);
}
```

#### Geb
```Groovy
Browser.drive {
    to GoogleHomePage
  
    search "ストアクリエイターPro - Yahoo! JAPAN"
  
    at GoogleResultsPage
  
    firstResultLink.text().contains("ストアクリエイターPro - Yahoo! JAPAN")
    resultSize() == 10
}
```
