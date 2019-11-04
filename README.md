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
