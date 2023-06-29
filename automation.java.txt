package prog;

import java.time.Duration;
import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.Select;

public class joes_pizza {

	public static void main(String[] args) throws InterruptedException {

		System.setProperty("webdriver.chrome.driver",
				"C:\\Users\\dell\\Desktop\\Avinash\\Automation\\Basicsamme\\drivers\\chromedriver.exe");
		WebDriver driver = new ChromeDriver();
		driver.manage().window().maximize();
		driver.get("http://3.89.33.220/login");

		WebElement username = driver.findElement(By.xpath("//input[@id=\"email\"][@placeholder=\"Email ID\"]"));
		username.click();
		username.sendKeys("john@restaurant.com");

		WebElement password = driver.findElement(By.id("password"));
		password.sendKeys("admin123");

		WebElement login = driver.findElement(By.xpath("//button"));
		login.click();
		WebElement Orders = driver.findElement(By.xpath("//div[@id=\"sidebar-menu\"]/ul/li[6]/a"));
		Orders.click();

		List<WebElement> tableLength = driver.findElements(
				By.xpath("//div[@id=\"orders-table_wrapper\"]//div[@id=\"orders-table_length\"]/label/select/option"));
		tableLength.size();
		System.out.println(tableLength.size());
		for (WebElement wb : tableLength) {
			String text = wb.getText();
			if (text.equalsIgnoreCase("All")) {
				wb.click();

			}
		}

		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(2));
		WebElement ordersTable = driver.findElement(By.id("orders-table"));
		List<WebElement> orderRows = ordersTable.findElements(By
				.xpath("//div[@id=\"orders-table_wrapper\"]//table//tbody//tr//td[9]/div//select//option[@selected]"));
		System.out.println(orderRows.size());
		int pendingCount = 0;
		int completedCount = 0;
		int inprogressCount = 0;
		int totalCount = orderRows.size(); // Total count of orders

		for (WebElement row : orderRows) {

			String status = row.getText();

			if (status.equals("Pending")) {

				pendingCount++;
			} else if (status.equalsIgnoreCase("Completed")) {
				completedCount++;
			} else if (status.equalsIgnoreCase("In progress")) {
				inprogressCount++;
				
			}
		}

		System.out.println("Total Count: " + totalCount);
		System.out.println("Pending Count: " + pendingCount);
		System.out.println("Completed Count: " + completedCount);
		System.out.println("In Progress Count: " + inprogressCount);

		driver.close();
	}

}
