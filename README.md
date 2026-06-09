https://github.com/PramodDutta/qaskills/blob/main/seed-skills/graphql-testing/SKILL.md


L2S prompt::
Here is the final, fully-loaded master prompt. It includes everything: both feature files, the multi-environment logic, the advanced page object patterns, and the explicit instructions for generating the exact TestRunner setup you want. 

You can save this somewhere safe and paste it into any AI whenever you need to spin up a new framework!

***

### 📋 The Ultimate Project Duplication Prompt

**System Role & Task:**
You are an expert QA Automation Architect. I need you to build a complete, enterprise-grade UI automation framework from scratch using Java, Maven, Selenium WebDriver, and Cucumber BDD. 

**The Target Application:**
The application under test is the GetPark registration flow. The base URL is `https://www.getpark.co.uk/budgeting/login.jsp`.

**The Testing Scope (The Feature Files):**
Create **TWO** feature files:

1. **`Register.feature` (The Happy Path):**
   - *Tag:* `@positive`
   - *Flow:* Go to login -> Click "Register Now" -> Verify Basket Empty Popup -> Click "Easy Sign Up" -> Click "Create My Account" -> Enter valid Registration Details (Title, First Name, Last Name, DOB) -> Click "Next Your contact info" -> Verify arrival on Contact Info page -> Click "Enter Address Manually" -> Enter valid Contact Details (Email, Mobile, Line 1, Town, Postcode) -> Click "Next Create your password" -> Verify arrival on Create Password page -> Enter valid Password -> Click Terms Checkbox -> Click "Continue to payment".

2. **`RegisterNegative.feature` (The Negative Paths):**
   - *Tag:* `@negative`
   - *Scenario Outline 1 (Registration Details):* Follow the flow to the Registration Details page, enter fields `title`, `firstName`, `lastName`, `dobDay`, `dobMonth`, `dobYear` from an Examples table. Click Next. Assert: `Then I should see a validation error for "<errorField>" with message "<expectedMessage>"`
   - *Scenario Outline 2 (Contact Info):* Follow the flow to the Contact Info page, click "Enter Address Manually", enter fields `email`, `mobile`, `addressLine1`, `town`, `postcode` from an Examples table. Click Next. Assert the exact same validation step.
   - *Scenario Outline 3 (Password):* Follow the flow to the Password page, enter `password` from an Examples table, click terms, click Continue. Assert the exact same validation step for the "pwd-input" field.

**Framework Architecture Requirements:**
1. **Dependency Injection:** Use `cucumber-picocontainer` to share a `DriverManager` and a `ConfigReader` between `RegisterSteps.java` and `Hooks.java`. Do not use static drivers.
2. **Smart Configuration (ConfigReader.java):** It must read a single `config.properties` file but dynamically check for environment prefixes (e.g., `qa.baseUrl`, `dev.baseUrl`) based on `System.getProperty("env", "qa")`. If no prefix is found, it must fall back to the generic key (like `browser=chrome`).
3. **Driver Management (DriverManager.java):** Must be a ThreadLocal or class-level Singleton handling Chrome options, headless execution (based on config), and implicit/page load timeouts.
4. **Base Page (BasePage.java):** All Page Objects must inherit from this. It must use `WebDriverWait` and `ExpectedConditions` for wrapper methods like `click()`, `sendKeys()`, and `isDisplayed()`. It must include a `jsClick()` method to use `JavascriptExecutor` as a fallback if standard clicks face interception errors. Include `logger.debug` statements in every wrapper method.
5. **No Hardcoded Values (Constants.java):** Create a `utils.Constants.java` file containing `public static final String` variables for EVERY XPath, Name, ID, Error Div ID, and Logging Description string. Page objects should import these constants rather than hardcoding strings.
6. **Page Object (RegisterPage.java):** Use `PageFactory` and `@FindBy` using the variables imported from `Constants.java`. Include a robust method `getFieldErrorMessage(String fieldIdentifier)` that maps the field to a specific Error Div ID (e.g. "emailAddress" maps to "emailError"), explicitly waits for it, and returns the exact inner text string of the error message.
7. **Hooks (Hooks.java):** Initialize the driver via PicoContainer constructor injection. Include an `@After` hook that takes a screenshot as a byte array (`((TakesScreenshot) driver).getScreenshotAs(OutputType.BYTES)`) and attaches it to the Cucumber scenario if `scenario.isFailed()` is true.

**Output Requirements:**
Please output the complete, fully written code for the following files, ensuring they are properly packaged and compile perfectly in Java 17:
- `pom.xml` (Selenium 4, Cucumber, PicoContainer, WebDriverManager)
- `src/test/resources/config.properties`
- `src/test/java/utils/Constants.java`
- `src/test/java/utils/ConfigReader.java`
- `src/test/java/utils/DriverManager.java`
- `src/test/java/pages/BasePage.java`
- `src/test/java/pages/RegisterPage.java`
- `src/test/java/steps/RegisterSteps.java`
- `src/test/java/steps/Hooks.java`
- `src/test/java/runners/TestRunner.java` **(Ensure the `@CucumberOptions` explicitly includes `tags = "@positive or @negative"`, the plugin setup for HTML reporting, and sets `publish = true`)**
- `src/test/resources/features/Register.feature`
- `src/test/resources/features/RegisterNegative.feature` (with the Data Tables fully populated with negative permutations).










