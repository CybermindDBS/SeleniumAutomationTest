# Selenium TestNG Sandbox

A small TestNG harness for Selenium, kept as a reference for the pieces that are fiddly to wire up
from memory: retry analysers, Extent reporting, and Excel-driven data providers.

Currently exercises dropdown handling against the Bootstrap form-select docs page. The point is the
scaffolding, not coverage.

## What is wired up

- **`RetryAnalyzer`** — reruns a failed test up to a limit, attached through TestNG rather than in
  test code
- **`ExtentReporterListener`** — an `ITestListener` that builds an Extent HTML report as tests run
- **`TestDataProvider`** — TestNG `@DataProvider` reading cases from `testData.xlsx`, so cases are
  added in the spreadsheet instead of in Java
- **`ExcelUtil`** — Apache POI read and write helpers; results are written back to `testOutput.xlsx`
- **`DriverFactory`** — local or Grid driver from one property, Chrome and Edge
- **`BaseTest`** — driver setup and teardown per test

## Running it

```
mvn test
```

Runs the suite in `src/test/resources/testng.xml`. The report is written to
`src/test/resources/extent-report.html`.

Everything is configured in `src/test/resources/config.properties`:

```properties
test.target=https://getbootstrap.com/docs/5.0/forms/select/
test.launch_mode=local          # or: remote
selenium.grid.hub_url=http://localhost:4444/wd/hub
in.excel=src/test/resources/testData.xlsx
out.excel=src/test/resources/testOutput.xlsx
```

Set `test.launch_mode=remote` to run against a Grid. The server jar is in `selenium-grid-jar/`.

## Related

For a fuller framework — BDD specs, Page Object Model, tag-based suites and automatic retesting of
failed scenarios — see
[SeleniumGridHackathon](https://github.com/CybermindDBS/SeleniumGridHackathon).
