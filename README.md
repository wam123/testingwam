# testingwam
url class

namespace test123.test123
{
    public class xyzUrls
    {
        public const string StartPage = "https\\";
    }
}

Hooks Class

namespace xyztest.TestInitHelpers
{
    using OpenQA.Selenium;

    using TechTalk.SpecFlow;

    [Binding]
    public class Hooks
    {
        public static IWebDriver Driver { get; set; }

        [BeforeScenario]
        public static void SetupBrowser()
        {
            var webDriverFactory = new WebDriverFactory();
            var driver = webDriverFactory.GetWebDriver("ChromeDriver");
            Driver = driver;

            driver.Manage().Window.Maximize();
        }

        [AfterScenario]
        public static void AfterScenario()
        {
            //Driver.Quit();
        }

        [AfterTestRun]
        public static void AfterTestRun()
        {
            //Driver.Quit();
        }
    }
}

WebDriverFactoryClass


namespace xyztest.TestInitHelpers
{
    using System;

    using OpenQA.Selenium;
    using OpenQA.Selenium.Chrome;
    using OpenQA.Selenium.Firefox;
    using OpenQA.Selenium.IE;

    public class WebDriverFactory
    {
        public IWebDriver GetWebDriver(string BrowserName)
        {
            IWebDriver driver;
            switch (BrowserName)
            {
                case "FireFox":
                    driver = new FirefoxDriver();
                    break;
                case "InternetExplorer":
                    driver = new InternetExplorerDriver();
                    break;
                default:
                    driver = new ChromeDriver();
                    break;
            }

            driver.Manage().Timeouts().ImplicitWait = TimeSpan.FromSeconds(3);

            return driver;
        }
    }
}


Rate Feature file

Feature: Rate123
	As a MD
	I should be able to add new 123 rate
	
@123Rate
Scenario Outline: Add a new 123 rate
	Given A user with the role MD
	When User logs in as an Administrator 
	| Username | Password  |
	| test123  | p123      |
	And Clicks on the home tab
	And Click Add new 123 rate button
	And User enters <MinimumWage>, <HourlyRate>, <eveningrate> and <Date>
	When User clicks on the Add button
	Then new rate should be added 
	Examples: of 1233Rates 
	| MinimumWage | HourlyRate | eveningrate    | Date     |
	| 5.20        | 5.20       | 5.20           | 13122018 |
	| 8.20        | 4.20       | 6.20           | 13122018 |


Rate Steps 


namespace test123.zzzzTests.xoxoxo.StepsDefination
{
    using System;
    using System.Threading;

    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using OpenQA.Selenium;
    using TechTalk.SpecFlow;
    using TechTalk.SpecFlow.Assist;

    [Binding]
    public sealed class 123Rate 
    {
        private RatesPageElements ratesPageElements;
        private LoginPageElements loginPageElements;
  
        [Given(@"A user with the role MD")]
        [Scope(Tag = "New123Rate")]
        public void GivenAUserWithTheMD()
        {
            Hooks.Driver.Manage().Timeouts().ImplicitWait = TimeSpan.FromSeconds(3);
            Hooks.Driver.Navigate().GoToUrl(StaffMappingUrls.StartPage());
            this.ratesPageElements = new RatesPageElements(Hooks.Driver);
            this.loginPageElements = new LoginPageElements(Hooks.Driver);
        }

        [When(@"User logs in as an Administrator")]
        [Scope(Tag = "123Rate")]
        public void WhenUserLogsInAsAnAdministrator(Table table)
        {
            dynamic credentials = table.CreateDynamicInstance();

            this.loginPageElements.UsernameTxtBox.Clear();
            this.loginPageElements.UsernameTxtBox.SendKeys(credentials.Username);
            this.loginPageElements.PasswordTxtBox.Clear();
            this.loginPageElements.PasswordTxtBox.SendKeys(EncryptedTextHelper.Decrypt(credentials.Password));
            this.loginPageElements.SignInBtn.Click();
            this.loginPageElements.StaffMappingAdmin.Click();     
        }

        [When(@"Clicks on the settings tab")]
        [Scope(Tag = "123Rate")]
        public void WhenClicksOnTheSettingsTab()
        {
            this.ratesPageElements.AdminCog.Click();
        }

