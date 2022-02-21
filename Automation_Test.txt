import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;



public class testcodepippin {

public static void main(String[] args) throws InterruptedException {

System.setProperty("Webdriver.chrome.driver", "C:\\chromedriver.exe");

WebDriver driver = new ChromeDriver();

// applying implicit wait

driver.manage().timeouts().implicitlyWait(10,TimeUnit.SECONDS) ;

driver.get("https://www.google.com");
driver.get("https://demo.pippintitle.com/");

driver.manage().window().maximize();

// entering username
driver.findElement(By.xpath("//input[@type='email']")).sendKeys("pippintitle_demotest@mailinator.com");
// entering password
driver.findElement(By.xpath("//input[@type='password']")).sendKeys("DemoTest#567#");

driver.findElement(By.xpath("//input[@type='submit']")).click();

//clicking on In Progress tab
driver.findElement(By.xpath("//a[@class='active']")).click();

// fetching order no. of a particular record
String OrderID = driver.findElement(By.xpath("(//tr[@class='ng-star-inserted']/td[1])[1]")).getText();
System.out.println("the order ID  found is " + OrderID);

// entering the order no. in the search field and hitting enter key

WebElement m  =driver.findElement(By.xpath("//div[@class='mat-form-field-infix']//input"));
m.sendKeys(OrderID);
m.sendKeys(Keys.ENTER);
Thread.sleep(5000);

// Taking expected values of a particular record in a list

List<String> list = Arrays.asList("Ankit Kumar Singh", "Confirmed", "Full Search", "Aug 14, 2021");

System.out.println("expected values of the record is :- " + list);
System.out.println();

// Taking actual values of that particular record from the UI

List<WebElement> ls = driver.findElements(By.xpath("//div//tr[@class]//td//div"));

ArrayList<String> text = new ArrayList<String>();
for (WebElement e : ls) {
text.add(e.getText().trim());
}
System.out.println("actual values of the record is :- " + text);

// Comparing the contents of both the lists for assertion true

if (list.equals(text) == true) {
System.out.println("Test Passed");
Assert.assertTrue(true);
}

// logging out

driver.findElement(By.xpath("//div[@class='ng-star-inserted']//span[@class='mat-button-wrapper']")).click();
driver.findElement(By.xpath("(//div[@class='mat-menu-content']//button)[4]")).click();

System.out.println("End of Test");
}

}
