# SDET Java - 90-Day Master Roadmap (24 LPA → 40 LPA)

---

## Overview & Strategy

| Phase | Duration | Focus | Goal |
|-------|----------|-------|------|
| Phase 1 | Week 1-2 | Core Java | Strong foundation |
| Phase 2 | Week 3-5 | Selenium + TestNG/JUnit | UI Automation Pro |
| Phase 3 | Week 6-7 | API Testing | RestAssured Expert |
| Phase 4 | Week 8-9 | CI/CD + DevOps Tools | Pipeline Integration |
| Phase 5 | Week 10-11 | Advanced Topics | Teach-level mastery |
| Phase 6 | Week 12 | Portfolio + Interview Prep | Land 40 LPA job |

---

## PHASE 1: Core Java (Days 1-14)

### Day 1 — Java Setup + Basics
**Topics:** JDK install, IDE setup, Hello World, data types, variables

**Example:**
```java
public class Day1 {
    public static void main(String[] args) {
        int age = 30;
        String name = "SDET";
        boolean isActive = true;
        double salary = 24.5;
        System.out.println("Name: " + name + ", Age: " + age);
    }
}
```

**Resources:**
- https://www.javatpoint.com/java-tutorial
- YouTube: "Telusko Java Tutorial" (free, excellent)

---

### Day 2 — Operators, Conditionals, Loops
**Topics:** if/else, switch, for, while, do-while

**Example:**
```java
// Loop through test cases
for (int i = 1; i <= 5; i++) {
    System.out.println("Running Test Case: TC_00" + i);
}

// Switch for browser selection
String browser = "chrome";
switch(browser) {
    case "chrome": System.out.println("Launching Chrome"); break;
    case "firefox": System.out.println("Launching Firefox"); break;
    default: System.out.println("Unknown browser");
}
```

---

### Day 3 — Arrays + Strings
**Topics:** String methods, Arrays, String manipulation

**Example:**
```java
String url = "  https://www.google.com  ";
System.out.println(url.trim());
System.out.println(url.contains("google"));
System.out.println(url.replace("google","amazon"));

String[] browsers = {"chrome", "firefox", "edge"};
for(String b : browsers) {
    System.out.println("Test on: " + b);
}
```

**Resources:**
- https://www.w3schools.com/java/java_strings.asp

---

### Day 4 — OOP Part 1: Classes, Objects, Constructors
**Topics:** Class, Object, Constructor, `this` keyword

**Example:**
```java
public class TestConfig {
    String browser;
    String url;
    int timeout;

    public TestConfig(String browser, String url, int timeout) {
        this.browser = browser;
        this.url = url;
        this.timeout = timeout;
    }

    public void printConfig() {
        System.out.println("Browser: " + browser + " | URL: " + url);
    }

    public static void main(String[] args) {
        TestConfig config = new TestConfig("chrome", "https://amazon.com", 30);
        config.printConfig();
    }
}
```

---

### Day 5 — OOP Part 2: Inheritance + Polymorphism
**Topics:** extends, super, method overriding, @Override

**Example:**
```java
public class BaseTest {
    public void setUp() {
        System.out.println("Browser launched");
    }
    public void tearDown() {
        System.out.println("Browser closed");
    }
}

public class LoginTest extends BaseTest {
    @Override
    public void setUp() {
        super.setUp();
        System.out.println("Navigating to Login page");
    }

    public void testValidLogin() {
        System.out.println("Testing valid login");
    }
}
```

---

### Day 6 — OOP Part 3: Encapsulation + Abstraction + Interface
**Topics:** private, getters/setters, abstract class, interface

**Example:**
```java
interface BrowserDriver {
    void openBrowser();
    void closeBrowser();
    void navigateTo(String url);
}

abstract class BaseDriver implements BrowserDriver {
    public void navigateTo(String url) {
        System.out.println("Navigating to: " + url);
    }
}

class ChromeDriver extends BaseDriver {
    public void openBrowser() { System.out.println("Chrome opened"); }
    public void closeBrowser() { System.out.println("Chrome closed"); }
}
```

---

### Day 7 — Collections: List, Set, Map
**Topics:** ArrayList, LinkedList, HashSet, HashMap, iteration

**Example:**
```java
import java.util.*;

public class CollectionsDemo {
    public static void main(String[] args) {
        List<String> testSteps = new ArrayList<>();
        testSteps.add("Open browser");
        testSteps.add("Enter URL");
        testSteps.add("Click login");

        Map<String, String> testData = new HashMap<>();
        testData.put("username", "admin@test.com");
        testData.put("password", "Admin@123");
        System.out.println("User: " + testData.get("username"));

        Set<String> browsers = new HashSet<>();
        browsers.add("chrome");
        browsers.add("chrome"); // ignored
        browsers.add("firefox");
        System.out.println(browsers); // [chrome, firefox]
    }
}
```

---

### Day 8 — Exception Handling
**Topics:** try/catch/finally, throws, custom exceptions

**Example:**
```java
public class ExceptionDemo {

    static class TestFailedException extends RuntimeException {
        public TestFailedException(String message) {
            super("TEST FAILED: " + message);
        }
    }

    public static void clickElement(String element) {
        try {
            if (element == null) throw new NullPointerException();
            System.out.println("Clicked: " + element);
        } catch (NullPointerException e) {
            throw new TestFailedException("Element not found: " + element);
        } finally {
            System.out.println("Screenshot captured");
        }
    }

    public static void main(String[] args) {
        clickElement(null);
    }
}
```

---

### Day 9 — File Handling + Properties Files
**Topics:** FileReader, Properties, reading config files

**Example:**
```java
// config.properties file:
// browser=chrome
// url=https://www.google.com
// timeout=30

import java.util.Properties;
import java.io.FileInputStream;

public class ConfigReader {
    private Properties props = new Properties();

    public ConfigReader() throws Exception {
        FileInputStream fis = new FileInputStream("src/test/resources/config.properties");
        props.load(fis);
    }

    public String getBrowser() { return props.getProperty("browser"); }
    public String getUrl() { return props.getProperty("url"); }
    public int getTimeout() { return Integer.parseInt(props.getProperty("timeout")); }

    public static void main(String[] args) throws Exception {
        ConfigReader config = new ConfigReader();
        System.out.println("Browser: " + config.getBrowser());
    }
}
```

