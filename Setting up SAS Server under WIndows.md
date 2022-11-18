# The setup - 2 SAS Servers - One File-Server - One Client #
2012 R2 Foundation - SAS Server TEST2012 - User Admin2012 - 192.168.1.212  
2019 Essentials - SAS Server TEST2019 - User Admin2019 - 192.168.1.219  
2019 Essentials - DNS and File Server - 192.168.1.252  
Windows 11 - SAS Foundation => SAS EG, SAS DM and SAS Studio
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
### SAS DM - Display Manager ###  
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
### SAS MC - Management Console - The Admin User ###  
<img width="181" alt="image" src="https://user-images.githubusercontent.com/12120277/202748172-fd11ca80-5afc-4236-b8b1-4c9fce81691e.png">
The DBMSOwner is the password for the PostgreSQL server that has been installed by the SAS Installation Process.  
<img width="290" alt="image" src="https://user-images.githubusercontent.com/12120277/202748835-a503e1ea-9522-43c2-8255-da8ce116ce80.png">  

### SAS EG - Enterprise Guide ###  
<img width="414" alt="image" src="https://user-images.githubusercontent.com/12120277/202750935-115af8d1-14cc-448d-9009-6ec7d4d3e248.png">
Default placement of the WORK folder, and the relation to the windows process that is part of the temp folder
<img width="640" alt="image" src="https://user-images.githubusercontent.com/12120277/202751788-d0f93337-3b9b-4b74-b826-3a5c28b04d71.png">

### SAS Foundation - With SAS CONNECT ###
Using SAS Integration Tech. COnfig Wizard
## Running SAS EG from client ##  

The services Metadata, port 8561 and Object Spawner, port 8581 must be started on server  
The server firewall must be open for TCP port 8561 and 8591  
A look in SAS MC Server Manager shows that SASAPP - Workspace Server uses port 8591, and that explains why that port has to be open in firewall  
User Starts SAS EG that connects to Metadat on port 8561. When user try to browse librarys on server, metadata service talks to spawner to start a workspace server for the user, using port 8591

