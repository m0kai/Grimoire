-- -
### Basic Usage
```bash
nmap 10.10.10.10 -sC # default scripts
nmap 10.10.10.10 --script <script> # specify script
nmap 10.10.10.10 --script <script>,<script> # specify multiple scripts

# aggressive scan
# Does:
# -sV: version
# -O: OS detection
# --traceroute
# -sC: default scripts
nmap 10.10.10.10 -A

# vulnerability assesment
# For HTTP vulns only it seems
nmap -p 80 10.10.10.10 --script vuln
```