---

### Day 10 — Java 8 Features (Critical for SDET)
**Topics:** Lambda, Stream API, Optional, Functional interfaces

**Example:**
```java
import java.util.*;
import java.util.stream.*;

public class Java8Demo {
    public static void main(String[] args) {
        List<String> testCases = Arrays.asList("TC001_Login", "TC002_Logout",
                                                "TC003_Login", "TC004_Search");

        List<String> loginTests = testCases.stream()
            .filter(tc -> tc.contains("Login"))
            .distinct()
            .sorted()
            .collect(Collectors.toList());

        loginTests.forEach(System.out::println);

        testCases.stream()
            .map(String::toUpperCase)
            .forEach(System.out::println);
    }
}
```

---

### Day 11 — Generics + Enums
**Topics:** Generic classes, methods, Enum for test data

**Example:**
```java
public class TestResult<T> {
    private T data;
    private boolean passed;
    private String message;

    public TestResult(T data, boolean passed, String message) {
        this.data = data;
        this.passed = passed;
        this.message = message;
    }
}

enum Environment {
    DEV("https://dev.app.com"),
    QA("https://qa.app.com"),
    STAGING("https://staging.app.com"),
    PROD("https://prod.app.com");

    private final String url;
    Environment(String url) { this.url = url; }
    public String getUrl() { return url; }
}

// Usage
Environment env = Environment.QA;
System.out.println("Running on: " + env.getUrl());
```

---

### Day 12 — Design Patterns for Test Automation
**Topics:** Singleton, Factory, Page Object Model concept

**Example:**
```java
// Singleton - Single WebDriver instance
public class DriverManager {
    private static DriverManager instance;

    private DriverManager() {}

    public static DriverManager getInstance() {
        if (instance == null) {
            synchronized(DriverManager.class) {
                if (instance == null) {
                    instance = new DriverManager();
                }
            }
        }
        return instance;
    }
}

// Factory - Create different drivers
public class DriverFactory {
    public static Object createDriver(String browserName) {
        switch(browserName.toLowerCase()) {
            case "chrome": return "ChromeDriver Created";
            case "firefox": return "FirefoxDriver Created";
            default: throw new IllegalArgumentException("Unknown: " + browserName);
        }
    }
}
```

---

### Day 13 — Maven Build Tool
**Topics:** pom.xml, dependencies, plugins, lifecycle

**Example pom.xml:**
```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.sdet</groupId>
    <artifactId>automation-framework</artifactId>
    <version>1.0</version>

    <dependencies>
        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>4.18.1</version>
        </dependency>
        <dependency>
            <groupId>org.testng</groupId>
            <artifactId>testng</artifactId>
            <version>7.9.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.2.5</version>
                <configuration>
                    <suiteXmlFiles>
                        <suiteXmlFile>testng.xml</suiteXmlFile>
                    </suiteXmlFiles>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

**Resources:**
- https://maven.apache.org/guides/getting-started/

---

### Day 14 — Git + GitHub
**Topics:** init, clone, add, commit, push, pull, branch, merge

**Commands to master:**
```bash
git init
git clone https://github.com/repo.git
git checkout -b feature/login-tests
git add .
git commit -m "Add login automation tests"
git push origin feature/login-tests
git pull origin main
git merge main
git log --oneline
git stash
git stash pop
```

**Resources:**
- https://learngitbranching.js.org (interactive, best resource)

---

## PHASE 2: Selenium + TestNG/JUnit (Days 15-35)

### Day 15 — Selenium Introduction + Setup
**Topics:** WebDriver, ChromeDriver, basic operations

**Example:**
```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class FirstSeleniumTest {
    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();
        driver.get("https://www.google.com");
        System.out.println("Title: " + driver.getTitle());
        driver.quit();
    }
}
```

---

### Day 16 — Locators (Critical Day)
**Topics:** ID, Name, Class, XPath, CSS Selector, LinkText

**Example:**
```java
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;

public class LocatorsDemo {
    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();
        driver.get("https://www.saucedemo.com");

        driver.findElement(By.id("user-name")).sendKeys("standard_user");
        driver.findElement(By.name("password")).sendKeys("secret_sauce");
        driver.findElement(By.cssSelector("input[data-test='login-button']")).click();

        // XPath - relative (preferred)
        driver.findElement(By.xpath("//input[@id='user-name']"));
        driver.findElement(By.xpath("//button[text()='Login']"));
        driver.findElement(By.xpath("//div[@class='error-message']//h3"));

        driver.quit();
    }
}
```

**XPath Cheat Sheet:**
```
//tagname[@attribute='value']      → //input[@id='email']
//tagname[text()='text']           → //button[text()='Submit']
//parent/child                     → //form/input
//ancestor//descendant             → //div[@class='form']//input
contains(@attr,'partial')          → //input[contains(@id,'user')]
starts-with(@attr,'val')           → //input[starts-with(@name,'pass')]
```

---

### Day 17 — WebDriver Commands
**Topics:** navigate, window, browser actions

**Example:**
```java
driver.get("https://google.com");
driver.navigate().to("https://amazon.com");
driver.navigate().back();
driver.navigate().forward();
driver.navigate().refresh();

driver.manage().window().maximize();
driver.manage().window().fullscreen();
System.out.println("Title: " + driver.getTitle());
System.out.println("URL: " + driver.getCurrentUrl());

driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
driver.manage().timeouts().pageLoadTimeout(Duration.ofSeconds(30));
```

---

### Day 18 — WebElement Interactions
**Topics:** click, sendKeys, clear, getText, isDisplayed, isEnabled

**Example:**
```java
WebElement emailField = driver.findElement(By.id("email"));

emailField.sendKeys("test@example.com");
emailField.clear();
emailField.click();

System.out.println("Visible: " + emailField.isDisplayed());
System.out.println("Enabled: " + emailField.isEnabled());
System.out.println("Selected: " + emailField.isSelected());
System.out.println("Text: " + emailField.getText());
System.out.println("Attr: " + emailField.getAttribute("placeholder"));
System.out.println("CSS: " + emailField.getCssValue("color"));
```

---

### Day 19 — Waits (Most Important for Stable Tests)
**Topics:** Implicit, Explicit, Fluent wait

**Example:**
```java
import org.openqa.selenium.support.ui.*;

