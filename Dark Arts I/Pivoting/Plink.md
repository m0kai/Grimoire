-- -
PuTTY Link, bundled with PuTTY, so a way to live-off-the-land and use "built-in" tools to achieve pivoting. Generally leverages a Windows attack host. 
#### Dynamic Port forward
Setup a pivot over a specific port that you can funnel your traffic through. Should let you use whatever service or tools you want through that listener port. 
```powershell
plink -ssh -D <listener port> <user>@<pivot target>
plink -ssh -D 9050 ubuntu@10.129.15.50
```