-- -
For situations where you are on a Windows only network that has no SSH or linux server anywhere. 

This page is a bit different in terminology, and given how easily confused pivoting becomes, I feel the need to explain the workflow. Assume you have gotten a foothold on a windows 10 system. 
Attackbox (kali) -> Windows foothold -> Windows Pivot Host -> Internal Target
The steps here will only be on the Windows foothold and Windows Pivot host and result in being able to connect to the internal host. 
### Process
1. Download the following binaries to attack box:
	- [Proxifier](https://www.proxifier.com/download/#win-tab) Get the ProxifierPE.zip 
	- [SocksOverRDP](https://github.com/nccgroup/SocksOverRDP/releases)
2. Then [[Dark Arts I/File Transfer/~Home|File Transfer]] `SocksOverRDPx64.zip` (or whichever architecture you chose) to the Windows foothold.
3. Load SocksOverRDP.dll on Windows foothold
```powershell
regsvr32.exe SocksOverRDP-Plugin.dll
```
4. Next, [[Dark Arts I/File Transfer/Windows|File Transfer]] `SocksOverRDP.zip` or only the `SocksOverRDP-Server.exe` to Windows Pivot Host. 
5. Once on the Windows Pivot Host, run `SocksOverRDP-Server.exe` with admin privileges
6. On Windows Foothold, use netstat to check if the listener is up, it should have a TCP connection LISTENING on `127.0.0.1:1080`
```powershell
netstat -antb | gindstr 1080
```
7. [[Dark Arts I/File Transfer/Windows|File Transfer]] proxifier portable to Windows Pivot Host
8. Configure proxifier on Windows Pivot Host, run Proxifier Portable -> Profile -> Proxy Servers -> Add -> Address: 127.0.0.1 Port: 1080 -> Ok
9. RDP to Internal Target