// Implicit Wait - applied globally
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));

// Explicit Wait - for specific condition
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(20));

WebElement element = wait.until(
    ExpectedConditions.visibilityOfElementLocated(By.id("submit"))
);

wait.until(ExpectedConditions.elementToBeClickable(By.id("btn")));
wait.until(ExpectedConditions.textToBePresentInElement(element, "Success"));
wait.until(ExpectedConditions.urlContains("dashboard"));
wait.until(ExpectedConditions.alertIsPresent());

// Fluent Wait - polling with ignore exceptions
Wait<WebDriver> fluentWait = new FluentWait<>(driver)
    .withTimeout(Duration.ofSeconds(30))
    .pollingEvery(Duration.ofSeconds(2))
    .ignoring(NoSuchElementException.class);

fluentWait.until(d -> d.findElement(By.id("result")).isDisplayed());
```

---

### Day 20 — TestNG Framework
**Topics:** @Test, @BeforeMethod, @AfterMethod, Assertions, Groups

**Example:**
```java
import org.testng.annotations.*;
import org.testng.Assert;

public class LoginTest {
    WebDriver driver;

    @BeforeSuite
    public void globalSetup() {
        System.out.println("Test Suite Started");
    }

    @BeforeClass
    public void classSetup() {
        System.out.println("Test Class Started");
    }

    @BeforeMethod
    public void setUp() {
        driver = new ChromeDriver();
        driver.manage().window().maximize();
        driver.get("https://www.saucedemo.com");
    }

    @Test(priority = 1, groups = {"smoke"}, description = "Verify valid login")
    public void testValidLogin() {
        driver.findElement(By.id("user-name")).sendKeys("standard_user");
        driver.findElement(By.id("password")).sendKeys("secret_sauce");
        driver.findElement(By.id("login-button")).click();

        String currentUrl = driver.getCurrentUrl();
        Assert.assertTrue(currentUrl.contains("inventory"), "Login failed!");
        Assert.assertEquals(driver.getTitle(), "Swag Labs");
    }

    @Test(priority = 2, groups = {"smoke", "regression"})
    public void testInvalidLogin() {
        driver.findElement(By.id("user-name")).sendKeys("wrong_user");
        driver.findElement(By.id("password")).sendKeys("wrong_pass");
        driver.findElement(By.id("login-button")).click();

        String error = driver.findElement(By.cssSelector("[data-test='error']")).getText();
        Assert.assertTrue(error.contains("Username and password do not match"));
    }

    @AfterMethod
    public void tearDown() {
        driver.quit();
    }

    @AfterSuite
    public void globalTearDown() {
        System.out.println("All tests completed");
    }
}
```

**testng.xml:**
```xml
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="Regression Suite" parallel="methods" thread-count="3">
    <test name="Login Tests">
        <groups>
            <run>
                <include name="smoke"/>
            </run>
        </groups>
        <classes>
            <class name="tests.LoginTest"/>
        </classes>
    </test>
</suite>
```

---

### Day 21 — Page Object Model (POM) - Industry Standard Pattern

**Project Structure:**
```
src/
 └── test/
      ├── java/
      │    ├── pages/
      │    │    ├── BasePage.java
      │    │    ├── LoginPage.java
      │    │    └── DashboardPage.java
      │    ├── tests/
      │    │    └── LoginTest.java
      │    └── utils/
      │         └── DriverFactory.java
      └── resources/
           └── config.properties
```

**BasePage.java:**
```java
public class BasePage {
    protected WebDriver driver;
    protected WebDriverWait wait;

    public BasePage(WebDriver driver) {
        this.driver = driver;
        this.wait = new WebDriverWait(driver, Duration.ofSeconds(20));
        PageFactory.initElements(driver, this);
    }

    protected void click(WebElement element) {
        wait.until(ExpectedConditions.elementToBeClickable(element)).click();
    }

    protected void type(WebElement element, String text) {
        wait.until(ExpectedConditions.visibilityOf(element)).clear();
        element.sendKeys(text);
    }

    protected String getText(WebElement element) {
        return wait.until(ExpectedConditions.visibilityOf(element)).getText();
    }
}
```

**LoginPage.java:**
```java
import org.openqa.selenium.support.FindBy;
import org.openqa.selenium.support.PageFactory;

public class LoginPage extends BasePage {

    @FindBy(id = "user-name")
    private WebElement usernameField;

    @FindBy(id = "password")
    private WebElement passwordField;

    @FindBy(id = "login-button")
    private WebElement loginButton;

    @FindBy(css = "[data-test='error']")
    private WebElement errorMessage;

    public LoginPage(WebDriver driver) {
        super(driver);
    }

    public DashboardPage loginWithValidCredentials(String username, String password) {
        type(usernameField, username);
        type(passwordField, password);
        click(loginButton);
        return new DashboardPage(driver);
    }

    public String getErrorMessage() {
        return getText(errorMessage);
    }
}
```

**LoginTest.java:**
```java
public class LoginTest extends BaseTest {

    @Test
    public void validLoginRedirectsToDashboard() {
        LoginPage loginPage = new LoginPage(driver);
        DashboardPage dashboard = loginPage.loginWithValidCredentials(
            "standard_user", "secret_sauce"
        );
        Assert.assertTrue(dashboard.isLoaded(), "Dashboard not loaded");
    }
}
```

---

### Day 22 — Data-Driven Testing with TestNG DataProvider
**Topics:** @DataProvider, Excel reading with Apache POI

**Example:**
```java
@DataProvider(name = "loginData")
public Object[][] getLoginData() {
    return new Object[][] {
        {"standard_user", "secret_sauce", true},
        {"locked_out_user", "secret_sauce", false},
        {"wrong_user", "wrong_pass", false}
    };
}

@Test(dataProvider = "loginData")
public void testLogin(String username, String password, boolean shouldPass) {
    LoginPage loginPage = new LoginPage(driver);
    loginPage.enterUsername(username);
    loginPage.enterPassword(password);
    loginPage.clickLogin();

    if (shouldPass) {
        Assert.assertTrue(driver.getCurrentUrl().contains("inventory"));
    } else {
        Assert.assertTrue(loginPage.getErrorMessage().length() > 0);
    }
}