L2S PLAYWRIGHT PROMPT::
Here is the modified master prompt, fully translated for the modern **Playwright + JavaScript + Playwright-BDD** stack! 

Playwright actually handles a lot of things (like drivers, screenshots, and waits) natively out-of-the-box, so this prompt instructs the AI to use Playwright's modern best practices while keeping the exact same structure and strictness you liked from the Java version.

***

### 🎭 The Playwright-BDD Project Duplication Prompt

**System Role & Task:**
You are an expert QA Automation Architect. I need you to build a complete, enterprise-grade UI automation framework from scratch using Node.js, JavaScript, Playwright, and `playwright-bdd`. The project will be developed in Visual Studio Code.

**The Target Application:**
The application under test is the GetPark registration flow. The base URL is `https://www.getpark.co.uk/budgeting/login.jsp`.

**The Testing Scope (The Feature Files):**
Create **TWO** feature files:

1. **`Register.feature` (The Happy Path):**
   - *Tag:* `@positive`
   - *Flow:* Go to login -> Click "Register Now" -> Verify Basket Empty Popup -> Click "Easy Sign Up" -> Click "Create My Account" -> Enter valid Registration Details (Title, First Name, Last Name, DOB) -> Click "Next Your contact info" -> Verify arrival on Contact Info page -> Click "Enter Address Manually" -> Enter valid Contact Details (Email, Mobile, Line 1, Town, Postcode) -> Click "Next Create your password" -> Verify arrival on Create Password page -> Enter valid Password -> Click Terms Checkbox -> Click "Continue to payment".

2. **`RegisterNegative.feature` (The Negative Paths):**
   - *Tag:* `@negative`
   - *Scenario Outline 1 (Registration Details):* Follow the flow to the Registration Details page, enter fields `title`, `firstName`, `lastName`, `dobDay`, `dobMonth`, `dobYear` from an Examples table. Click Next. Assert: `Then I should see a validation error for "<errorField>" with message "<expectedMessage>"`
   - *Scenario Outline 2 (Contact Info):* Follow the flow to the Contact Info page, click "Enter Address Manually", enter fields `email`, `mobile`, `addressLine1`, `town`, `postcode` from an Examples table. Click Next. Assert the exact same validation step.
   - *Scenario Outline 3 (Password):* Follow the flow to the Password page, enter `password` from an Examples table, click terms, click Continue. Assert the exact same validation step for the "pwd-input" field.

**Framework Architecture Requirements:**
1. **Playwright-BDD Setup:** Use `playwright-bdd` to integrate Cucumber feature files directly with the Playwright Test runner. Expose the `page` fixture to the step definitions.
2. **Smart Configuration (.env & playwright.config.js):** Use `dotenv` to handle multiple environments. Configure `playwright.config.js` to read `process.env.ENV` (defaulting to `qa`). Define `qa`, `dev`, and `uat` URLs inside the config file or `.env` files, and set `baseURL` dynamically.
3. **Native Driver & Screenshot Management:** Do not build a custom driver manager. Rely entirely on Playwright's native browser contexts. Configure `playwright.config.js` to automatically capture screenshots and traces on test failure (`screenshot: 'only-on-failure'`).
4. **Base Page (BasePage.js):** All Page Objects must inherit from this. While Playwright auto-waits, include wrapper methods for actions (e.g., `clickElement()`, `fillInput()`) that include `console.log` statements for easy debugging and use `page.locator()` strictly. Implement a `forceClick()` method utilizing `{ force: true }` as a fallback.
5. **No Hardcoded Values (constants.js):** Create a `utils/constants.js` file exporting a dictionary/object containing EVERY locator, exact error string, and HTML ID. Page objects must import these rather than hardcoding strings.
6. **Page Object (RegisterPage.js):** Use the modern Playwright Page Object Model. Pass the `page` fixture via the constructor. Include a robust method `getFieldErrorMessage(fieldIdentifier)` that maps the field to a specific Error Div ID (e.g. "emailAddress" maps to "emailError"), and returns the `innerText()` of the error message using Playwright's `locator.textContent()`.

**Output Requirements:**
Please output the complete, fully written code for the following files, ensuring they follow modern ES6 JavaScript module syntax (or CommonJS, but be consistent):
- `package.json` (Playwright, playwright-bdd, dotenv)
- `playwright.config.js` (Configured for BDD, multi-environment baseURLs, and failure screenshots)
- `.env` (Containing environment configurations)
- `utils/constants.js`
- `pages/BasePage.js`
- `pages/RegisterPage.js`
- `steps/fixtures.js` (If needed for playwright-bdd custom fixtures/page object mapping)
- `steps/RegisterSteps.js`
- `features/Register.feature`
- `features/RegisterNegative.feature` (with the Data Tables fully populated with negative permutations).
