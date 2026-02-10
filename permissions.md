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
