-- -
Mitre ATT&CK T1557.001: Adversary-in-the-middle: LLMBR/NBT-NS Poisoning and SMB Relay.

**Mitigation:** Disable LLMBR and NBT-NS in the environment.

**Notes of Caution:** Disabling of this feature **should not** be done all at once, it should be rolled out slowly and carefully before a full environment rollout is attempted. Lost of testing to the effects it will have on the environment as it can break plenty of unintended things.

**Detection**: It may not always be possible to fully disable these features, in which case you will need to setup IDS/IPS systems for detecting and blocking specific traffic in relation to poisoning of this feature. One simple way of doing this is to have LLMNR and NBT-NS requests constantly go out for non-existent hosts, and if a response is given for these non-existent hosts, then it's indicative of an adversary's existence on your network. Basically honey pot them with fake hosts. This [blog post](https://www.praetorian.com/blog/a-simple-and-effective-way-to-detect-broadcast-name-resolution-poisoning-bnrp/) explains better. 

We can also monitor for traffic on UDP ports 5355 and 137, event IDs 4697 and 7045, and the registry key `HKLM\Software\Policies\Microsoft\Windows NT\DNSClient` for changes to the `EnableMulticast` DWORD value, 0 meaning disabled. 
##### Steps: 
- LLMNR can be disable in Group Policy:
	- Computer Configuration -> Administrative Templates -> Network -> DNS Client -> Turn OFF multicast Name Resolution
- NBT-NS cannot be disabled by group policy, instead it must be disabled on each host manually or using a powershell script:
	- Manual:
		- Open `Control Panel` -> Open `Network and Sharing Center `-> Click on `Change adapter settings` -> right-click on the `adapter `to view its properties -> Select `Internet Protocol Version 4 (TCP/IPv4) `-> Click `Properties` -> `Advanced` -> Select `WINS` tab -> Select `Disable NetBIOS over TCP/IP.` 
	- Powershell Script:
		- To propagate this script through the network, you will need to put the script in the `/SYSVOL` directory in a DC so every host can access it, then set a GPO that runs it from the `SYSVOL` location. 
		- Set a locations such as `\\INLANEGREIGHT.LOCAL\SYSVOL\scripts\disable_nbt.ps1`
		- In the `Group Policy Management Editor`: Set the script location in: `Computer Configuration` -> `Policies` -> `Windows Settings` -> `Scripts (Startup/Shutdown` -> `Startup`
		- Script:
		```powershell
		$regkey = "HKLM:SYSTEM\CurrentControlSet\services\NetBT\Parameters\Interfaces"
		Get-ChildItem $regkey |foreach { Set-ItemProperty -Path "$regkey\$($_.pschildname)" -Name NetbiosOptions -Value 2 -Verbose}
		```