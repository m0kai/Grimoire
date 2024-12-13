-- -
### Executables
-- -
##### winPEAS.exe
[Repo](https://github.com/peass-ng/PEASS-ng/tree/master/winPEAS)
Requires Net.4 to run. They provide a .bat file for situations where Net.4 is not available.
[[Dark Arts I/File Transfer/~Home|File Transfer]] to target:
```powershell
# cd to location of executable
winPEAS.exe
```
##### Seatbelt.exe
[Repo](https://github.com/GhostPack/Seatbelt)
##### Watson.exe
[Repo](https://github.com/rasta-mouse/Watson)
Updated version of Sherlock. 
##### SharpUp.exe
[Repo](https://github.com/GhostPack/SharpUp)
### PowerShell Scripts
-- -
##### Sherlock.ps1 (deprecated)
[Repo](https://github.com/rasta-mouse/Sherlock)
##### PowerUp.ps1
[Repo](https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc)
##### jaws-enum.ps1
[Repo](https://github.com/411Hall/JAWS)
### Misc
-- -
##### windows-exploit-suggester.py
[Repo](https://github.com/AonCyberLabs/Windows-Exploit-Suggester)
```bash
# run systeminfo on targetbox via cmd shell
systeminfo

# copy+paste into file on attackbox, call it ~/systeminfo.txt

# on attack box
# install dependencies
pip install xlrd --upgrade

# update db, will output save file location, in our example ~/2020-04-17-mssb.xls
./windows-exploit-suggester.py --update

# run w/ db file and systeminfo file
./windows-exploit-suggester.py --database <db file> --systeminfo <systeminfo file>
./windows-exploit-suggester.py --database ~/2020-04-17-mssb.xls --systeminfo ~/systeminfo.txt
```

^6bd9e9

##### Exploit Suggester (metasploit)
[Manual](https://www.rapid7.com/blog/post/2015/08/11/metasploit-local-exploit-suggester-do-less-get-more/)
```bash
# from a meterpreter shell
run post/multi/recon/local_exploit_suggester
```

^056912
