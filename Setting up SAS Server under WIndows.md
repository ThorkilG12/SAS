# The setup - 2 SAS Servers - One File-Server - One Client #
2012 R2 Foundation - SAS Server TEST2012 - User Admin2012 - 192.168.1.212
2019 Essentials - SAS Server TEST2019 - User Admin2019 - 192.168.1.219
2019 Essentials - DNS and File Server - 192.168.1.252
Windows 11 - SAS ? 
## Initial preperation of the servers ##
Be sure that WIndows is not "holding" port 80/443  
Disable IP Ver 6  
Set 192.168.1.252 as primary DNS  
Allow Remote Controle (RDP)
## Install SAS ##
The two SAS Servers are installed by using a PLAN-file, and after a 100% successfull install the server boots up with these services running: 
<img width="592" alt="image" src="https://user-images.githubusercontent.com/12120277/202742705-886fea9e-ab6d-4cf9-85ce-f71f0b4fbc5e.png">  
SAS EG 8.3, SAS DM 9.4, SAS DI, SAS MC, SAS ODS Graphichs Editor
## Running programs direct on the server ##  
SAS DM - Display Manager  
```
NOTE: Copyright (c) 2016 by SAS Institute Inc., Cary, NC, USA.
NOTE: SAS (r) Proprietary Software 9.4 (TS1M7)
      Licensed to <company> - PARTNER - SERVER, Site <site-id>.
NOTE: This session is executing on the X64_SRV19  platform.
NOTE: Analytical products:
      SAS/STAT 15.2
NOTE: Additional host information:
 X64_SRV19 WIN 10.0.17763  Server
NOTE: SAS initialization used:
      real time           1.67 seconds
      cpu time            0.81 seconds
```
SAS MC - Management Console  