        [When(@"Click Add new baseline rate button")]
        public void WhenClickAddNewBaselineRateButton()
        {
            this.ratesPageElements.AddNewBaselineRate.Click();
        }

        [When(@"User enters (.*), (.*), (.*) and (.*)")]
        public void GivenIEnterAnd(string MinimumWage, string HourlyRate, string eveningRate, string Date)
        {
            this.ratesPageElements.MinWage.Clear();
            this.ratesPageElements.MinWage.SendKeys(MinimumWage);
            this.ratesPageElements.HourlyRate.Clear();
            this.ratesPageElements.HourlyRate.SendKeys(HourlyRate);
            this.ratesPageElements.eveiningRate.Clear();
            this.ratesPageElements.eveingRate.SendKeys(SleepNightRate);
          
        }

        [When(@"User clicks on the Add button")]
        public void WhenUserClicksOnTheAddButton()
        {
            this.ratesPageElements.RatesAddButton.Click();
        }

        [Then(@"new rate should be added")]
        public void ThenNewRateShouldBeAdded()
        {
            Assert.IsTrue(Hooks.Driver.FindElement(By.TagName("body")).Text.Contains("Base rate updated"));
        }
    }
}

Pageobjects class

namespace xxxxx.123Tests.123Payment.123PageObjects
{
    using OpenQA.Selenium;

    public class 123PageObjects
    {
        private readonly IWebDriver driver;

        public 123PageObjects(IWebDriver driver)
        {
            this.driver = driver;
        }

        public IWebElement ReferenceNo => this.driver.FindElement(By.XPath("//input[@data-automation='CReference']"));

        public IWebElement CeremonyDate => this.driver.FindElement(By.XPath("//input[@data-automation='CeremonyDate']"));

        public IWebElement FindCeremonyBtn => this.driver.FindElement(By.XPath("//button[@data-automation='SubmitButton']"));

        public IWebElement TermsCheckBox => this.driver.FindElement(By.XPath("//button[@data-automation='TermsAndConditionsConsent']"));
    }
}



Practice

namespace Practice3
{
    public class Program
    {
        //Write a code snippet to launch Chrome browser using Selenium WebDriver?
        IWebDriver driver = new ChromeDriver();

        public void Initialize()
        {
            //Navigate to url
            driver.Navigate().GoToUrl("www.test.com");

            //Maximise window
            driver.Manage().Window.Maximize();
            Console.WriteLine("Navigated to site");
        }
   
        public void Execute()

