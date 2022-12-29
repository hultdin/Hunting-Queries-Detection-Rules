# Abuse.ch Botnet C2 IP Blacklist to detect external C2 connections

#### Source: Abuse.ch
#### Feed link: https://sslbl.abuse.ch/blacklist/sslipblacklist.txt

### Defender For Endpoint
```
let ThreatIntelFeed = externaldata(DestIP: string)[@"https://sslbl.abuse.ch/blacklist/sslipblacklist.txt"] with (format="txt", ignoreFirstRecord=True);
let IPRegex = '[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}';
let MaliciousIP = materialize (
     ThreatIntelFeed
     | where DestIP matches regex IPRegex
     | distinct DestIP
     );
DeviceNetworkEvents
| where RemoteIP in (MaliciousIP)
```


### Sentinel
```
let ThreatIntelFeed = externaldata(DestIP: string)[@"https://sslbl.abuse.ch/blacklist/sslipblacklist.txt"] with (format="txt", ignoreFirstRecord=True);
let IPRegex = '[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}';
let MaliciousIP = materialize (
     ThreatIntelFeed
     | where DestIP matches regex IPRegex
     | distinct DestIP
     );
DeviceNetworkEvents
| where RemoteIP in (MaliciousIP)
```
