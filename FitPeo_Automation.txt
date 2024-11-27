package Assignment;

import java.time.Duration;
import java.util.List;

import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.testng.Assert;
;

public class FitPeo {

	public static void main(String[] args) throws InterruptedException {
		// TODO Auto-generated method stub
		
		
		ChromeDriver driver = new ChromeDriver();
		
		driver.manage().window().maximize();
		
		driver.get("https://www.fitpeo.com/");
		 driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(20));

		//webElement to Navigate to Revenue Calculator page
		driver.findElement(By.xpath("//div[contains(text(),'Revenue Calculator')]")).click();
		
	// webElement for scrolling the page 
		WebElement element = driver.findElement(By.xpath("//h4[contains(text(),'Medicare Eligible Patients')]"));
		
		// Scrolling down the page till the element is found
		JavascriptExecutor js = (JavascriptExecutor) driver;
        js.executeScript("arguments[0].scrollIntoView();", element);
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(20));
        
        //Code for sliding the slider
      WebElement slider = driver.findElement(By.xpath("//span[@class='MuiSlider-thumb MuiSlider-thumbSizeMedium MuiSlider-thumbColorPrimary MuiSlider-thumb MuiSlider-thumbSizeMedium MuiSlider-thumbColorPrimary css-1sfugkh']"));
  
        Actions action = new Actions(driver);
        action.dragAndDropBy(slider,94,0).perform();
        
        //driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(20));  
        Thread.sleep(5000);
      WebElement valueBox =   driver.findElement(By.xpath("//input[@id=':r0:']"));
     System.out.println(valueBox.getText());
      valueBox.clear();
      valueBox.sendKeys("560");
        
         
      List<WebElement> checkboxes= driver.findElements(By.xpath("//input[@type='checkbox']"));
      
    
      //code for selecting the CPT codes
      
      for (int i = 0;i<3;i++) {
    	  
    	  if(!checkboxes.get(i).isSelected()) {
    		  checkboxes.get(i).click();
    		  
    	  }
      }
      
      
		
      if(!checkboxes.get(7).isSelected()) {
		  checkboxes.get(7).click();
		  
	  }
      
      //code for Validating Total Recurring Reimbursement
      WebElement totalrevenue= driver.findElement(By.xpath("//p[@class='MuiTypography-root MuiTypography-body2 inter css-1xroguk'][contains(text(),'Total Recurring Reimbursement for all Patients Per')]"));
      System.out.println(totalrevenue.getText());
      
      String actualText = totalrevenue.getText();
      
      int totalReimbursement = 111105;
      
      // Print the result
      String expectedText="Total Recurring Reimbursement for all Patients Per Month:\n$" + totalReimbursement;
      
      Assert.assertEquals(actualText,expectedText,"Heading text does not match!") ;
      
      // for closing a=the browser
      driver.quit();
	}
	

}
