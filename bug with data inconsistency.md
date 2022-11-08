Issues

Code numbers to not seems to match the contact code that appear in the URLS associated
with the data

The following information seems to be incorrect for most records:

-   decision_maker_contact_code - table
-   system_admin_contact_code - table
-   system build - table
-   system configured_nm4 - table
-   system configured_karaoke - table

For client code contact code 19005

This is what Martin gets back. Comments show the deltas between his response and mine.

```typescript
{
      "code": "JVIL0001",
      "name": "1841 Bar & Restaurant",
      "system_admin_contact_code": 190005, // incorrect , this showed up correct on my side
      "decision_maker_contact_code": 157928, // incorrect, same here
      "systems": [
        {
          "code": "JVIL0001A",
          "build": "B33W",  // incorrect, same here
          "configured_nm4": "NO", // incorrect , this was flipped due to a bug
          "configured_karaoke": "YES", // incorrect
        }
      ]
    }
```

The claim was everything was fixed when he looked later for the system codes but not the config_nm4 and karaoke.

A further example was provided my Martin:
```json
  {
      "code": "WAXY03",
      "name": "Waxy's Irish Pub",
...
      "systems": [
        {
          "code": "WAXY03A",
          "status": "Active",
          "type": "HDS",
          "purchase_rental": "Rental",
          "build": "B33W",
          "location": "Bar",
          "juke_kiosk": "N/A",
          "configured_nm4": "YES",
          "configured_karaoke": "YES",
          "zones": [
            {
              "index": 1,
                …
          "equipment": [
            {
              "serial": "NMS7024",
              "type": "HDS",
              "spec3": "B27W/423",
               …

```

My API call for system for "WAXY03A":

```json
  "clients": [
                  {
                        "code": "WAXY03",
                        "name": "Waxy's Irish Pub",
                        "legal": "Invercargill Licensing Trust",
                        "type": "MONTH",

  "systems": [
                              {
                                    "code": "WAXY03A",
                                    "status": "Active",
                                    "type": "HDS",
                                    "purchase_rental": "Rental",
                                    "build": "B27W", <-- this is good
                                    "location": "Bar",
                                    "juke_kiosk": "N/A",
                                    "configured_nm4": "YES",
                                    "configured_karaoke": "YES"
                                    ...
                                }
```

The query that calls the configuration of the systems in the intranet code base:

```php
	function getSystemsConfigObject($systemCodesArray) {
		$MNM = new MonolithSql();
		$systemsList = "'" . implode ( "', '", $systemCodesArray) . "'";
		$onlineUpdates = $this->getConfiguredOnlineUpdates($systemCodesArray); //get the systems data on Online Updates
		$query = "SELECT * FROM hdmslive_rep.system_config
		WHERE system IN ($systemsList)
		AND (type LIKE 'zone_\_hardconf' OR type = 'system'
		OR (type LIKE 'registry_nl' AND `key` like '%ConnectedAdapterMACAddress%'))";
```

I created a query that looks at the system martin referenced in the last email:

```sql
        SELECT * FROM hdmslive_rep.system_config
		WHERE system="WAXY03A"
		AND (`key` LIKE "%NM4%" OR `key` LIKE "%KARAOKE%")
		AND (type LIKE 'zone_\_hardconf' OR type = 'system'
		OR (type LIKE 'registry_nl' AND `key` like '%ConnectedAdapterMACAddress%'));
```

And got the following result:
```text
    WAXY03A zone1_hardconf KARAOKE ENABLED YES
    WAXY03A zone1_hardconf NM4 ENABLED YES
```

This leads me to believe that the intranet could be the culprit rather then crowded-house since biggie smalls
is telling me karaoke is enabled.
