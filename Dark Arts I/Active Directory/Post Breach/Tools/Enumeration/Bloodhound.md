-- -
Tool for visualizing AD as a mindmap or web and from a variety of different contexts. Excels at displaying complex attack paths that would be very difficult to come up with without this tool. 
### Setup
```bash
# can also do with pip, but may only need to: pip install bloodhound
sudo apt install bloodhound bloodhound.py
neo4j console

# this will give you a port to connect to via browser, setup and create an admin account. You need to remember the password so write it down or make it stupid. 
```
### Run Ingestor
```bash
# from linux attackbox
# -ns: nameserver, probably the DC but potentially a different server? maybe? 
sudo bloodhound.py -d <domain> -u <username> -p <password> -ns <dc ip> -c all
```