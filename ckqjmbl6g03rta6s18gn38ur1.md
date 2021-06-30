## Selenium Web Automation: Some approaches, Tips and Tricks.

Recently I got encouraged to write something on UI Automation stability or say cheat-sheat kind of stuff. So here I am, sharing some of the hacks I have learned from experience while doing UI browser automation. 

### 1. Never assign browser instance directly: 

Do it while creating small dedicated functions instead. 
For example:

Have 1 function ONLY for instance:

``` 
private WebDriver driver;
public String browserName = "Chrome";

/*This function will Initiate the type of browser defined in constants file
	 * and will create the browser instance accordingly
	 * */
	public  WebDriver getDriver()
	{
		if(browserName.equalsIgnoreCase("chrome")){
			driver = initChromeDriver();
			//driver = initChromeDriverIncognito();
		}else if(browserName.equalsIgnoreCase("Edge")){
			driver = initEdgeDriver();
		}else if(browserName.equalsIgnoreCase("firefox")){
			driver = initFirefoxDriver();
		}else if(browserName.equalsIgnoreCase("IE")){
			driver = initIEDriver();
		}

		return driver;
	}
 ``` 
and this function will return driver based on your const value Say chrome, so your chrome function will be like: 


```
/*
	 * This function will create the Chrome browser instance 
	 * In Incognito mode  and return the driver
	 * */
	public WebDriver initChromeDriverIncognito()
	{	
		System.setProperty("webdriver.chrome.driver", "Lib\\chromedriver.exe");
		DesiredCapabilities capabilities = DesiredCapabilities.chrome();
		ChromeOptions options = new ChromeOptions();
		options.addArguments("incognito");
		options.addArguments("disable-extensions");
		options.addArguments("--start-maximized");
		capabilities.setCapability(ChromeOptions.CAPABILITY, options);
		driver = new ChromeDriver(capabilities);
		// Issue in using this with incognito window  
		//driver.manage().window().maximize();  	
		return driver;

	}

``` 
This way you will always be in control of how many browsers you want to run your tests on and adding/ removing any behaviour whenever you want. 

*Please note, with selenium 4, DesiredCapabilities objects are now replaced with Options, and we need to create an Options object to use the Driver class* so the updated code will be something like 

```
ChromeOptions options = new ChromeOptions();
  options.setAcceptInsecureCerts(true);
  driver.get("https://www.yourURL.com");
``` 
But the basic funda remains the same. 

### 2. Use wrapper functions to wait for an element

In modern-day websites, many contents are dynamic and you might need to create some wait mechanism for your framework which can be clubbed and work together. To handle this scenario, create your own wait functions and call those functions in your action keywords functions, for example:

```
/* 
	 * findElementWait method specification :-
	 * This method will wait for an element to be visible, it requires following parameters
	 * @elementIdentifier: Type of element require to wait
	 * @elementValue: Value of that element
	 */

	public WebElement findElementWait(WebDriver driver, String elementIdentifier, String elementValue)
	{

		int timer = 3;
		WebDriverWait wait = new WebDriverWait(driver, timer);	
		if(elementIdentifier.equalsIgnoreCase("xpath"))
			element = wait.until(ExpectedConditions.elementToBeClickable(By.xpath(elementValue)));
		else if(elementIdentifier.equalsIgnoreCase("id"))
			element = wait.until(ExpectedConditions.elementToBeClickable(By.id(elementValue)));
		else if(elementIdentifier.equalsIgnoreCase("className"))
			element = wait.until(ExpectedConditions.elementToBeClickable(By.className(elementValue)));
		else if(elementIdentifier.equalsIgnoreCase("linkText"))
			element = wait.until(ExpectedConditions.elementToBeClickable(By.linkText(elementValue)));

		return element;
	}

	/* 
	 * click method specification :-
	 * This method should be used to click on element, it requires
	 * @elementIdentifier: Type of element we require to wait
	 * @elementValue: Value of that element
	 */	
	public void click(WebDriver driver, String elementIdentifier,String elementValue){
		WebElement element=findElementWait(driver, elementIdentifier, elementValue);
		element.click();
	}

``` 


Observe, how the click function first will wait for an element by using a wrapper function and then only will perform any operation. This approach will be very helpful for having an inbuilt wait system throughout the framework and can be clubbed later with other wait functions you probably will create based on your application-specific spinners etc. 

### 3. Never use assertions/ halts/ exceptions in your page objects or keyword classes
Use it in your test cases instead.
I have done it and faced issues when the code base grows. This reduces reusability and causes execution interruptions in between which is later on harder to debug. More so, you end up creating more duplicate functions bifurcating the entire reusability principle you wanted to have in the first place. This applies to any automation you are doing be it API, mobile etc.

For example:
In your selenium keyword class, say you want to verify the element display, verify and only return boolean. avoid exception while checking an element exists.

```
	/* This function should be used to check if the element 
	 * is displayed on the Page
	 * @driver = driver object to perform selenium operations
	 * @elementIdentifier: Type of element we require to wait
	 * @elementValue: Value of that element
	 */	
	public boolean checkElementDisplay(WebDriver driver,String elementIdentifier,String elementValue){
		WebElement element = findElementWait(driver, elementIdentifier, elementValue);
		if (element.isDisplayed()) {
			return true;
			}else{
		return false;
		}
	}
``` 
do the same in the page object function where you will call this function. Do the final pass/fail assertion only in the case. will be cleaner and meaner and you will always be sure that nothing is breaking inside page object, keywords logic etc. 

