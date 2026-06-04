# Notification Settings - Test Cases

## Test Case 1: Enable Email Notifications
- **Precondition:** User is logged in, email notifications disabled
- **Steps:**
  1. Navigate to Settings > Notifications
  2. Find "Email Notifications" toggle
  3. Click toggle to enable
  4. Click "Save Settings"
- **Expected Result:** Toggle is ON, "Settings saved" message shown
- **Priority:** High
- **Status:** Ready for automation

## Test Case 2: Disable Email Notifications
- **Precondition:** Email notifications are enabled
- **Steps:**
  1. Navigate to Settings > Notifications
  2. Click toggle to disable email notifications
  3. Click "Save Settings"
- **Expected Result:** Toggle is OFF, no more emails sent
- **Priority:** High
- **Status:** Ready for automation

## Test Case 3: Select Notification Frequency
- **Precondition:** Email notifications enabled
- **Steps:**
  1. Navigate to Settings > Notifications
  2. Select frequency dropdown
  3. Choose "Daily Digest"
  4. Click "Save Settings"
- **Expected Result:** Frequency changed to "Daily Digest", confirmation shown
- **Priority:** Medium
  - **Status:** Ready for automation

## Test Case 4: Unsubscribe from All Notifications
- **Precondition:** User has notification settings
- **Steps:**
  1. Navigate to Settings > Notifications
  2. Click "Unsubscribe from all"
  3. Confirm action
- **Expected Result:** All toggles OFF, confirmation email sent
- **Priority:** Medium
- **Status:** Ready for automation