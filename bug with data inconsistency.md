Issues

Code numbers to not seems to match the contact code that appear in the URLS accociated
with the data

The following information seems to be incorrect for most records:

-   decision_maker_contact_code - table 
-   system_admin_contact_code - table
-   system build - table
-   system configured_nm4 - table
-   system configured_karaoke - table

For client code contact code 19005

This is what they get back
```typescript
{
      "code": "JVIL0001",
      "name": "1841 Bar & Restaurant",
      "system_admin_contact_code": 190005, // incorrect
      "decision_maker_contact_code": 157928, // incorrect
      "systems": [
        {
          "code": "JVIL0001A",
          "build": "B33W",  // incorrect
          "configured_nm4": "NO", // incorrect 
          "configured_karaoke": "YES", // incorrect
        }
      ]
    }
```

- Fixed the switched config between nm4 and karaoke
- Need to look at intranet to see what query they are making 