// Reading from Excel (Apache POI)
// Add to pom.xml: org.apache.poi:poi-ooxml:5.2.5
import org.apache.poi.xssf.usermodel.*;

public Object[][] getExcelData(String filePath, String sheetName) throws Exception {
    FileInputStream fis = new FileInputStream(filePath);
    XSSFWorkbook workbook = new XSSFWorkbook(fis);
    XSSFSheet sheet = workbook.getSheet(sheetName);

    int rows = sheet.getLastRowNum();
    int cols = sheet.getRow(0).getLastCellNum();

    Object[][] data = new Object[rows][cols];
    for (int i = 1; i <= rows; i++) {
        for (int j = 0; j < cols; j++) {
            data[i-1][j] = sheet.getRow(i).getCell(j).getStringCellValue();
        }
    }
    workbook.close();
    return data;
}
```

---

### Day 23 — Advanced Selenium: Actions, JavaScript, Screenshot

**Example:**
```java
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.TakesScreenshot;
import org.apache.commons.io.FileUtils;

public class AdvancedSelenium {
    WebDriver driver;
    Actions actions;
    JavascriptExecutor js;

    public void hoverAndClick(WebElement menu, WebElement subMenu) {
        actions = new Actions(driver);
        actions.moveToElement(menu)
               .pause(Duration.ofMillis(500))
               .click(subMenu)
               .perform();
    }

    public void dragAndDrop(WebElement source, WebElement target) {
        actions.dragAndDrop(source, target).perform();
    }

    public void scrollToElement(WebElement element) {
        js = (JavascriptExecutor) driver;
        js.executeScript("arguments[0].scrollIntoView(true);", element);
    }

    public void clickWithJS(WebElement element) {
        js.executeScript("arguments[0].click();", element);
    }

    public void highlightElement(WebElement element) {
        js.executeScript("arguments[0].style.border='3px solid red'", element);
    }

    public void captureScreenshot(String testName) throws Exception {
        TakesScreenshot ts = (TakesScreenshot) driver;
        File source = ts.getScreenshotAs(OutputType.FILE);
        FileUtils.copyFile(source, new File("screenshots/" + testName + ".png"));
    }
}
```

---

### Day 24 — Handling Alerts, Frames, Windows

**Example:**
```java
public class BrowserHandling {
    WebDriver driver;

    public void handleAlert() {
        Alert alert = new WebDriverWait(driver, Duration.ofSeconds(10))
            .until(ExpectedConditions.alertIsPresent());
        System.out.println("Alert text: " + alert.getText());
        alert.accept();
        // alert.dismiss();
        // alert.sendKeys("text");
    }

    public void workWithFrame() {
        driver.switchTo().frame(0);
        driver.switchTo().frame("frameName");
        WebElement frame = driver.findElement(By.id("myFrame"));
        driver.switchTo().frame(frame);

        driver.findElement(By.id("input")).sendKeys("text");
        driver.switchTo().defaultContent();
    }

    public void handleMultipleWindows() {
        String parentWindow = driver.getWindowHandle();
        Set<String> allWindows = driver.getWindowHandles();

        for (String window : allWindows) {
            if (!window.equals(parentWindow)) {
                driver.switchTo().window(window);
                System.out.println("Child window title: " + driver.getTitle());
                driver.close();
            }
        }
        driver.switchTo().window(parentWindow);
    }
}
```

---

### Day 25 — Dropdown, Checkbox, Radio Button, Tables

**Example:**
```java
import org.openqa.selenium.support.ui.Select;

public class FormElements {
    WebDriver driver;

    public void handleDropdown() {
        Select dropdown = new Select(driver.findElement(By.id("country")));
        dropdown.selectByVisibleText("India");
        dropdown.selectByValue("IN");
        dropdown.selectByIndex(2);

        List<WebElement> options = dropdown.getOptions();
        options.forEach(opt -> System.out.println(opt.getText()));
    }

    public String getTableCellValue(int row, int col) {
        String xpath = "//table[@id='dataTable']//tr[" + row + "]/td[" + col + "]";
        return driver.findElement(By.xpath(xpath)).getText();
    }

    public int getTableRowCount() {
        return driver.findElements(By.xpath("//table[@id='dataTable']//tr")).size();
    }

    public void checkIfNotChecked(WebElement checkbox) {
        if (!checkbox.isSelected()) {
            checkbox.click();
        }
    }
}
```

---

### Day 26 — ExtentReports (Professional Reporting)

**Example:**
```java
import com.aventstack.extentreports.*;
import com.aventstack.extentreports.reporter.*;

// pom.xml: com.aventstack:extentreports:5.1.1
public class ExtentReportManager {
    private static ExtentReports extent;
    private static ThreadLocal<ExtentTest> test = new ThreadLocal<>();

    public static ExtentReports createInstance() {
        ExtentSparkReporter spark = new ExtentSparkReporter("reports/ExtentReport.html");
        spark.config().setDocumentTitle("Automation Report");
        spark.config().setReportName("Regression Suite");

        extent = new ExtentReports();
        extent.attachReporter(spark);
        extent.setSystemInfo("Tester", "Your Name");
        extent.setSystemInfo("Environment", "QA");
        return extent;
    }

    public static ExtentTest getTest() { return test.get(); }
    public static void setTest(ExtentTest extentTest) { test.set(extentTest); }
}

public class TestListener implements ITestListener {
    @Override
    public void onTestStart(ITestResult result) {
        ExtentTest extentTest = ExtentReportManager.createInstance()
            .createTest(result.getMethod().getMethodName());
        ExtentReportManager.setTest(extentTest);
    }

    @Override
    public void onTestSuccess(ITestResult result) {
        ExtentReportManager.getTest().log(Status.PASS, "Test Passed");
    }

    @Override
    public void onTestFailure(ITestResult result) {
        ExtentReportManager.getTest().log(Status.FAIL, result.getThrowable());
    }
}
```

---

### Day 27 — Allure Reports (Industry Preferred)

**pom.xml additions:**
```xml
<dependency>
    <groupId>io.qameta.allure</groupId>
    <artifactId>allure-testng</artifactId>
    <version>2.25.0</version>
</dependency>
```

**Example:**
```java
import io.qameta.allure.*;

@Epic("Authentication Module")
@Feature("Login Feature")
public class LoginTest {

