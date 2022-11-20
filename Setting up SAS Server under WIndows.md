# The setup - 2 SAS Servers - One File-Server - One Client #
2012 R2 Foundation - SAS Server TEST2012 - User Admin2012 - 192.168.1.212  
2019 Essentials - SAS Server TEST2019 - User Admin2019 - 192.168.1.219  
2019 Essentials - DNS and File Server - 192.168.1.252  
Windows 11 - SAS Foundation => SAS EG, SAS DM and SAS Studio
## Initial preperation of the servers and PC##
Be sure that WIndows is not "holding" port 80/443  
Disable IP Ver 6  
Set 192.168.1.252 as primary DNS  
Allow Remote Controle (RDP)
## Install SAS ##
The two SAS Servers are installed by using a PLAN-file, and after a 100% successfull install the server boots up with these services running: 
<img width="592" alt="image" src="https://user-images.githubusercontent.com/12120277/202742705-886fea9e-ab6d-4cf9-85ce-f71f0b4fbc5e.png">  
SAS EG 8.3, SAS DM 9.4, SAS DI, SAS MC, SAS ODS Graphichs Editor  
On server goto folder `C:\Program Files\SASHome\SASFoundation\9.4\core\sashelp` and copy the file `class.sas7bdat`. Rename the copy to `_Test2019Class.sas7bdat`  
This shows the clients in this test what server they look at.
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
Using SAS Integration Tech. Config Wizard
C:\Program Files\SASHome\SASFoundation\9.4\core\sashelp
## Running SAS EG from client ##  
The services Metadata, port 8561 and Object Spawner, port 8581 must be started on server  
The server firewall must be open for TCP port 8561 and 8591  
A look in SAS MC Server Manager shows that SASAPP - Workspace Server uses port 8591, and that explains why that port has to be open in firewall  
User Starts SAS EG that connects to Metadat on port 8561. When user try to browse librarys on server, metadata service talks to spawner to start a workspace server for the user, using port 8591
## Running SAS DM on client - using the server ##  

## PC with Foundation vs. PC with SAS EG only ##
It is important to understand, that when you install Foundation on a PC, then this PC will have it's own *sas.exe* and a licence.  
It means that you can run SAS EG on your PC and that SAS Studio also can run on your laptop  
<img width="953" alt="image" src="https://user-images.githubusercontent.com/12120277/202843931-037a83e6-2dc8-4ef6-b249-61798be664a2.png">

### Using the browser ###

## Server admin ##
<img width="307" alt="image" src="https://user-images.githubusercontent.com/12120277/202843644-4e67630d-a405-42a5-85b0-2d7e3a006131.png">

On the PC where I have installed only SAS EG and SAS Studio (no Foundation) I have an error `Failed to load SAS Studio Tasks`
Is this about two different products ? SAS Studio and SAS Visual Studio ?
This was part of the installation:  
<img width="221" alt="image" src="https://user-images.githubusercontent.com/12120277/202849235-f0c080ad-6c96-4a52-b4a8-421f04dc4aaa.png">

In order to use SAS Visual Analytics both as an Admin and as a user, it the ONLY app a browser ?






