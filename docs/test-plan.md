# Test Plan: RealWorld (Conduit)

- **Version:** 0.2
- **Status:** Draft for review
- **Date:** 2026-10-15
- **Author:** Hemlal
- **Related documents:** requirements.md, exploration-notes.md

## 1. Introduction

This plan describes how the RealWorld (Conduit) web application will be tested. The application is a blogging platform where users can publish articles, comment, favorite, follow other users and manage a profile. No original specification exists, so the test basis is requirements.md, which was derived from exploratory testing.

## 2. Scope

**In scope (functional testing of the web UI):**

- Authentication: sign up, login, logout (REQ-AUTH)
- Articles: create, edit, delete, validation, unique URL, article not found (REQ-ART)
- Comments: post, validation, delete (REQ-COM)
- Social: favorite, follow, Your Feed (REQ-SOC)
- Discovery: Global Feed, tag filter (REQ-DIS)
- Profile: view profile, update settings (REQ-PRO)

**Out of scope (for this version):**

- Performance and load testing
- Security testing (beyond the generic login error message)
- Mobile and responsive layout testing
- Accessibility testing
- Cross-browser testing (only Microsoft Edge is used)
- Backend/API testing and database verification (planned for a later phase)

## 3. Test approach

- **Test design:** For each requirement, test cases cover positive, negative, boundary and edge scenarios.
- **Execution:** Manual testing, one variable changed at a time.
- **Exploratory testing:** Time-boxed sessions after scripted tests to find defects outside the documented cases.
- **Regression:** A core set of test cases (smoke/regression suite) is re-run after every change and after every bug fix.
- **Traceability:** Every test case references a requirement ID. A traceability matrix (RTM) links requirements, test cases and defects.
- **Automation:** Stable regression cases will be automated later with Python, pytest and Playwright.

## 4. Test environment

| Item         | Value                                                                |
| ------------ | -------------------------------------------------------------------- |
| Application  | https://demo.realworld.show/ (Angular frontend, public demo backend) |
| Browser      | Microsoft Edge 155 (64-bit)                                          |
| OS           | Windows                                                              |
| Test account | Dedicated test account (no real personal data)                       |
| Later phase  | Local backend for controlled data                                    |

## 5. Test data

- Test data is created by the tester for each test run (articles, comments, favorites).
- Seed data on the demo (users johndoe, janesmith, mikewilson, sarahchen and their articles) is used read-only, except follow and favorite tests.
- No real personal data or real passwords are used.

## 6. Entry and exit criteria

**Entry criteria:**

- Requirements document is reviewed.
- The demo application is reachable and a test account can log in.
- Test cases are written and linked to requirement IDs.

**Exit criteria:**

- 100% of planned test cases are executed.
- All High severity defects are reported and retested, or accepted with a written reason.
- Test summary report is completed.

## 7. Defect management

- Defects are logged as GitHub Issues with: title, environment, steps, expected result, actual result, severity, priority, screenshot.
- Severity levels: High (blocks use or loses data), Medium (feature works incorrectly), Low (cosmetic or minor).
- Lifecycle: New, Confirmed, Fixed, Retested, Closed (or Reopened).

## 8. Risks and assumptions

| #   | Risk / assumption                                                                                                                              | Mitigation                                                      |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| 1   | No original specification; requirements are derived from observed behaviour and may contain mistakes.                                          | Review requirements; list open questions for the product owner. |
| 2   | The public demo may behave inconsistently. On 2026-10-14 the test data was temporarily not visible and later reappeared (cause not confirmed). | Create fresh data per test run; move to a local backend.        |
| 3   | Two defects were observed on 2026-10-13 and are not yet re-checked on a later date.                                                            | Re-verify before logging bug reports.                           |
| 4   | Only one browser is tested.                                                                                                                    | Documented as out of scope.                                     |

## 9. Deliverables

- Requirements (docs/requirements.md)
- Test plan (this document)
- Test cases (docs/test-cases.xlsx)
- Requirements traceability matrix (docs/rtm.xlsx)
- Defect reports (GitHub Issues)
- Test summary report (docs/test-summary-report.md)
