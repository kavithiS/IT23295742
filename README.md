# Playwright Automation –Assignment 1 - IT23295742 

Automated test suite for [SwiftTranslator](https://www.swifttranslator.com/) - a Singlish to Sinhala translation web application.

##  Project Overview

This project contains **35 comprehensive test cases** covering:

- ✅ 24 Positive Functional Tests (Pos_Fun)
- ✅ 10 Negative Functional Tests (Neg_Fun)
- ✅ 1 UI Test (Pos_UI)

Built with **Playwright Test Framework** for robust, reliable browser automation.

---

##  Prerequisites

Before you begin, ensure you have the following installed:

1. **Node.js** (v18 or higher)
   - Download: https://nodejs.org/
   - Verify installation: `node --version`

2. **Google Chrome Browser**
   - The tests use real Chrome (not Chromium) to avoid automation detection
   - Download: https://www.google.com/chrome/

3. **Git** (optional, for version control)
   - Download: https://git-scm.com/

---

##  Installation

### Step 1: Clone or Download the Project

```bash
# If using Git
git clone <repository-url>
cd IT23295742

# Or download and extract ZIP, then navigate to folder
cd IT23295742
```

### Step 2: Install Dependencies

```bash
npm install
```

This will install:

- `@playwright/test` - Playwright Test Framework
- `@types/node` - TypeScript definitions for Node.js

### Step 3: Install Playwright Browsers

```bash
npm run install:browsers
# or
npx playwright install
```

This downloads the required browser binaries (Chromium, Firefox, WebKit).

**Note:** If you only want Chrome:

```bash
npx playwright install chrome
```

---

##  Running Tests

### Run All Tests (Recommended)

```bash
npm test
# or
npx playwright test swifttranslator-all.spec.js --project=chrome
```

**Note:** Tests run with **visible browser** by default (headed mode) to avoid bot detection. Tests run sequentially to avoid API rate limiting.

### Run in Headless Mode

For faster execution without visible browser:

```bash
npm run test:headless
# or
npx playwright test swifttranslator-all.spec.js --project=chrome --headless
```

### Run with Visible Browser (Explicit)

```bash
npm run test:headed
# or
npx playwright test swifttranslator-all.spec.js --project=chrome --headed
```

### Run Specific Test Case

```bash
# By test name pattern
npx playwright test swifttranslator-all.spec.js -g "Pos_Fun_0001" --project=chrome

# By test ID
npx playwright test swifttranslator-all.spec.js -g "TC1" --project=chrome
```

### Debug Mode

```bash
npm run test:debug
# or
npx playwright test swifttranslator-all.spec.js --project=chrome --debug
```

Opens Playwright Inspector for step-by-step debugging.

### View Test Report

After tests complete, view the HTML report:

```bash
npm run test:report
# or
npx playwright show-report
```

---

##  Project Structure

```
IT23295742/
├── tests/
│   └── swifttranslator-all.spec.js    # Main test suite (35 tests)
├── playwright.config.js               # Playwright configuration
├── test-cases.md                      # Test case documentation with results
├── package.json                       # Project dependencies
└── README.md                          # This file
```

---

##  Configuration

The test suite is configured in `playwright.config.js`:

| Setting         | Value   | Reason                                            |
| --------------- | ------- | ------------------------------------------------- |
| `workers`       | 1       | Run tests sequentially to avoid API rate limiting |
| `fullyParallel` | false   | Prevent concurrent API requests                   |
| `retries`       | 2       | Retry failed tests twice                          |
| `timeout`       | 60000ms | Allow time for translation API response           |
| `headless`      | false   | Use headed mode to avoid bot detection            |
| `channel`       | chrome  | Use real Chrome browser (not Chromium)            |

**Anti-Bot Protection:**

```javascript
args: [
  "--disable-blink-features=AutomationControlled",
  "--disable-features=site-per-process",
  "--no-sandbox",
];
```

---

##  Test Results

### Current Status (as of January 31, 2026)

| Status     | Count | Description                                  |
| ---------- | ----- | -------------------------------------------- |
| ✅ PASS    | 32    | All functional tests verified and passing    |
| ⏭️ SKIPPED | 3     | TC23, TC28, TC33 (emoji/newline limitations) |

**Final Results: 32 PASSED ✅ | 3 SKIPPED ⏭️ | 0 FAILED ❌**

**Sample Verified Test Cases:**

- ✅ **TC1** (Pos_Fun_0001): Daily greeting - `haloo suba udhaesanak` → `හලෝ සුබ උදැසනක්`
- ✅ **TC2** (Pos_Fun_0002): Polite request - `oyaata puluvandha...` → `ඔයාට පුලුවන්ද...`
- ✅ **TC3** (Pos_Fun_0003): Informal command - `adoo ikmanata enna!` → `අඩෝ ඉක්මනට එන්න!`
- ✅ **TC26** (Neg_Fun_0002): Spelling errors - Literal transliteration behavior verified
- ✅ **TC35** (Pos_UI_0001): Real-time translation - `man car ekak gaththaa` → `man car එකක් ගත්තා`

---

##  Troubleshooting

### Issue: Tests fail with "Browser not found"

**Solution:**

```bash
npx playwright install chrome
```

### Issue: All tests fail with empty output

**Cause:** API rate limiting or temporary unavailability

**Solutions:**

1. Wait 5-10 minutes before retrying
2. Check if the website works manually: https://www.swifttranslator.com/
3. Verify internet connection and try again

### Issue: "Cannot find module @playwright/test"

**Solution:**

```bash
npm install
```

### Issue: Tests timeout

**Possible causes:**

- Slow internet connection
- API latency
- Website under heavy load

**Solution:** Increase timeout in `playwright.config.js`:

```javascript
timeout: 120000, // 2 minutes
```

---

##  Test Case Documentation

Full test case specifications are documented in:

- **test-cases.md** - All 35 test cases with expected/actual results and final verification status

### Test Categories

**Positive Functional Tests (Pos_Fun_0001 - Pos_Fun_0024)**

- Basic translations (greetings, daily phrases)
- Different tenses (past, present, future)
- Complex sentences (conditionals, questions)
- Mixed Singlish and English
- Special characters (numbers, currency, dates)

**Negative Functional Tests (Neg_Fun_0001 - Neg_Fun_0010)**

- Joined words without spaces
- Heavy spelling errors
- Random symbols
- Emoji handling
- Ambiguous inputs
- Abbreviations

**UI Tests (Pos_UI_0001)**

- Real-time translation updates

---

##  Advanced Usage

### Run Tests in Different Browsers

```bash
# Firefox
npx playwright test swifttranslator-all.spec.js --project=firefox

# Chromium
npx playwright test swifttranslator-all.spec.js --project=chromium

# WebKit (Safari)
npx playwright test swifttranslator-all.spec.js --project=webkit
```

**Note:** Chrome project is recommended for best results due to anti-bot measures.

### Run with Custom Reporter

```bash
# JSON reporter
npx playwright test swifttranslator-all.spec.js --project=chrome --reporter=json

# List reporter (detailed console output)
npx playwright test swifttranslator-all.spec.js --project=chrome --reporter=list
```

### Update Snapshots (if using visual testing)

```bash
npx playwright test --update-snapshots
```

---

##  Notes

- **API Dependency:** Tests require SwiftTranslator API to be available
- **Rate Limiting:** Run tests sequentially to avoid being blocked
- **Browser Requirement:** Chrome browser must be installed on system
- **Execution Time:** Full suite takes ~4-5 minutes (35 tests, 32 executed × ~8s each)
- **Network:** Stable internet connection required

---

##  Support

For issues or questions:

1. Review test output logs in the terminal
2. Check HTML report: `npx playwright show-report`
3. Verify the SwiftTranslator website is accessible manually
4. Check **test-cases.md** for expected vs actual outputs

---

##  License

ISC

---

##  Quick Reference

### NPM Scripts (Recommended)

| Command                    | Description                  |
| -------------------------- | ---------------------------- |
| `npm install`              | Install dependencies         |
| `npm run install:browsers` | Install Playwright browsers  |
| `npm test`                 | Run all tests (headed mode)  |
| `npm run test:headless`    | Run tests without browser UI |
| `npm run test:headed`      | Run with visible browser     |
| `npm run test:debug`       | Debug mode                   |
| `npm run test:report`      | View test report             |

### Playwright Commands (Alternative)

| Command                                                                              | Description                  |
| ------------------------------------------------------------------------------------ | ---------------------------- |
| `npx playwright install chrome`                                                      | Install Chrome browser       |
| `npx playwright test swifttranslator-all.spec.js --project=chrome`                   | Run all tests (headed mode)  |
| `npx playwright test swifttranslator-all.spec.js --project=chrome --headless`        | Run tests without browser UI |
| `npx playwright test swifttranslator-all.spec.js --project=chrome --headed`          | Run with visible browser     |
| `npx playwright test swifttranslator-all.spec.js -g "Pos_Fun_0001" --project=chrome` | Run specific test            |
| `npx playwright show-report`                                                         | View test report             |
| `npx playwright test --debug`                                                        | Debug mode                   |

---


