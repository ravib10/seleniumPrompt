https://github.com/PramodDutta/qaskills/blob/main/seed-skills/graphql-testing/SKILL.md


L2S prompt::
Here is a comprehensive, master prompt you can use to generate an identical, enterprise-grade automation framework from scratch. You can copy and paste this into any AI assistant (like me!) when starting a new project.

***

### 📋 The Master Prompt

**System Role & Task:**
You are an expert QA Automation Architect. I want you to generate a complete, enterprise-grade UI automation framework from scratch using Java, Maven, Selenium WebDriver, and Cucumber BDD.

**Architecture & Design Patterns:**
Please strictly adhere to the following design patterns and structure:
1. **Page Object Model (POM):** Use Selenium's `PageFactory` and `@FindBy` annotations. UI elements and page actions must be strictly separated from test logic.
2. **Base Page Concept:** Create a `BasePage.java` that all Page Objects inherit from. It must contain robust wrapper methods for common actions (`click`, `sendKeys`, `isDisplayed`, `getText`) that implement `WebDriverWait` explicit waits, gracefully handle `StaleElementReferenceException`, and include fallback mechanisms (e.g., JavaScript clicks if standard clicks fail).
3. **No Hardcoded Values:** Create a `utils.Constants.java` file containing `public static final String` variables for all XPath/CSS locators, HTML IDs, and logging descriptions. Page objects should import these constants rather than hardcoding strings.
4. **Dependency Injection:** Use `cucumber-picocontainer` to share state (like the `DriverManager` and `ConfigReader`) seamlessly between Step Definition classes and `Hooks.java`. Do not use static drivers.
5. **Smart Configuration Management:** Create a `ConfigReader.java` that reads a single `config.properties` file. It must support environment-specific keys (e.g., `qa.baseUrl`, `dev.baseUrl`) based on a `-Denv=qa` system property, and gracefully fall back to generic keys (like `browser=chrome`) or code-level default fail-safes if missing.

**Core Components Needed:**
Please provide the complete code for the following files, ensuring they are properly packaged:
1. `pom.xml` (with dependencies for Selenium 4, Cucumber Java/JUnit/PicoContainer, WebDriverManager, and log4j).
2. `utils.ConfigReader.java` (with the smart environment fallback logic).
3. `utils.DriverManager.java` (handling Chrome/Firefox/Edge setup, headless mode toggles, and safe teardown).
4. `utils.Constants.java` (a template for locators and strings).
5. `pages.BasePage.java` (with explicit waits and JS execution capabilities).
6. `steps.Hooks.java` (to handle setup, teardown, and taking screenshots on test failures using `@After`).
7. `runners.TestRunner.java` (JUnit runner configured for Cucumber).

**Coding Standards:**
- Code must compile perfectly in Java 17.
- Implement defensive programming: check for nulls and catch timeouts elegantly without crashing the whole suite unexpectedly.
- Use `logger.debug` or `System.out.println` inside `BasePage` wrapper methods so that every click and keystroke is automatically logged for easy debugging.

***

### How to use this prompt in the future:
When you start a new project, just paste that prompt. Once the AI gives you the foundational files, you can follow up with: *"Great, now here is the HTML for my Login Page. Please generate the `LoginPage.java`, `LoginSteps.java`, and `Login.feature` files following the framework rules you just built."*
