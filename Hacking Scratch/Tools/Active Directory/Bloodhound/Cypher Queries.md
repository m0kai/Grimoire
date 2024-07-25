-- -
Query language used by bloodhound to enumerate data, get oriented to the domain or, more usefully, get attack paths to Domain Admin. You can find custom queries to run in the `Raw Query` box at the bottom of the Bloodhound GUI [here](https://hausec.com/2019/09/09/bloodhound-cypher-cheatsheet/)
#### Builtin Queries
Click on `Analysis` tab. 
- `Find Computers with Unsupported Operating Systems`: Find outdated and unsupported operating systems running legacy software. Easy way to find old/easy vulnerabilities on the network. 
- `Find Computers where Domain Users are Local Admin`: Find computers where any domain user has local admin rights, meaning given valid credentials, you have local admin. 
### Raw Queries
#### Enumerate WinRM Access
```cypher
MATCH p1=shortestPath((u1:User)-[r1:MemberOf*1..]->(g1:Group)) MATCH p2=(u1)-[:CanPSRemote*1..]->(c:Computer) RETURN p2
```

^293840

#### Enumerate SQL Admin Rights
```cypher
MATCH p1=shortestPath((u1:User)-[r1:MemberOf*1..]->(g1:Group)) MATCH p2=(u1)-[:SQLAdmin*1..]->(c:Computer) RETURN p2
```

^60f753
