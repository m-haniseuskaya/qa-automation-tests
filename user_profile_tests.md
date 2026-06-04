# User Profile Update - Test Cases

## Test Case 1: Update User Name
- **Precondition:** User is logged in
- **Steps:**
  1. Navigate to Profile Settings
  2. Click "Edit Name"
  3. Clear current name
  4. Enter new name "Jane Doe"
  5. Click "Save"
- **Expected Result:** Profile updated, "Profile saved successfully" message shown
- **Priority:** High
- **Status:** Ready for automation

## Test Case 2: Update Email Address
- **Precondition:** User is logged in
- **Steps:**
  1. Navigate to Profile Settings
  2. Click "Edit Email"
  3. Enter new email "jane.doe@example.com"
  4. Click "Save"
  5. Verify confirmation email sent
- **Expected Result:** Email updated, confirmation sent
- **Priority:** High
- **Status:** Ready for automation

## Test Case 3: Update Avatar Image
- **Precondition:** User is logged in, image file exists
- **Steps:**
  1. Navigate to Profile Settings
  2. Click on current avatar
  3. Select new image file
  4. Click "Upload"
- **Expected Result:** Avatar updated immediately, profile refreshed
- **Priority:** Medium
- **Status:** Ready for automation

## Test Case 4: Cancel Profile Update
- **Precondition:** User is on Profile Settings
- **Steps:**
  1. Make changes to profile
  2. Click "Cancel" button
- **Expected Result:** Changes discarded, profile reverts to original
- **Priority:** Medium
- **Status:** Ready for automation

## Test Case 5: Reject Invalid Email Format
- **Precondition:** User is on Profile Settings
- **Steps:**
  1. Click "Edit Email"
  2. Enter invalid email "notanemail"
  3. Click "Save"
- **Expected Result:** Error message "Invalid email format" shown, profile not updated
- **Priority:** High
- **Status:** Ready for automation