Permission Difference: NAV vs Business Central

🔍 Issue
    -> User migrated from NAV
    -> Existing NAV permissions do not behave the same in BC

🔍 Root Cause
    -> BC permission sets are more granular
    -> Some NAV permissions split into multiple BC sets

✅ Recommended Approach
    -> Start with:
        = BASIC / D365 BASIC
          Add functional permissions:
          1. Sales
          2. Purchase
          3. Item View / Edit
    -> Avoid giving SUPER unless required

------------------------------------------------------------------- TT__TT
Workflow / Approval Issues
❌ Issue
    -> Document approval not triggered
    -> User cannot approve workflow

🔍 Root Cause
    -> Workflow setup incomplete or disabled
    -> User not included in workflow participants
    -> Document does not meet triggering conditions

✅ How to Fix
    -> Verify Workflow Configuration
    -> Check Participants & Permissions
    -> Confirm Document meets triggering criteria
    -> Test workflow with sample document