    @Test
    @Story("Valid User Login")
    @Severity(SeverityLevel.CRITICAL)
    @Description("Verify that valid user can login successfully")
    public void validLoginTest() {
        // test code
    }

    @Attachment(value = "Screenshot", type = "image/png")
    public byte[] captureScreen() {
        return ((TakesScreenshot) driver).getScreenshotAs(OutputType.BYTES);
    }

    @Step("Enter username: {username}")
    public void enterUsername(String username) {
        driver.findElement(By.id("user-name")).sendKeys(username);
    }
}
```

**Generate report:**
```bash
mvn test
allure serve target/allure-results
```

---

### Day 28 — Cucumber BDD Framework

**Feature file (login.feature):**
```gherkin
Feature: Login Functionality

  Background:
    Given user is on the login page

  @smoke
  Scenario: Valid login with correct credentials
    When user enters username "standard_user"
    And user enters password "secret_sauce"
    And user clicks the login button
    Then user should be redirected to dashboard
    And page title should be "Swag Labs"

  @regression
  Scenario Outline: Login with multiple users
    When user enters username "<username>"
    And user enters password "<password>"
    And user clicks the login button
    Then the result should be "<result>"

    Examples:
      | username        | password     | result  |
      | standard_user   | secret_sauce | success |
      | locked_out_user | secret_sauce | failure |
      | wrong_user      | wrong_pass   | failure |
```

**StepDefinitions.java:**
```java
import io.cucumber.java.en.*;
import static org.testng.Assert.*;

public class LoginSteps {
    WebDriver driver = Hooks.driver;
    LoginPage loginPage;

    @Given("user is on the login page")
    public void userIsOnLoginPage() {
        loginPage = new LoginPage(driver);
        driver.get("https://www.saucedemo.com");
    }

    @When("user enters username {string}")
    public void userEntersUsername(String username) {
        loginPage.enterUsername(username);
    }

    @When("user enters password {string}")
    public void userEntersPassword(String password) {
        loginPage.enterPassword(password);
    }

    @When("user clicks the login button")
    public void userClicksLoginButton() {
        loginPage.clickLogin();
    }

    @Then("user should be redirected to dashboard")
    public void userShouldBeRedirectedToDashboard() {
        assertTrue(driver.getCurrentUrl().contains("inventory"));
    }
}
```

---

### Day 29 — Parallel Execution + Cross-Browser Testing

**testng.xml for parallel:**
```xml
<suite name="Parallel Suite" parallel="tests" thread-count="3">
    <test name="Chrome Tests">
        <parameter name="browser" value="chrome"/>
        <classes><class name="tests.LoginTest"/></classes>
    </test>
    <test name="Firefox Tests">
        <parameter name="browser" value="firefox"/>
        <classes><class name="tests.LoginTest"/></classes>
    </test>
    <test name="Edge Tests">
        <parameter name="browser" value="edge"/>
        <classes><class name="tests.LoginTest"/></classes>
    </test>
</suite>
```

**ThreadSafe DriverFactory:**
```java
public class DriverFactory {
    private static ThreadLocal<WebDriver> driver = new ThreadLocal<>();

    public static WebDriver getDriver() { return driver.get(); }

    public static void initDriver(String browser) {
        WebDriver webDriver;
        switch (browser.toLowerCase()) {
            case "chrome":
                webDriver = new ChromeDriver();
                break;
            case "firefox":
                webDriver = new FirefoxDriver();
                break;
            default:
                throw new IllegalArgumentException("Browser not supported: " + browser);
        }
        webDriver.manage().window().maximize();
        driver.set(webDriver);
    }

    public static void quitDriver() {
        if (driver.get() != null) {
            driver.get().quit();
            driver.remove();
        }
    }
}
```

---

### Day 30 — Selenium Grid + Docker

**Docker Compose for Selenium Grid:**
```yaml
version: '3'
services:
  selenium-hub:
    image: selenium/hub:4.18.1
    ports:
      - "4442:4442"
      - "4443:4443"
      - "4444:4444"

  chrome-node:
    image: selenium/node-chrome:4.18.1
    depends_on: [selenium-hub]
    environment:
      - SE_EVENT_BUS_HOST=selenium-hub
    volumes:
      - /dev/shm:/dev/shm

  firefox-node:
    image: selenium/node-firefox:4.18.1
    depends_on: [selenium-hub]
    environment:
      - SE_EVENT_BUS_HOST=selenium-hub
```

**Connect to Grid:**
```java
URL gridUrl = new URL("http://localhost:4444");
ChromeOptions options = new ChromeOptions();
WebDriver driver = new RemoteWebDriver(gridUrl, options);
```

---

### Days 31-35 — Build Complete POM Framework

Build a full framework with:
- DriverFactory (ThreadLocal)
- BaseTest, BasePage
- ConfigReader
- ExcelDataReader
- ScreenshotUtil
- AllureReport + ExtentReport
- 20+ test cases on saucedemo.com
- testng.xml with parallel execution

**Practice site:** https://www.saucedemo.com

---

## PHASE 3: API Testing with RestAssured (Days 36-49)

### Day 36 — API Basics + REST Concepts
**Topics:** HTTP methods, status codes, request/response

```
GET    - Read data          → 200 OK
POST   - Create data        → 201 Created
PUT    - Update (full)      → 200 OK
PATCH  - Update (partial)   → 200 OK
DELETE - Delete data        → 204 No Content

Status codes:
2xx - Success  | 200, 201, 204
3xx - Redirect | 301, 302
4xx - Client   | 400, 401, 403, 404, 422
5xx - Server   | 500, 502, 503
```

**Tools:** Postman (practice first), then RestAssured

---

### Day 37 — RestAssured Setup + First Test

**pom.xml:**
```xml
<dependency>
    <groupId>io.rest-assured</groupId>
    <artifactId>rest-assured</artifactId>
    <version>5.4.0</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>io.rest-assured</groupId>
    <artifactId>json-path</artifactId>
    <version>5.4.0</version>
</dependency>
```

**First RestAssured test:**
```java
import io.restassured.RestAssured;
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

public class FirstAPITest {

    @BeforeClass
    public void setup() {
        RestAssured.baseURI = "https://reqres.in/api";
    }

