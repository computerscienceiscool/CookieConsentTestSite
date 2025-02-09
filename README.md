# Cookie Consent Testing Checklist: WIP

## Setup
1. Open your browser (Chrome recommended for these tests)
2. Open Developer Tools:
   - Windows/Linux: Press F12 or Ctrl+Shift+I
   - Mac: Press Cmd+Option+I
   - Or right-click and select "Inspect"
3. Go to Application tab (Chrome) or Storage tab (Firefox)
4. Select "Cookies" in the left sidebar
5. Click the arrow next to "Cookies" and select your site's domain

## Test 1: Initial State
- [ ] Clear all cookies and site data:
   1. In Developer Tools, right-click on your domain
   2. Select "Clear" or "Delete all"
   3. Refresh the page
- [ ] Verify:
   1. Cookie consent banner appears
   2. No cookies present except strictly necessary
   3. Local storage is empty

## Test 2: Accept All Flow
- [ ] Click "Accept All" button
- [ ] Check Developer Tools for:
   1. necessary_cookie is present
   2. analytics_cookie is present
   3. marketing_cookie is present
- [ ] Check Local Storage for:
   1. cookieConsent = "all"
   2. analyticsConsent = "true"
   3. marketingConsent = "true"
   4. consentTimestamp exists

## Test 3: Necessary Only Flow
- [ ] Clear all cookies and storage
- [ ] Click "Necessary Only" button
- [ ] Verify:
   1. Only necessary_cookie is present
   2. No analytics_cookie exists
   3. No marketing_cookie exists
- [ ] Check Local Storage for:
   1. cookieConsent = "necessary"
   2. analyticsConsent = "false"
   3. marketingConsent = "false"
   4. consentTimestamp exists

## Test 4: Custom Preferences
- [ ] Clear all cookies and storage
- [ ] Click "Cookie Preferences"
- [ ] Verify preference panel shows:
   1. Necessary Cookies checked and disabled
   2. Analytics Cookies unchecked
   3. Marketing Cookies unchecked
- [ ] Check only Analytics Cookies
- [ ] Click Save
- [ ] Verify:
   1. necessary_cookie exists
   2. analytics_cookie exists
   3. marketing_cookie does not exist
- [ ] Check Local Storage for:
   1. cookieConsent = "custom"
   2. analyticsConsent = "true"
   3. marketingConsent = "false"

## Test 5: Cookie Properties
For each cookie present, verify properties:
- [ ] Secure flag is set
- [ ] SameSite attribute is set
- [ ] Path is correct
- [ ] Expiration is 24 hours (86400 seconds)

## Test 6: Persistence
- [ ] Set preferences using any method
- [ ] Refresh the page
- [ ] Verify:
   1. Banner doesn't reappear
   2. Cookies remain consistent
   3. Preferences are maintained

## Test 7: Preference Updates
- [ ] With existing preferences set:
   1. Open Cookie Preferences
   2. Change some options
   3. Save changes
- [ ] Verify:
   1. Cookies update correctly
   2. Local Storage updates
   3. Timestamp updates

## Common Issues to Watch For
1. Cookie Banner reappearing when it shouldn't
2. Cookies being set before consent
3. Preferences not saving correctly
4. Missing or incorrect cookie properties
5. Inconsistent state between cookies and local storage

## How to Document Issues
For each issue found:
1. Note the test case number
2. Screenshot the Developer Tools state
3. List steps to reproduce
4. Document expected vs actual behavior

## Developer Tools Quick Reference

### View Cookies
```text
Application (Chrome) or Storage (Firefox)
  └─ Cookies
      └─ [your-domain]
```

### View Local Storage
```text
Application
  └─ Local Storage
      └─ [your-domain]
```

### Clear Data
```text
Application
  └─ Clear Storage
      └─ Clear site data
```

## Notes
- Document any deviations from expected behavior
- Note browser version used for testing
- Record timestamps of tests
- Save screenshots of significant findings