### 4. Use Webdriver manager, instead of hardcoding driver binaries path

So, with developments in recent years, it's much easier to manage driver binaries now. Gone are the days where you were hardcoding driver paths inside the frameworks. these days WebDriverManager do the jobs for you.

**What does WebDriverManager do?**

WebDriverManager is a class that allows us to download and set the browser driver binaries without us, as developers, having to put them in automation scripts manually.


```
WebDriverManager.chromedriver().setup(); 
driver = new ChromeDriver();
``` 

> Here, "WebDriverManager.chromedriver().setup();" checks for the latest version of the binary in local, if not present download it and instantiate driver instance with chrome

we can do this for any browser instance:


```
WebDriverManager.firefoxdriver().setup();
 
WebDriverManager.iedriver().setup();
 
WebDriverManager.edgedriver().setup();
 
WebDriverManager.operadriver().setup();
 
WebDriverManager.phantomjs().setup();
``` 

### 5. Handle popup windows

A common challenge in selenium web automation is interacting with pop-up windows. These windows appear could be a Simple alert, Confirmation alert or Prompt alert. 
use the switch_to method to manage pop-ups.

```
alert = driver.switch_to.alert
alertText = alert.text
print ("The alert message is "+ alertText)
alert.accept()
``` 
You can get clever and create a wrapper function to reuse the stuff in the page object if you aren't sure when the popup will occur.

### 6. Capture inner HTML and operate
There might be a scenario where you want to examine any changes in the page since the page was first loaded by the web browser. In these cases, the innerHTML property can be used to capture the source code and then operate upon it. For example: 

```
driver.get("https://www.google.com")
elem = driver.find_element_by_xpath("//*")
source_code = elem.get_attribute("innerHTML")
 
filename = open('Google_page_source.html', 'w')
filename.write(source_code)
filename.close()
``` 
You can create a wrapper function and reuse the same code to fetch innerHTML and operate upon it based on your specific needs.

### 7. Use javascript executor to handle some pain

for example:

**Make selenium webDriver click a checkbox that Is not currently visible.**
```
((JavascriptExecutor)driver).executeScript("arguments[0].checked = true;", checkbox);
``` 

**Handle Alerts popup**
```
JavascriptExecutor js =(JavascriptExecutor)driver;
js.executeScript("alert('SW Test Academy!');");
driver.switchTo().alert().accept();
``` 

**Highlight an Element** 
Use it as a wrapper and it will be very cool.
```
WebElement secondArticle = driver.findElement(By.xpath("//div/article[2]"));
js.executeScript("arguments[0].style.border='3px dotted blue'", secondArticle);
``` 

**Hide and Show an Element**
```
//JS hide an element
js.executeScript("document.querySelector('div>article:nth-of-type(2)').style.display='none'");
//JS show an element
js.executeScript("document.querySelector('div>article:nth-of-type(2)').style.display='block'");
``` 

**Use Async to wait**

```
//Declare JavascriptExecutor
JavascriptExecutor js =(JavascriptExecutor)driver;
//Call executeAsyncScript() method to wait for 4 seconds
js.executeAsyncScript("window.setTimeout(arguments[arguments.length - 1], 4000);"); 
``` 
> here, “arguments[arguments.lenght-1];” is a callback function to signal that async execution has finished. We have to call from JavaScript, to tell Webdriver, that our Asynchronous execution has finished. Make sure you set the script timeout before you call it.

**Use JS to wait for ajax calls to complete, instead of using thread.sleep**

I hate thread.sleep(). it's unreliable, hold CPU resources for specific times even if everything is done. Create JS-based wait functions instead, waiting for ajax or angular or jquery calls.

One smart way of doing it is to check if jquery is null or active :
```
public static ExpectedCondition<Boolean> jQueryAJAXCallsHaveCompleted() {
    return new ExpectedCondition<Boolean>() {

        @Override
        public Boolean apply(WebDriver driver) {
            return (Boolean) ((JavascriptExecutor) driver).executeScript("return (window.jQuery != null) && (jQuery.active === 0);");
        }
    };
  }
``` 

> Please note, that there is no universal approach for the above. You can check this good article to expand your understanding: https://www.swtestacademy.com/selenium-wait-javascript-angular-ajax/

refer to my [GitHub Repo](%[https://github.com/Ishan-Kumar/BaseFramework_Repo/tree/master/BaseFramework/src/com]) for some of the approaches I implemented some time back.  

**And most important practice above all? ** last but not least, understand your product:  There is no concrete/ magic framework architecture/ tool that will work in all applications. Different project(business requirements ) requires different architecture and should be directly in line with your use case. Spend some time to understand the user stories and use cases. Decide your setup and tech stack based on your research and identify what you want to achieve then jump into code.

Now, of course, there are much more things to share and I am sure, all of you have developed something suited for your purpose. If you have any such thing which can benefit others, please share It in the comments for us all :). 