    @Test
    public void getUsers_ShouldReturn200() {
        given()
            .header("Content-Type", "application/json")
        .when()
            .get("/users?page=2")
        .then()
            .statusCode(200)
            .body("page", equalTo(2))
            .body("data", hasSize(6))
            .body("data[0].id", equalTo(7))
            .body("data[0].email", containsString("@reqres.in"));
    }
}
```

**Practice API:** https://reqres.in (free, no auth needed)

---

### Day 38 — POST, PUT, DELETE Requests

**Example:**
```java
import io.restassured.response.Response;
import org.json.JSONObject;

public class CRUDTests {

    @Test
    public void createUser_ShouldReturn201() {
        JSONObject requestBody = new JSONObject();
        requestBody.put("name", "SDET Pro");
        requestBody.put("job", "Automation Lead");

        Response response =
        given()
            .contentType(ContentType.JSON)
            .body(requestBody.toString())
        .when()
            .post("/users")
        .then()
            .statusCode(201)
            .body("name", equalTo("SDET Pro"))
            .body("id", notNullValue())
            .extract().response();

        String userId = response.jsonPath().getString("id");
        System.out.println("Created User ID: " + userId);
    }

    @Test
    public void updateUser_ShouldReturn200() {
        JSONObject body = new JSONObject();
        body.put("name", "Updated Name");
        body.put("job", "Senior SDET");

        given()
            .contentType(ContentType.JSON)
            .body(body.toString())
        .when()
            .put("/users/2")
        .then()
            .statusCode(200)
            .body("name", equalTo("Updated Name"))
            .body("updatedAt", notNullValue());
    }

    @Test
    public void deleteUser_ShouldReturn204() {
        given()
        .when()
            .delete("/users/2")
        .then()
            .statusCode(204);
    }
}
```

---

### Day 39 — Authentication in APIs

**Example:**
```java
// Basic Auth
given()
    .auth().basic("username", "password")
.when()
    .get("/secure-endpoint")
.then()
    .statusCode(200);

// Bearer Token (JWT)
String token = getAuthToken();
given()
    .header("Authorization", "Bearer " + token)
.when()
    .get("/protected-resource")
.then()
    .statusCode(200);

// OAuth2
given()
    .auth().oauth2("access_token_here")
.when()
    .get("/api/resource");

// API Key
given()
    .header("X-API-Key", "your-api-key")
.when()
    .get("/api/data");

// Login and extract token
public String getAuthToken() {
    return given()
        .contentType(ContentType.JSON)
        .body("{\"email\":\"eve.holt@reqres.in\",\"password\":\"cityslicka\"}")
    .when()
        .post("/login")
    .then()
        .statusCode(200)
        .extract()
        .jsonPath()
        .getString("token");
}
```

---

### Day 40 — JSON Schema Validation

**Example:**
```java
// Add dependency: io.rest-assured:json-schema-validator:5.4.0
import static io.restassured.module.jsv.JsonSchemaValidator.*;

// user-schema.json (in resources folder)
{
    "$schema": "http://json-schema.org/draft-07/schema",
    "type": "object",
    "properties": {
        "id": {"type": "integer"},
        "name": {"type": "string"},
        "email": {"type": "string", "format": "email"},
        "createdAt": {"type": "string"}
    },
    "required": ["id", "name", "email"]
}

@Test
public void validateUserSchema() {
    given()
    .when()
        .get("/users/2")
    .then()
        .statusCode(200)
        .body(matchesJsonSchemaInClasspath("schemas/user-schema.json"));
}
```

---

### Day 41 — API Framework with POJO + RestAssured

**POJO classes:**
```java
// User.java
public class User {
    private int id;
    private String email;
    private String firstName;
    private String lastName;
    private String avatar;
    // getters and setters
}

// Test using POJO deserialization
@Test
public void getUserWithPOJO() {
    User user = given()
    .when()
        .get("/users/2")
    .then()
        .statusCode(200)
        .extract()
        .jsonPath()
        .getObject("data", User.class);

    Assert.assertEquals(user.getId(), 2);
    Assert.assertEquals(user.getEmail(), "janet.weaver@reqres.in");
}
```

---

### Days 42-49 — API Framework + Advanced Topics

- Request/Response Specification (reusable setup)
- Logging and filtering
- File upload/download via API
- GraphQL API testing
- Database validation after API calls
- End-to-end API test suite (20+ test cases)
- Integrate API tests with TestNG + Allure

**Advanced API Framework structure:**
```
src/
 └── test/
      ├── java/
      │    ├── api/
      │    │    ├── endpoints/        (UserEndpoints, OrderEndpoints)
      │    │    ├── models/           (User, Order POJO)
      │    │    ├── utils/            (ApiHelper, AuthManager)
      │    │    └── tests/            (UserTests, OrderTests)
      └── resources/
           ├── schemas/               (JSON schemas)
           └── testdata/              (JSON test data)
```

---

## PHASE 4: CI/CD + DevOps (Days 50-63)

### Day 50-52 — Jenkins Pipeline

**Jenkinsfile:**
```groovy
pipeline {
    agent any

    parameters {
        choice(name: 'BROWSER', choices: ['chrome', 'firefox'], description: 'Browser')
        choice(name: 'ENV', choices: ['qa', 'staging'], description: 'Environment')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your/repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('UI Tests') {
            steps {
                sh "mvn test -Dbrowser=${params.BROWSER} -Denv=${params.ENV} -Dgroups=smoke"
            }
        }

        stage('API Tests') {
            steps {
                sh 'mvn test -Dtest=*APITest*'
            }
        }

        stage('Reports') {
            steps {
                allure([
                    includeProperties: false,
                    results: [[path: 'target/allure-results']]
                ])
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
            emailext(
                subject: "Test Results: ${currentBuild.result}",
                body: "Tests completed. Check report at ${BUILD_URL}",
                to: "team@company.com"
            )
        }
    }
}
```

---

### Day 53-55 — GitHub Actions

**.github/workflows/automation.yml:**
```yaml
name: Automation Tests

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]
  schedule:
    - cron: '0 9 * * *'   # Run daily at 9 AM

jobs:
  ui-tests:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Cache Maven packages
        uses: actions/cache@v3
        with:
          path: ~/.m2
          key: ${{ runner.os }}-m2-${{ hashFiles('**/pom.xml') }}

      - name: Run Tests
        run: mvn test -Dbrowser=chrome -Dheadless=true

      - name: Generate Allure Report
        uses: simple-elf/allure-report-action@master
        with:
          allure_results: target/allure-results

      - name: Upload Test Results
        uses: actions/upload-artifact@v3
        if: always()
        with:
          name: test-results
          path: target/surefire-reports/
