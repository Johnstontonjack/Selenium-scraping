# Selenium-scraping


package WebScrapper; 
import java.io.*;
import java.util.*;
import java.util.regex.*;
 
import org.openqa.selenium.*;
import org.openqa.selenium.firefox.FirefoxDriver;
 
public class wait {
 
	public static void main(String[] args) throws IOException {
 
		WebDriver driver = new FirefoxDriver();
		driver.navigate().to("https://en.wikipedia.org/wiki/Trinity_Seven#Anime");
 
		List<WebElement> Airdate =  driver.findElements(By.xpath("//th[text()='Original air date']//following::td[contains(text(), '20')]"));
		List<WebElement> allTitlesza =  driver.findElements(By.xpath("//th[text()='Original air date']//following::td[contains(text(), '20')]"));
		int i=0;
		String fileText = "";
 
		for (WebElement date : Airdate){
			String date1 = ((WebElement) Airdate).getText();
			String Url = (String)((JavascriptExecutor)driver).executeScript("return arguments[0].innerHTML;", allTitlesza.get(i++));
			final Pattern pattern = Pattern.compile("title=(.+?)>");
			final Matcher matcher = pattern.matcher(Url);
			matcher.find();
			String title = matcher.group(1);
			fileText = fileText+Airdate+","+allTitlesza+"\n";
		}
 
		Writer writer = new BufferedWriter(new OutputStreamWriter(new FileOutputStream("books.csv"), "utf-8"));
		writer.write(fileText);
		writer.close();
 
		driver.close();
	}
}
