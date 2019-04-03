# ExlJS
ExlJS is a simple, but powerful tool for rapid and easy creation of **MAINTAINABLE** keyword and data driven test automation scripts.
ExlJS allows assembly of test cases in EXCEL by **copy/pasting** keywords in Excel sheet and feeding them with test data from another sheets in the same workbook.
Also this tool allows you to cut your test execution time **tenfold** by running your tests in parallel in multiple browsers at the same time.\
This tool is designed to enforce **test automation best practices**, so there is no "record and playback" functionality or other features that are not used by *REAL life test automation experts* as they make scripts unmaintainable.
- With this tool you can use Selenium **from JavaScript**, which is much easier than learning complex Java or C#.
- **No need** to install Node.js, Java, Selenium or other dependencies, the tool is self contained, just download this tool and you are all set.
- It supports test exection on *Selenium Grid nodes* and/or local machine.
- It supports Angular and JQuery ajax waits.
- Automatically takes screeenshots upon test failure for easy bug tracking.
- CI/CD integration.
- **!!!New!!!** *API testing* is available now.
- **!!!New!!!** Enterprise level reporting with drill down to step level, charts, screenshots and more
- **Save up to 70%** on your test automation development and maintenance time.

# Comparison to Selenium
1. ## Data-driving keywords<br/>
	**Selenium:**<br/>
	Either hardcoded values or have to write JDBC code to fetch it from data storage.
	```javascript
		//hardcoded values
		driver.findElement(By.css("#FirstName")).sendKeys("George");
		driver.findElement(By.css("#LastName")).sendKeys("Orwell");
		driver.findElement(By.css("#Address")).sendKeys("22 Main st");
	```		
	**ExlJS:**<br/>
	Data seemlessly driven to keyword from Excel sheet.
	[![Data driving compared](http://23.236.144.243/VisualTAFScreenshots/DataDrivingCompared2.png)](http://23.236.144.243/VisualTAFScreenshots/DataDrivingCompared2.png)



2. ## Waiting for Ajax, JQuery, Angualar, React page full load<br>
	**Selenium:**<br/>
	```javascript
		//OMG!
		FluentWait<By> fluentWait = new FluentWait<By>(By.tagName("TEXTAREA"));
		fluentWait.pollingEvery(100, TimeUnit.MILLISECONDS);
		fluentWait.withTimeout(1000, TimeUnit.MILLISECONDS);
		fluentWait.until(new Predicate<By>() {
		    public boolean apply(By by) {
			try {
			    return browser.findElement(by).isDisplayed();
			} catch (NoSuchElementException ex) {
			    return false;
			}
		    }
		});
	```		
	**ExlJS:**<br/>
	```javascript
		waitForAngularJQueryJS();
		//OR
		waitForObjectToBecomeVisible(UserRegistratioPage.textArea, 30);
	```
3. ## Filling form data<br/>
	**Selenium:**<br/>
	```javascript
		void fillUserRegistrationForm(String firstName, String lastName, String address)
		{
			if( firstName!= null )
				driver.findElement(By.css("#FirstName")).sendKeys(firstName);
			if( lastName!= null )
				driver.findElement(By.css("#LastName")).sendKeys(lastName);
			if( address!= null )
				driver.findElement(By.css("#Address")).sendKeys(address);
				
		}
	```		
	**ExlJS:**<br/>
	```javascript
		function fillUserRegistrationForm(params)
		{
			//auto searches for element and fills in text straight from Excel data row
			typeText(UserRegistratioPage.firstName, params.get("FirstName") );
			typeText(UserRegistratioPage.lastName, params.get("LastName") );
			typeText(UserRegistratioPage.address, params.get("Address") );
				
		}
	```


4. ## Checkpoints/element verification <br/>
	**Selenium:**</br>
	```javascript
		if( textToVerify!= null) 
			assertTrue( driver.findElement(By.id("CustomerId")).getText(), textToVerify) );
	```		
	**ExlJS:**<br/>
	```javascript
		assertObjectText( textToVerify, UserRegistratioPage.customerId );
	```		
	
5. ## Reporting <br>
	**Selenium:**<br/>
	Virtually None, except<br/>
	```javascript
		System.out.println("TC130 started"); 
		System.out.println("Clicked Submit button"); 
		...
		System.out.println("TC130 finished"); 
	```
		
	**ExlJS:**<br/>
	Comprehensive drill-down HTML report is generated **automatically** where you clearly see which test cases passed/failed WITH step-by-step action performed by each test case and screenshots.
	[![Reporting compared](http://23.236.144.243/VisualTAFScreenshots/ReportingCompared2.png)](http://23.236.144.243/VisualTAFScreenshots/ReportingCompared2.png)
	

5.  ## Parallel test execution <br>
	**Selenium:**</br>
	You would need to create new Threads by yourself in your Java code
	```javascript
		new Thread() {

		    @Override
		    public void run() {
			driver1 = new ChromeDriver();
		    }

		}.start();
		...
		new Thread() {

		    @Override
		    public void run() {
			driver2 = new ChromeDriver();
		    }

		}.start();
		
	```		
	**ExlJS:**<br/>
	Just select # of parallel threads you want and browser type from GUI when you start test execution, no need to code anything, test scripts are not dependant on browser type and threads.
	[![Parallel execution compared](http://23.236.144.243/VisualTAFScreenshots//threadandbrowsers2.png)](http://23.236.144.243/VisualTAFScreenshots/threadandbrowsers2.png)

6.  ## Deployment and learning curve <br>
	**Selenium:**</br>
	Need to download Java, Eclipse or Netbeans IDE, selenium jars, chromedriver.exe, compile tests to jar.<br/>
	Learning curve: need to learn Java classes, add strong types to every parameter, learn JDBC for data feed.
	
	**ExlJS:**<br/>
	Just unpack downloaded zip file, everything is included, and start running tests immediately, no compilation required!<br/>
	Learning curve: 1 day max to learn how to create Javascript functions and how to copy/paste rows in Excel :-), that's it.
<!---	
[![Main Screen](http://23.236.144.243/VisualTAFScreenshots/overallcomponents4.png)](http://23.236.144.243/VisualTAFScreenshots/overallcomponents4.png)
-->

# Installation
1. You would need Chrome Browser if you want to run included demo tests (https://www.google.com/chrome/).
2. Download ExcelTAF.zip file (http://23.236.144.243/VisualTAF/ExcelTAF.zip).
3. Unzip content of zip file to some folder.

# Running
1. In unzipped folder run ExcelTAF.exe
2. Right click on "Regression" in tool left panel and in popped up context menu click "Run selected test set" option to run built-in demo scripts
3. Then select number of parallel threads for execution, demo has 3 Excel files under Regression set, so if we specify 3 threads, then thread 1 will pick "Demo1.xlsx", thread 2 will pick "Demo2.xlsx", thread 3 will pick "Demo3.xlsx" for execution.
4. Test Execution will start with multiple browser windows (parallel execution) 
5. After test run completes you will see comprehensive test execution report

[![Main Screen](http://23.236.144.243/VisualTAFScreenshots/report.png)](http://23.236.144.243/VisualTAFScreenshots/report.png)

# Developing test cases
Doubleclick on "Demo1.xlsx" node to open this file in Excel and see it's structure.
It's quite simple, in each Excel file you need to have a sheet called "Instructions", this is where you assemble test cases. Instructions sheet has "TCName", "Keyword", "Input", "ExpectedResult", "Comment" columns. In "TCName" column you give name to your test case, that's how test case starts, then in the next lines in "Keywords" column you fill in instructions and attach data to them in "Input" column, then you end test case by typing "END" in "TCNAME" column. It's better pictured in diagram below

[![Main Screen](http://23.236.144.243/VisualTAFScreenshots/CreatingTestCasesInExcel.png)](http://23.236.144.243/VisualTAFScreenshots/CreatingTestCasesInExcel.png)

Now let's see how you add on-page objects to your scripts, in the left panel of the tool
expand **"Page Objects"** folder, it acts as an Object Repository, and doubleclick on any file there to open it and see its structure.
```javascript
//LoginPage.js
//Encapsulates page objects of Login page

var LoginPage = 
{
    email : selectorAndDescription("input#email", "Email address field"),
    password : selectorAndDescription("input#password", "Password field"),
    LoginButton : selectorAndDescription("button.btn-primary", "Login Button"),
    
    ErrorMessage : selectorAndDescription("span.help-block", "Error Message Area"),
}

LoginPage.url = "http://23.236.144.243/TicketsAUT/public/login";

//Then in your code you can  use on-page objects like typeText(LoginPage.email, "alaserm@yahoo.com")
// or click(LoginPage.LoginButton)
//Notice that all object recognition properties like "input#email" stored only  
//in one xxxxPage file, it's for easy script maintainability later when application changes

```
this is how you keep your object recognition properties in one place, so if developers change object in AUT (Application Under Test) then you can easily update it in just one place in your scripts, this is automation best practice for script maintainability.


So once you added on-page objects you can easily create keywords (keyword is a reusable function to perform common workflows in your application). Add keywords to **"Keywords"** folder in the left panel of the tool, keyword can be reused many times in Excel, you just feed it with different data rows for different test cases. here is an example of Login keyword for demo app that come with this tool.

```javascript
var Login = {};
Login.login = function(params) {
	
    navigate(LoginPage.url);
    waitForAngularJQueryJS();
    
    typeText(LoginPage.email, params.get("email") );
    typeText(LoginPage.password, params.get("password") );
    
    click(LoginPage.LoginButton);
}
```

You can also use plain Selenium code like driver.findElement(...).click() or driver.findElement(...).sendKeys("") to which you are used to. But there are also built-in convinience methods like typeText(), click() to make your life easier. You can see a list of convenience methods below:


```javascript
waitForAngularJQueryJS()
waitForObjectToBecomeVisible(obj, timeoutSecs )
navigate(to)

css(selector)
xpath(selector)
findObject(desc)

isObjectPresent(obj)
isObjectVisible(obj)
isObjectEnabled(obj)

clearText(obj)
typeText(obj, text)
select(obj, visibleText)
click(obj)

getText(obj)
getValue(obj)
getAttribute(obj, attrName)
getCssValue(obj, valName)

assertCurrentPageUrl(url)
assertObjectPresent(obj)
assertObjectVisible(obj)
assertObjectText( text, obj)
assertObjectRegExp( text, obj)
assertCssValue(valName, val, obj )

getAlertText()
acceptAlert()
dismissAlert()
 
```

Become an early distributor and earn millions with this hot new product ;)\
For any question contact **alaserm@yahoo.com**