```

---

### Day 56-58 — Docker for Test Automation

**Dockerfile:**
```dockerfile
FROM maven:3.9.5-eclipse-temurin-17

WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src

CMD ["mvn", "test", "-Dheadless=true"]
```

**docker-compose.yml (full setup):**
```yaml
version: '3'
services:
  selenium-hub:
    image: selenium/hub:4.18.1
    ports:
      - "4444:4444"

  chrome:
    image: selenium/node-chrome:4.18.1
    depends_on: [selenium-hub]
    environment:
      - SE_EVENT_BUS_HOST=selenium-hub

  test-runner:
    build: .
    depends_on: [chrome]
    environment:
      - GRID_URL=http://selenium-hub:4444
      - BROWSER=chrome
    volumes:
      - ./reports:/app/reports
```

```bash
docker-compose up --scale chrome=3  # 3 parallel Chrome nodes
```

---

### Day 59-61 — Database Testing

**Example:**
```java
// pom.xml: mysql:mysql-connector-java:8.0.33
import java.sql.*;

public class DatabaseHelper {
    private Connection connection;

    public DatabaseHelper(String host, String dbName, String user, String pass) throws Exception {
        String url = "jdbc:mysql://" + host + ":3306/" + dbName;
        connection = DriverManager.getConnection(url, user, pass);
    }

    public ResultSet executeQuery(String sql) throws Exception {
        Statement stmt = connection.createStatement();
        return stmt.executeQuery(sql);
    }

    @Test
    public void verifyUserCreatedInDB() throws Exception {
        given().contentType(ContentType.JSON)
               .body("{\"name\":\"John\",\"email\":\"john@test.com\"}")
               .post("/users");

        ResultSet rs = dbHelper.executeQuery(
            "SELECT * FROM users WHERE email='john@test.com'"
        );
        Assert.assertTrue(rs.next(), "User not found in database!");
        Assert.assertEquals(rs.getString("name"), "John");
    }
}
```

---

### Day 62-63 — BrowserStack / Cloud Testing

**Example:**
```java
public class BrowserStackTest {

    @Test
    public void testOnBrowserStack() throws Exception {
        MutableCapabilities caps = new MutableCapabilities();

        HashMap<String, Object> bsOptions = new HashMap<>();
        bsOptions.put("os", "Windows");
        bsOptions.put("osVersion", "10");
        bsOptions.put("browserVersion", "latest");
        bsOptions.put("projectName", "My Project");
        bsOptions.put("buildName", "Build 1.0");
        bsOptions.put("sessionName", "Login Test");

        caps.setCapability("browserName", "Chrome");
        caps.setCapability("bstack:options", bsOptions);

        WebDriver driver = new RemoteWebDriver(
            new URL("https://YOUR_USERNAME:YOUR_KEY@hub.browserstack.com/wd/hub"),
            caps
        );

        driver.get("https://www.saucedemo.com");
        // run tests...
        driver.quit();
    }
}
```

---

## PHASE 5: Advanced Topics (Days 64-77)

### Day 64-66 — Performance Testing with JMeter

**JMeter Test Plan (via GUI):**
```
Thread Group
 ├── Number of threads: 100
 ├── Ramp-up: 10 seconds
 └── Loop Count: 5

HTTP Request Sampler
 ├── Server: api.example.com
 ├── Path: /api/users
 └── Method: GET

Assertions:
 ├── Response Code: 200
 └── Response Time < 2000ms

Listeners:
 ├── Summary Report
 ├── View Results Tree
 └── Aggregate Report
```

**Run via Maven/CLI:**
```bash
mvn jmeter:jmeter -Djmeter.test=performance-test.jmx
jmeter -n -t test.jmx -l results.jtl -e -o reports/
```

---

### Day 67-69 — Mobile Testing with Appium

**Setup:**
```java
// pom.xml: io.appium:java-client:9.2.2
import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.android.options.UiAutomator2Options;

public class MobileTest {

    @BeforeClass
    public void setup() throws Exception {
        UiAutomator2Options options = new UiAutomator2Options();
        options.setPlatformName("Android");
        options.setPlatformVersion("13");
        options.setDeviceName("emulator-5554");
        options.setApp("/path/to/app.apk");
        options.setAutomationName("UiAutomator2");

        driver = new AndroidDriver(
            new URL("http://localhost:4723"), options
        );
    }

    @Test
    public void testLoginOnMobile() {
        driver.findElement(By.id("com.app:id/editTextEmail"))
              .sendKeys("test@example.com");

        driver.swipe(
            new Point(500, 1500),
            new Point(500, 500),
            Duration.ofMillis(500)
        );
    }
}
```

---

### Day 70-72 — Contract Testing with Pact

**Consumer test:**
```java
// pom.xml: au.com.dius.pact.consumer:junit5:4.6.7
import au.com.dius.pact.consumer.dsl.*;
import au.com.dius.pact.consumer.junit5.*;

@ExtendWith(PactConsumerTestExt.class)
public class UserServiceContractTest {

    @Pact(consumer = "UserService", provider = "UserAPI")
    public RequestResponsePact getUserPact(PactDslWithProvider builder) {
        return builder
            .given("User with ID 1 exists")
            .uponReceiving("Get user request")
            .path("/users/1")
            .method("GET")
            .willRespondWith()
            .status(200)
            .body(new PactDslJsonBody()
                .integerType("id", 1)
                .stringType("name", "John")
                .stringType("email", "john@test.com")
            )
            .toPact();
    }

    @Test
    @PactTestFor(pactMethod = "getUserPact")
    public void verifyUserContract(MockServer mockServer) {
        given()
            .baseUri(mockServer.getUrl())
        .when()
            .get("/users/1")
        .then()
            .statusCode(200)
            .body("name", notNullValue());
    }
}
```

---

### Day 73-75 — Microservices Testing Strategy

**Key concepts to master:**
```
1. Unit Tests          → JUnit 5 + Mockito
2. Integration Tests   → Spring Boot Test
3. Contract Tests      → Pact
4. Component Tests     → Testcontainers
5. E2E Tests           → Selenium + RestAssured
```

**Testcontainers (real DB in tests):**
```java
import org.testcontainers.containers.MySQLContainer;
import org.testcontainers.junit.jupiter.Container;

