-- -
Basically, you setup [[Responder]] and wait for DNS to fail so that a system calls out asking for an unknown host. Responder replies as the unknown host, then gives you the hash it acquires from the response. 

For mitigation steps, go [[Poisoning Attacks|here]]
#### From Linux
![[Responder#^92af1e]]
#### From Windows
**Inveigh (Depricated)**
Inveigh written in PowerShell, which no longer has support. 
![[Inveigh#^72b71f]]
**Inveigh Zero**
![[Inveigh#^675aa5]]