        {
            // Get current url 

            driver.Navigate().GoToUrl("www.test.com");
            driver.Url = "hhtps\\test.com";


            // Refresh page
           
            driver.Navigate().Refresh();
            driver.FindElement(By.Id("test")).SendKeys(Keys.F5);
          

            // Delete all cookies

            driver.Manage().Cookies.DeleteAllCookies();
           

            // Get Text from textbox

            string TypedText = driver.FindElement(By.Id("test")).GetAttribute("value");
            Console.WriteLine("value of the textbox is" + TypedText);

            // Select Drop Down Menu DDL / SelectByText/SelectByValue/SlectByIndex
            // (Selenium Select Class)

            var option = driver.FindElement(By.Id("test"));
            var SelectElement = new SelectElement(option);
            SelectElement.SelectByText("henry");


            Assert.IsTrue(driver.FindElement(By.Id("25-39kg")).Selected);

            // Hover and Click (Selenium Action Class)

            Actions action = new Actions(driver);
            IWebElement element1 = driver.FindElement(By.Id("test"));
            action.MoveToElement(element1).Build().Perform();
            driver.FindElement(By.Id("test")).Click();


            // Double Click (Selenium Action Class)

            Actions actions2 = new Actions(driver);
            IWebElement element2 = driver.FindElement(By.Id("test"));
            actions2.DoubleClick(element2).Build().Perform();

            Actions action55 = new Actions(driver);
            IWebElement element55 = driver.FindElement(By.Id("test"));
            action55.DoubleClick(element55).Build().Perform();

            // Right click (Selenium Action Class)

            Actions actions3 = new Actions(driver);
            IWebElement element3 = driver.FindElement(By.Id("test"));
            actions3.ContextClick(element3).Build().Perform();

            //Scroll Down Window 

            IJavaScriptExecutor js = (IJavaScriptExecutor)driver;
            js.ExecuteScript("Scroll (0, 290);");

            //Page Down  (Selenium Action Class)

            Actions actions4 = new Actions(driver);
            actions4.SendKeys(Keys.PageDown).Build().Perform();


            // Static Wait /Sleep

            Thread.Sleep(2000);

            // clear text box 

          

            //  Send text/ keys

            driver.FindElement(By.Id("texbox")).SendKeys("test");

            // Click

            driver.FindElement(By.Id("texbox")).Click();

            // Click dynamic object/image

            var CategoryLinks = driver.FindElements(By.Id("test"))[0];
            CategoryLinks.Click();

            // Verify Element displayed

            IWebElement element6 = driver.FindElement(By.Id("test"));
            Console.WriteLine(element6.Displayed);
            //or use
         

            //Assert checkbox ticked 

            Assert.IsTrue(driver.FindElement(By.XPath("test")).Selected);

            // Assert Are Equal to / Page Title

            Assert.AreEqual("bbc", driver.Title);

            // Assert page source

            string html = driver.PageSource;
            Assert.IsTrue(driver.FindElement(By.TagName("body")).Text.Contains(html));

            // Assert image displayed 

            Assert.IsTrue(driver.FindElement(By.Id("henryjpeg")).Displayed);

            // Assert page item using body tagname

            Assert.IsTrue(driver.FindElement(By.TagName("body")).Text.Contains("Base rate updated"));

            // Assert is False checkbox not clicked

            Assert.IsFalse(driver.FindElement(By.XPath("test")).Enabled);

            // Navigate forward/ backwards

            driver.Navigate().Back();


            // Accept alert/dismiss

            IAlert alert = driver.SwitchTo().Alert();
            alert.Accept();

            //SWITCH TO NEW TAB POP UP which opens after a click
            // handle multiple windows

            var popups = driver.WindowHandles[1];
            Assert.AreEqual(driver.SwitchTo().Window(popups).Url, "https test.com");
            driver.SwitchTo().Window(driver.WindowHandles[1]).Close();
            driver.SwitchTo().Window(driver.WindowHandles[0]);


            // Implicit wait

            driver.Manage().Timeouts().ImplicitWait = TimeSpan.FromSeconds(3);
      

            // Explicit wait

            //WebDriverWait wait = new WebDriverWait(driver, TimeSpan.FromSeconds(10));
            //IWebElement myDynamicElement = wait.Until<IWebElement>(d => d.FindElement(By.Id("someDynamicElement")));
            //   element7.Click();

            WebDriverWait wait = new WebDriverWait(driver, TimeSpan.FromSeconds(3));
            IWebElement element7 = wait.Until<IWebElement>(d => d.FindElement(By.Id("test")));
            element7.Click();

            // How to handle hidden elements in Selenium WebDriver?

            IWebElement hiddenInput = driver.FindElement(By.Id("code"));
            String value = hiddenInput.GetAttribute("value");

            // Find broken links in a webpage

            // List links = driver.FindElement(By.TagName("a"));

            // How to Upload a file in Selenium WebDriver?

            IWebElement UploadFiles = driver.FindElement(By.Id("searchbar"));
            UploadFiles.SendKeys("C:\\pics\\me");


            // How to switch between frames in Selenium?

            driver.SwitchTo().ParentFrame();
     

            //Resize Browser Window ssize

            driver.Manage().Window.Size = new Size(880, 940);

            try
            {
                Assert.IsTrue(driver.FindElement(By.TagName("body")).Text.Contains("test"));
                 
            }
            catch (Exception e)
            {

                throw;
            }
          

            // Switch Statement

            //     public class WebDriverFactory
            //{
            //    public IWebDriver GetWebDriver(string BrowserName)
            //    {
            //        IWebDriver driver;
            //        switch (BrowserName)
            //        {
            //            case "FireFox":
            //                driver = new FirefoxDriver();
            //                break;
            //            case "InternetExplorer":
            //                driver = new InternetExplorerDriver();
            //                break;
            //            default:
            //                driver = new ChromeDriver();
            //                break;
            //        }

            //        driver.Manage().Timeouts().ImplicitWait = TimeSpan.FromSeconds(20);

            //        return driver;
            //    }
            //}
