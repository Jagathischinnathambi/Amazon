package testNG;

import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;

import java.util.Iterator;
import java.util.Set;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.Dimension;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.Select;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.Assert;
import org.testng.annotations.AfterTest;

public class NewTest {
	public static WebDriver driver;
	public static JavascriptExecutor js;
  @Test
  public void f() throws Throwable {
	  
//	  Getting the URL of the Application using the WebDriver  
	  driver.get("https:\\www.amazon.in");
//	  Maximize the WebApplication window using webdriver
	  driver.manage().window().maximize();
	  driver.manage().timeouts().implicitlyWait(25, TimeUnit.SECONDS);
//	Getting the Current application Url
	  String base = driver.getCurrentUrl();
	  System.out.println(base);
//	Actual url of the Application
	  String actual = "https://www.amazon.in/";
	  System.out.println(actual);
//	checking the url of the application is matched by the current window 
	  if(base.equals(actual))
	  {
		  System.out.println("The url is Matched by the actual to base");
	  }
	  else
	  {
		  System.out.println("the url is doesn't match the actual url");
	  }
//	Intiating the Action class for mouse hover functions
	  Actions q = new Actions(driver);
	  WebElement sign =driver.findElement(By.id("nav-link-yourAccount"));
	  q.click(sign).build().perform();
	  driver.manage().timeouts().pageLoadTimeout(25, TimeUnit.SECONDS);
//	  Sending the username of the Application to the application
	  WebElement username = driver.findElement(By.xpath("//*[@name='email']"));
	  username.sendKeys("username");
	  driver.manage().timeouts().implicitlyWait(15, TimeUnit.SECONDS);
//	  Clicking the continue button using WebElement
	  WebElement con_button = driver.findElement(By.xpath("//*[@id='continue']"));
	  con_button.click();
	  driver.manage().timeouts().implicitlyWait(15, TimeUnit.SECONDS);
//	  Sending the Password of the Application to the application
	  WebElement pass =driver.findElement(By.xpath("//*[@id='ap_password']"));
	  pass.sendKeys("password");
//	  Clicking the Application Login button Using WebElement
	  WebElement Log_button = driver.findElement(By.xpath("//*[@id='signInSubmit']"));
	  Log_button.click();
	  driver.manage().timeouts().implicitlyWait(25, TimeUnit.SECONDS);
	  WebElement drop =driver.findElement(By.xpath("//*[@id='searchDropdownBox']"));
//    Clicking the application Dropdown of the SearchBox of the Amazon
	  Select s = new Select(drop);
	  s.selectByValue("search-alias=stripbooks");
//	  Sending the searchbox data using sendkeys
	  WebElement search = driver.findElement(By.xpath("//*[@id='twotabsearchtextbox']"));
	  search.sendKeys("Data catalougue");
	  driver.manage().timeouts().implicitlyWait(15, TimeUnit.SECONDS);
//	  Clicking the Application Searchbox of the Application
	  WebElement search_click = driver.findElement(By.xpath("//input[@class='nav-input']"));
	  driver.manage().timeouts().implicitlyWait(15, TimeUnit.SECONDS);
	  q.click(search_click).build().perform();  
//	  Getting the link of the Application after the search result
	  driver.manage().timeouts().implicitlyWait(25, TimeUnit.SECONDS);
      String sear_res = driver.getCurrentUrl();
	  System.out.println(sear_res); 
	  String nwin =driver.getWindowHandle();
	  System.out.println(nwin);
//	  Click the result of the applications first link
	  Thread.sleep(3000);
	  js.executeScript("window.scrollBy(0,800)");
	  driver.manage().timeouts().implicitlyWait(25, TimeUnit.SECONDS);
	  WebElement content_cli =driver.findElement(By.linkText("Library Catalogue:: Computerization & OPAC Services"));
	  content_cli.click();
//	  Switching the searchresultWindow
	  driver.switchTo().window(nwin);
//	  Switching between the Windows
	  Set<String> wres = driver.getWindowHandles();
	  Iterator<String> wman = wres.iterator();
	  while(wman.hasNext())
	  {
		  driver.switchTo().window(wman.next());
	  }
//	  Getting the Application Title
	  WebElement g_BookTitle =driver.findElement(By.xpath("//*[@id='productTitle']"));
	  String title = g_BookTitle.getText();
	  System.out.println(title);
//	  Getting the Product discription of the application
	  WebElement discrip = driver.findElement(By.xpath("//div[@id='productDescription']"));
	  System.out.println("Display the Product discription of the Application");
	  System.out.println( discrip.getText());
//	  Validating the Application Imagesize 
	  WebElement image = driver.findElement(By.xpath("//*[@id='imgBlkFront']"));
	  int height = image.getSize().height;
	  System.out.println(height);
	  int eheight =346;
	  int width =image.getSize().width;
	  System.out.println(width);
	  int ewidth   = 225;
//	  Geting the imagesize from the Application
	  Dimension isize = image.getSize();
	  System.out.println(isize);
//	  Validating the im of the Application Based on Dimensions
	  try {
		Assert.assertEquals(eheight, height);
		System.out.println("The value of the height is Equal");
	} catch (Exception e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
//	  Getiing the image width of the Application
	  try {
		Assert.assertEquals(ewidth, width);
		System.out.println("The Width is equal is Expected");
	} catch (Exception e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
//	 Using JavaScriptExecutor in the Script
	  
	  System.out.println("Lets Execute the Application javascript");
	  Thread.sleep(2000);
      js.executeScript("window.scrollBy(0,800)");
	
      
      
      
  }
  @BeforeTest
  public void beforeTest() {
//	 intiating the WebDriver Location from the local storage
	  System.setProperty("webdriver.chrome.driver", "C:\\Users\\venkat\\Desktop\\driverr\\chromedriver.exe");
//	 Creating the variable Object for the WebDriver interface
	  driver = new ChromeDriver(); 
//	  Creating a JavaScriptExecutor
	  js = (JavascriptExecutor)driver;
  }

  @AfterTest
  public void afterTest() {
	  
	  
 
  driver.close();
  
  
  
  }

}
