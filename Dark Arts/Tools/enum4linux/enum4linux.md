-- -
### Under the hood
enum4linux is in essence a wrapper script that uses other common Samba tools to gather information for you. Below is a list of **some** of the enumeration tools and corresponding ports used by enum4linux.
- nmblookup    137/UDP
- nbtstat 	       137/UDP
- net 	               139/TCP, 135/TCP, TCP and UDP 135 and 49152-65535
- rpcclient 	135/TCP
- smbclient 	445/TCP
### General Usage
![[Dark Arts/Active Directory/Initial Breach/Enum/Password Policy#^5028a6|Password Policy]]
