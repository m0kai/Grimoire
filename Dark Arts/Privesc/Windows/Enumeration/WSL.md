-- -
Windows Subsystem for Linux, you know what this is. 
#### Find executables
```powershell
# you obviously can try to do the root C:\ or in the program files or whereever
where /R C:\windows bash.exe # bash executable
where /R C:\windows wsl.exe # wsl executable
```
#### Run commands
```powershell
# obviously, you can supply the full or relative path to it, and may need to. 
wsl.exe whoami
```
[[Dark Arts/Privesc/Windows/Exploits/WSL|Exploit]]
