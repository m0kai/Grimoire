-- -
Bloodhound Ingestor.  Runs on #Windows. Gathers AD info using a host on the internal network or from a domain joined host and outputs data as a ZIP file that, presumably, is made up of JSON files that you will upload to Bloodhound.
### Basic Usage
```bash
SharpHound.exe -c All --sipfilename [output file]
.\SharpHound.exe -c All --zipfilename ILFREIGHT
```