-- -
Scans a domain for SMB shares then scans each share on each host it finds for files and file contents.
### Basic Usage
```powershell
# -d: domain
# -s: Print results to stdout
# -o: output file to write results to
# -v: verbosity
# data: only display results to screen, no errors
snaffler.exe -s -d [domain] -o [output file] -v data
Snaffler.exe -s -d inlanefreight.local -o snaffler.log -v data
```