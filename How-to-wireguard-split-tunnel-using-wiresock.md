# How to wireguard split tunnel using wiresock
##### _Prerequisites: Wireguard._ 

&nbsp;

#### First step: Download and install Wiresock client
https://www.wireguard.com/install/

&nbsp;

#### Second step: Open the wireguard .conf file with a text editor
Add the following lines at the end of the [Peer] section:

```
AllowedApps = msedge.exe
DisallowedApps = chrome.exe
```
Specify wich programs you want to include or exclude, example: msedge.exe, chrome.exe

&nbsp;

You can check for additional parameters in the official wiresock website.

https://www.wiresock.net/wiresock-vpn-client/wiresock-vpn-client-advanced-configuration-parameters/

&nbsp;

#### To run wiresock as a windows service:

Open command prompt as administrator.

Paste the following command, MAKE SURE TO CHANGE THE PATH TO THE .CONF FILE.

```
wiresock-client.exe install -start-type 2 -config "C:\Users\User\Desktop\Wireguard.conf" -log-level none
```

&nbsp;

And finally to start the service, paste the following line in the command prompt:
```
sc start wiresock-client-service
```

Or you can open the Services.msc, find Wiresock and start.

&nbsp;

To stop the service using command prompt:
```
sc stop wiresock-client-service
```
To delete the service using command prompt (Make sure to stop before):
```
sc delete wiresock-client-service
```
