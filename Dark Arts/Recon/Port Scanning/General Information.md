---

---
-- -
General information about #nmap and its output. Here for quick reminders of the output you are seeing spit out by nmap.
### Port Status Info
| **State**          | **Description**                                                                                                                                                                                         |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `open`             | This indicates that the connection to the scanned port has been established. These connections can be **TCP connections**, **UDP datagrams** as well as **SCTP associations**.                          |
| `closed`           | When the port is shown as closed, the TCP protocol indicates that the packet we received back contains an `RST` flag. This scanning method can also be used to determine if our target is alive or not. |
| `filtered`         | Nmap cannot correctly identify whether the scanned port is open or closed because either no response is returned from the target for the port or we get an error code from the target.                  |
| `unfiltered`       | This state of a port only occurs during the **TCP-ACK** scan and means that the port is accessible, but it cannot be determined whether it is open or closed.                                           |
| `open\|filtered`   | If we do not get a response for a specific port, `Nmap` will set it to that state. This indicates that a firewall or packet filter may protect the port.                                                |
| `closed\|filtered` | This state only occurs in the **IP ID idle** scans and indicates that it was impossible to determine if the scanned port is closed or filtered by a firewall.                                           |
### SYN Scan vs Connect Scan
- `-sS`: SYN Scan
	- Partial TCP 3-way handshake
	- Used to be stealthier, but now will give you away to IDS or IPS
	- **Faster**
- `-sT`: Connect Scan
	- Full TCP 3-way handshake is performed
	- Most accurate way to determine the state of a port
	- Mostly stealthy as it does a full handshake
	- Useful when you want to map a network w/o disturbing the underlying service on said port. 
	- Minimal impact, considered a more polite scan method
	- Bypasses firewalls that block incoming connections, but allows outgoing connections
	- **Slower**