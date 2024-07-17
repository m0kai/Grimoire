-- -
Security auditing software for #AD. It gives an overall report on the domain which points out security gaps, which you can use as an attacker to identify attack paths based on the gaps identified by the tool. It also finds cleartext credentials if available, such as cleartext credentials "hidden" in the domain user description field. 
Of note, it seems to only run on windows, so you would need to put it on a compromised windows host, or a windows VM you control that can interact with #AD.
You just need to download the tool from [here](https://www.pingcastle.com), download the zip which will have the executable in it, then run as administrator. 
You can run from CLI and you can run it from a host that isn't necessarily domain joined. 