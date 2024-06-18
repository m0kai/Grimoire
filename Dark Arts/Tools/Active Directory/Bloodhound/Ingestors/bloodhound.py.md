-- -
Python-based Linux Ingestor. Using a valid Domain user, ingests data about AD that you can import into BloodHound to visualize the domain as well as get complex (or simple) attack paths for said domain. 
#### Collect all
```bash
# note: this is noisy and just running this/Bloodhound will likely set off alarms
sudo bloodhound-python -u '<user>' -p '<passwd>' -ns <ns/dc ip> -d <domain> -c all 
```