@Testcontainers
public class UserRepositoryTest {

    @Container
    static MySQLContainer<?> mysql = new MySQLContainer<>("mysql:8.0")
        .withDatabaseName("testdb")
        .withUsername("test")
        .withPassword("test");

    @Test
    public void canSaveAndRetrieveUser() {
        String jdbcUrl = mysql.getJdbcUrl();
        // run actual DB operations - no mocking!
    }
}
```

---

### Day 76-77 — Security Testing Basics (OWASP)

**Topics for SDET:**
- SQL Injection testing in automation
- XSS detection
- OWASP ZAP integration with Selenium
- Auth bypass testing

**Example:**
```java
@Test
public void testSQLInjectionProtection() {
    String maliciousInput = "' OR '1'='1";
    driver.findElement(By.id("username")).sendKeys(maliciousInput);
    driver.findElement(By.id("password")).sendKeys("anypassword");
    driver.findElement(By.id("login")).click();

    Assert.assertFalse(driver.getCurrentUrl().contains("dashboard"),
        "SQL Injection vulnerability found!");
    Assert.assertTrue(driver.findElement(By.id("error")).isDisplayed(),
        "Error message should appear");
}
```

---

## PHASE 6: Portfolio + Interview Prep (Days 78-90)

### Days 78-83 — Build Portfolio Projects

**Project 1: Complete UI Automation Framework**
```
✅ Selenium 4 + TestNG
✅ POM Pattern
✅ Excel Data-Driven
✅ Cross-browser parallel
✅ Allure + Extent Reports
✅ Jenkins pipeline
✅ Docker support
✅ 50+ test cases on real site
→ Host on GitHub with README
```

**Project 2: API Automation Framework**
```
✅ RestAssured + TestNG
✅ POJO-based
✅ JSON Schema validation
✅ Auth handling (Basic, JWT, OAuth)
✅ DB validation
✅ 30+ test cases on reqres.in + any public API
→ Host on GitHub
```

**Project 3: Hybrid Framework (UI + API + DB)**
```
✅ Full E2E flows
✅ CI/CD with GitHub Actions
✅ Docker Compose
✅ Allure Cloud reports
→ Best portfolio piece - demo this in interviews
```

---

### Days 84-90 — Interview Preparation

**Top Interview Questions by Category:**

#### Java
- What is the difference between `==` and `.equals()`?
- What is `ThreadLocal` and why use it in Selenium?
- Explain `volatile`, `synchronized` in parallel testing
- What is `abstract class` vs `interface`?

#### Selenium
- How do you handle dynamic web elements?
- What is `StaleElementReferenceException` and how to fix it?
- Difference between `findElement` vs `findElements`?
- How does Selenium Grid work?
- `Implicit` vs `Explicit` vs `Fluent` wait?

#### TestNG
- How do you run tests in parallel?
- What is `@DataProvider`?
- What is `ITestListener`?
- How does `@Factory` work?

#### API Testing
- How do you validate API response schema?
- How to handle token refresh in RestAssured?
- What is the difference between `PUT` and `PATCH`?

#### Framework/Design
- Explain Page Object Model
- What design patterns have you used in frameworks?
- How do you handle flaky tests?
- Explain your CI/CD pipeline

#### Behavioral (Salary negotiation keywords)
- "I built a framework from scratch that reduced regression time from 3 days to 4 hours"
- "I integrated our automation suite with Jenkins reducing manual intervention"
- "I mentored junior SDETs in Selenium and API testing"

---

## Learning Resources Summary

| Topic | Best Resource |
|-------|--------------|
| Core Java | Telusko YouTube + javatpoint.com |
| Selenium | Mukesh Otwani YouTube + selenium.dev docs |
| TestNG | testng.org + Software Testing Material |
| RestAssured | rest-assured.io + Bas Dijkstra blog |
| Cucumber BDD | cucumber.io official docs |
| JMeter | Apache JMeter docs + Blazemeter blog |
| Appium | appium.io + BrowserStack guides |
| Jenkins | jenkins.io official docs |
| Docker | docs.docker.com + TechWorld with Nana (YouTube) |
| Git | learngitbranching.js.org |
| GitHub Actions | docs.github.com/actions |
| Maven | maven.apache.org |
| Design Patterns | Refactoring.guru |
| Interview Prep | LeetCode (easy problems), InterviewBit |

---

## Practice Sites

| Site | Purpose |
|------|---------|
| https://www.saucedemo.com | Selenium UI automation |
| https://reqres.in | API testing |
| https://www.demoblaze.com | E-commerce UI automation |
| https://restful-booker.herokuapp.com | Full API CRUD practice |
| https://parabank.parasoft.com | Banking app automation |
| https://the-internet.herokuapp.com | All tricky Selenium scenarios |

---

## Salary Negotiation Strategy (24 → 40 LPA)

| Factor | Action |
|--------|--------|
| Skills Gap | Fill with Phase 1-5 above |
| Portfolio | 3 GitHub projects (Week 11-12) |
| Target Companies | Product companies: Flipkart, Swiggy, Meesho, CRED, PhonePe |
| Resume Keywords | "Framework Architect", "CI/CD Integration", "Cross-browser automation", "API test coverage" |
| Negotiation | Quote 42-45 LPA expectation, settle at 40 LPA |
| Timing | Apply in Week 10, interview in Week 12 |

---

## Daily Schedule (2-3 hrs/day)

```
6:00 AM - 7:00 AM  → Theory (read/watch)
7:00 AM - 8:30 AM  → Hands-on coding
Evening 9:00 PM    → Review + push to GitHub (30 min)
Weekend            → Build mini-project + revise week's topics
```

---

> **Key Advantage:** You have 15 years of testing experience — you understand what breaks, what to test,
> and business impact. Add the technical SDET skills above and you become exceptionally valuable.
> Most SDET candidates either know Java well but don't understand testing depth, or they test well
> but can't code — you will be in neither trap.
>
> Start today with Day 1. Push code to GitHub every single day — by Day 90 you will have a portfolio
> that justifies 40 LPA confidently.
