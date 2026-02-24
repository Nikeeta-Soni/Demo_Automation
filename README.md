# Automation Framework

A comprehensive end-to-end test automation framework built with **Playwright** for the [Automation Exercise](http://automationexercise.com) e-commerce demo application. This project demonstrates modern web automation best practices using the Page Object Model pattern with stable selectors and explicit assertions.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [Running Tests](#running-tests)
- [Test Scenarios](#test-scenarios)
- [Page Objects](#page-objects)
- [Best Practices](#best-practices)
- [Utilities](#utilities)
- [Troubleshooting](#troubleshooting)

---

## 🎯 Project Overview

This automation framework validates the complete user lifecycle on the Automation Exercise website:

1. **User Registration** - Create a new account with personal details
2. **Account Verification** - Confirm account creation success
3. **User Login** - Successfully authenticate with credentials
4. **Account Deletion** - Remove the account from the system
5. **E-commerce Flows** - Test various product browsing and purchase scenarios

### Key Features

✅ **Page Object Model** - Organized, maintainable test structure  
✅ **Stable Selectors** - Uses `getByRole()` and `getByLabel()` for resilience  
✅ **Explicit Assertions** - Every step validated with clear expectations  
✅ **Single Worker Execution** - Sequential test execution prevents conflicts  
✅ **Comprehensive Reporting** - HTML reports with screenshots and traces  
✅ **Test Data Management** - Centralized test data helpers  

---

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v16 or higher)
- **npm** (v7 or higher)
- **Git** (optional, for version control)

---

## 🚀 Installation

1. **Clone the repository** (if applicable):
   ```bash
   git clone <repository-url>
   cd AutomationPractice
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Install Playwright browsers**:
   ```bash
   npx playwright install
   ```

---

## 📁 Project Structure

```
AutomationPractice/
├── tests/                          # Test specifications
│   ├── userSignupFlow.spec.js     # User registration and login tests
│   ├── brandCartCheckoutFlow.spec.js # E-commerce flow tests
│   ├── dressProductFlow.spec.js   # Product filtering and selection
│   ├── contactUsFlow.spec.js      # Contact form submission
│   ├── negativeTests.spec.js      # Error and validation tests
│   └── APIWebAutomation.spec.js   # API integration tests
│
├── pages/                          # Page Object Model classes
│   ├── HomePage.js                # Landing page interactions
│   ├── SignupLoginPage.js         # Auth page interactions
│   ├── AccountInfoPage.js         # Account creation form
│   ├── ProductDetailPage.js       # Product information
│   ├── CategoryPage.js            # Product category browsing
│   ├── CartPage.js                # Shopping cart operations
│   ├── CheckoutPage.js            # Order checkout
│   ├── PaymentPage.js             # Payment processing
│   ├── BrandsPage.js              # Brand filtering
│   └── ContactUsPage.js           # Contact form
│
├── utils/                          # Utility functions and helpers
│   ├── testDataHelper.js          # Centralized test data constants
│   └── APiUtils.js                # API helper functions
│
├── fixtures/                       # Test data files
│   └── file-sample_100kB.doc      # Sample document for file uploads
│
├── playwright-report/             # Test execution reports (auto-generated)
│   └── index.html                 # View report in browser
│
├── test-results/                  # Test artifacts (screenshots, traces)
│
├── playwright.config.js           # Playwright configuration
├── package.json                   # Project dependencies and metadata
├── CLAUDE.md                      # Project context notes
└── README.md                      # This file
```

---

## ⚙️ Configuration

### Playwright Configuration (`playwright.config.js`)

Key configuration settings:

| Setting | Value | Purpose |
|---------|-------|---------|
| `testDir` | `./tests` | Directory containing test files |
| `fullyParallel` | `false` | Run tests sequentially (prevents conflicts) |
| `workers` | `1` | Single worker to prevent account conflicts |
| `timeout` | `120000` | 2 minutes overall test timeout |
| `reporter` | `html` | Generate HTML test reports |
| `headless` | `true` | Run in headless mode |
| `slowMo` | `500ms` | Slow down actions for visibility |
| `screenshot` | `only-on-failure` | Capture screenshots on failures |
| `trace` | `on-first-retry` | Record traces on test retry |

---

## 🧪 Running Tests

### Run All Tests
```bash
npx playwright test
```

### Run Specific Test File
```bash
npx playwright test tests/userSignupFlow.spec.js
```

### Run Tests in Headed Mode (with visible browser)
```bash
npx playwright test --headed
```

### Run Tests with Debug Mode
```bash
npx playwright test --debug
```

### Run Tests with UI Mode (interactive test runner)
```bash
npx playwright test --ui
```

### Run Specific Test by Name
```bash
npx playwright test -g "User Signup and Login Flow"
```

### View Test Report
```bash
npx playwright show-report
```

---

## 📝 Test Scenarios

### 1. User Signup Flow (`userSignupFlow.spec.js`)
Tests the complete user registration and login journey:
- Navigate to homepage
- Click "Signup / Login"
- Fill signup form with new credentials
- Handle both new user and existing user scenarios
- Complete account creation form
- Verify successful login

### 2. Brand & Cart Checkout Flow (`brandCartCheckoutFlow.spec.js`)
Tests e-commerce purchasing workflow:
- Browse by brand
- Add products to cart
- Proceed to checkout
- Enter payment details
- Confirm order placement

### 3. Dress Product Flow (`dressProductFlow.spec.js`)
Tests product filtering and selection:
- Navigate to dress category
- Apply filters (color, size, price)
- View product details
- Verify product information

### 4. Contact Us Flow (`contactUsFlow.spec.js`)
Tests contact form submission:
- Fill contact form with valid data
- Submit form
- Verify success message
- Upload file if applicable

### 5. Negative Tests (`negativeTests.spec.js`)
Tests error handling and validation:
- Invalid login credentials
- Duplicate account registration
- Empty form submissions
- Invalid email formats

### 6. API Web Automation (`APIWebAutomation.spec.js`)
Tests API integrations alongside UI:
- Verify API responses match UI displays
- Test backend validations
- Confirm data persistence

---

## 🏗️ Page Objects

### HomePage
Handles interactions on the landing page:
- `goto()` - Navigate to the homepage
- `clickSignupLogin()` - Click signup/login button
- `verifyHomePageVisible()` - Assert homepage is displayed

### SignupLoginPage
Manages signup and login form interactions:
- `fillSignupForm(name, email)` - Enter signup credentials
- `clickSignup()` - Submit signup form
- `fillLoginForm(email, password)` - Enter login credentials
- `clickLogin()` - Submit login form
- `verifyNewUserSignupVisible()` - Assert signup heading

### AccountInfoPage
Handles account creation form:
- `selectTitleMr()` - Select salutation
- `enterPassword(password)` - Enter password
- `setDateOfBirth(day, month, year)` - Set DOB
- `fillAddressDetails(addressObj)` - Fill address information
- `clickCreateAccount()` - Submit account creation

### ProductDetailPage, CategoryPage, CartPage, CheckoutPage, PaymentPage, BrandsPage, ContactUsPage
Encapsulate specific page functionality following the same principles of:
- Locator definitions
- User actions
- Assertion methods

---

## ✅ Best Practices

### 1. Use Stable Selectors
```javascript
// ✅ Good
await page.getByRole('button', { name: 'Login' }).click();
await page.getByLabel('Email').fill('user@example.com');

// ❌ Avoid
await page.locator('button:nth-child(3)').click();
await page.locator('input[type="email"]').fill('user@example.com');
```

### 2. Explicit Assertions
```javascript
// ✅ Good - Clear expectation
await expect(page.locator('h2')).toContainText('Account Created!');

// ❌ Avoid - Implicit waits
await page.waitForTimeout(1000);
```

### 3. Page Object Pattern
```javascript
// ✅ Good - Encapsulated interactions
await homePage.clickSignupLogin();

// ❌ Avoid - Direct UI interactions in tests
await page.locator('a[href="/login"]').click();
```

### 4. Visibility Before Interaction
```javascript
// ✅ Good - Always wait for visibility
await expect(signupForm).toBeVisible();
await signupForm.fill(data);

// ❌ Avoid - Blindly interact
await form.fill(data);
```

### 5. Centralized Test Data
```javascript
// ✅ Good - Use test data helper
const user = TEST_USER;
await signup(user.email, user.password);

// ❌ Avoid - Hardcoded values
await signup('test@example.com', 'password123');
```

---

## 🛠️ Utilities

### testDataHelper.js
Centralized test data management:

```javascript
export const TEST_USER = {
  name: 'Mathew Smith',
  email: 'mathew@yopmail.com',
  password: 'mathew@123',
  dob: { day: 17, month: 'March', year: 2001 },
  address: {
    firstName: 'Mathew',
    lastName: 'Smith',
    company: 'Mathew Inc Pvt Ltd',
    address: 'Address',
    // ... more fields
  }
};
```

### APiUtils.js
Helper functions for API testing:
- API request methods
- Response validation
- Data assertion utilities

---

## 🐛 Troubleshooting

### Issue: Tests timeout on CI
**Solution**: Increase timeout in `playwright.config.js` or check network conditions.

### Issue: Selectors fail intermittently
**Solution**: Use explicit waits and `getByRole()`/`getByLabel()` instead of CSS selectors.

### Issue: "Email already exists" in signup tests
**Solution**: Use unique email addresses or clean up test data between runs. The current implementation handles this with conditional logic.

### Issue: Screenshots not being captured
**Solution**: Ensure `screenshot: 'only-on-failure'` is set in config and tests are actually failing.

### Issue: Cannot find element
**Solution**: 
1. Run test in headed mode: `npx playwright test --headed`
2. Use debug mode: `npx playwright test --debug`
3. Check if page fully loaded with `page.waitForLoadState()`

---

## 📊 Test Reports

After running tests, view the HTML report:

```bash
npx playwright show-report
```

The report includes:
- ✅ Passed/Failed test breakdown
- 📸 Screenshots of failures
- 🎬 Video traces (if enabled)
- ⏱️ Execution duration
- 📋 Detailed error messages

---

## 🔄 CI/CD Integration

This framework is ready for CI/CD pipelines. Add to your workflow:

```yaml
# Example GitHub Actions
- name: Run tests
  run: npx playwright test
  
- name: Upload report
  if: always()
  uses: actions/upload-artifact@v3
  with:
    name: playwright-report
    path: playwright-report/
```

---

## 📚 Resources

- [Playwright Documentation](https://playwright.dev)
- [Automation Exercise Website](http://automationexercise.com)
- [Page Object Model Pattern](https://playwright.dev/docs/pom)
- [Best Practices](https://playwright.dev/docs/best-practices)

---

## 💡 Tips & Tricks

1. **Debug a specific test**: Use `test.only()` to run single test
2. **Skip a test**: Use `test.skip()` to temporarily disable
3. **Use trace viewer**: `npx playwright show-trace trace.zip`
4. **Inspect element**: Use Inspector tool - `npx playwright codegen http://automationexercise.com`

---

## 🤝 Contributing

When adding new tests:
1. Create page object classes for new pages
2. Follow the naming convention: `PageNamePage.js`
3. Use stable selectors (getByRole, getByLabel)
4. Add explicit assertions for each step
5. Document test purpose in comments
6. Update this README if adding new test categories

---

## 📄 License

ISC

---

## 👤 Author

Created for automation practice and learning purposes.

---

**Last Updated**: February 2026

For questions or issues, refer to the test files and page object implementations for detailed code examples.
