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
### Start Bloodhound Session
```bash
# for when its installed and you want to open bloodhound again or its installed and you are starting a new session
sudo neo4j start
bloodhound
```
### Combine Json Output files into one
You can upload the json files the ingestor outputs individually or combine them as a zip file, and upload that so everything is ingested in one go:
```bash
 zip -r [zip name].zip *.json
```
![[Pasted image 20250115072707.png]]
### Cypher Queries
You can query the data in bloodhound using Cypher language queries. A cheatsheet can be found [here](https://hausec.com/2019/09/09/bloodhound-cypher-cheatsheet/)