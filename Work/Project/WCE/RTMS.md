#### Configurations

```json
"Database": {
    "AppDb" : [
      {
        "Name" : "SIPDB", // change to db name
        "Server" : "172.17.0.35\\sqlexpress", // change to host/ip address of db
        "Database": "SIPDB", // change to db name
        "User": "admin", // credential of db
        "Password": "admin", // credential of db
        "TrustedConnection": true // do not change
      }
    ]
  },
  "RtmsEchoConfiguration": {
    "Username": "admin", 
    // credential of radar. all radar that registered to the index of the service **MUST** share the same credential
    "Password": "12345678", 
    // same as above
    "FetchIntervalDataIntervalInMinute": 5, 
    // only change once after service is deployed
    // **DO NOT CHANGE** after service already run once
    // unless needed, delete all data first. raw, 15min etc 
    "PostDataWCFIntervalInSeconds": 20, 
    // Interval for updating the status of tmcs for latest traffic data and map display data
    "Enable5MinProcess": false, 
    // ignore all these config unless needed. should be all true except 5min
    "Enable15MinProcess": true,
    "EnableHourlyProcess": true,
    "EnableDailyProcess": true,
    "EnablePeakMorningProcess": true,
    "EnablePeakEveningProcess": true,
    "EnablePeakOffProcess": true,
    "EnableMonthlyProcess": true,
    "EnableYearlyProcess": true,
    // For all config below here except distance
    // **DO NOT CHANGE** after the service already run once
    // unless needed, delete all data first. raw, 15 min etc
    "MorningPeakStartHour": 6, 
    // timing set for start of morning peak(24h format)
    "MorningPeakStartMinute": 30, 
    // timing in minutes for start of morning peak
    "MorningPeakEndHour": 10, 
    // timing set for end of morning peak(24h format)
    "MorningPeakEndMinute": 0,
    // timing in minutes for end of morning peak
    "EveningPeakStartHour": 17,
    // timing set for start of evening peak(24h format)
    "EveningPeakStartMinute": 0,
    // timing in minutes for start of evening peak
    "EveningPeakEndHour": 20,
    // timing set for end of evening peak(24h format)
    "EveningPeakEndMinute": 0,
    // timing in minutes for end of morning peak
    "DistanceInKilometer": 1 // *DO NOT CHANGE* this config
  },
  "TmcsConfiguration": {
    "Protocol": "http", // *DO NOT CHANGE*
    "IpAddress": "localhost", // tmcs endpoint host address
    "Port": 65319, // tmcs endpoint port
    "PingerIntervalInSeconds": 30 , // interval to ping the status of radar, log network changes and send radar network status to tmcs
    "TrafficStatisticEndpoint": "/api/Traffic/update-traffic-data", // *DO NOT CHANGE UNLESS TMCS UPDATE*
    "PingerEndpoint": "/api/Traffic/vids-pinger" // *DO NOT CHANGE UNLESS TMCS UPDATE*
  },
  "GatewayIndex":  3 // Identifier for service to read VIDS in db. all vids with this index will be process by this service
```

#### Deployment setup

Environment (Prerequisite)
- Windows OS
- [Net Core 6 Runtime](https://dotnet.microsoft.com/en-us/download/dotnet/6.0/runtime?cid=getdotnetcore&os=windows&arch=x64)
- Internet Information Services (IIS) with [Web Deploy](https://www.iis.net/downloads/microsoft/web-deploy) enabled (either install of enable in add/remove features in Windows control panel)
- MSSQL database

Monitoring (Debugging)
- Log2Console

Deployment
- .zip file (ask from Software Engineer to publish the .zip file by portable package of IIS)

1. Create new site in IIS
2. Import the .zip file
3. Open application pool and find the services name
4. Right click and open `Advanced Settings...`
5. In **General** tab, click `Start Mode` and set it to `AlwaysRunning`
6. In **Something** tab, change the value to 0
7. Restart the application pool
8. Configure the configuration on site carefully as it will determine future calculations and logical process
9. Start the RTMS VIDS Service(stop and start if already running)

#### Encountered error

1. If `Http Error 500.19`[^1] after deploying that is because the Net Core 6 Runtime is not installed on the server. Refer environment 2.
2. Registered detector zone **must** be according to radar information given(must be in number). Failure to convert to number will cause major changes to software

#### Data Deletion

In case data is corrupted or not as expected, use this SQL script to clear all data and restart the service to track the issue. Irreversible action and should be used carefully. Understand the script before usage

```sql
DELETE
FROM [WCE_TMCS_S5_v3.19.8.1].[dbo].[traffic_statistics_raw]
--FROM [WCE_TMCS_S5_v3.19.8.1].[dbo].[traffic_statistics_15min]
--FROM [WCE_TMCS_S5_v3.19.8.1].[dbo].[traffic_statistics_hourly]
--FROM [WCE_TMCS_S5_v3.19.8.1].[dbo].[traffic_statistics_daily]
--FROM [WCE_TMCS_S5_v3.19.8.1].[dbo].[traffic_statistics_monthly]
--FROM [WCE_TMCS_S5_v3.19.8.1].[dbo].[traffic_statistics_yearly]
--FROM [WCE_TMCS_S5_v3.19.8.1].[dbo].[traffic_statistics_peak_morning]
--FROM [WCE_TMCS_S5_v3.19.8.1].[dbo].[traffic_statistics_peak_evening]
--FROM [WCE_TMCS_S5_v3.19.8.1].[dbo].[traffic_statistics_peak_off]
WHERE vids_id='VIDS_22_NB' -- change to each vids registered and change table above
```

---

[^1]: [asp.net - IIS HTTP Error 500.19 - Stack Overflow](https://stackoverflow.com/questions/11305821/iis-http-error-500-19)