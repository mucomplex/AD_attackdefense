# Disable Protection <br>
## WinDefend<br>
sc stop WinDefend<br>
## Firewall <br>
NetSh Advfirewall set allprofiles state off <br>
## Symantec <br>
smc -stop <br>
smc -stop -p password <br>
#### Symantec firewall <br>
smc -disable –ntp <br>
smc -disable –ntp -p password<br>
# Enable Protection <br>
## WinDefend <br>
sc start WinDefend <br>
## Firewall <br>
NetSh Advfirewall set allprofiles state on <br>
## Symantec <br>
smc -start <br>
smc -start -p password<br>
#### Symantec firewall <br>
smc -enable -ntp <br>
smc -enable -ntp -p password <br>
# Status Protection <br>
## WinDefend <br>
sc query WinDefend <br>
## Firewall <br>
Netsh Advfirewall show allprofiles <br>
<br>
## Resources <br>
https://www.windows-commandline.com/enable-disable-firewall-command-line/ <br>

