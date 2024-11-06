-- -
Python tool for getting OSINT info such as SSL certificate checking, whois, header analysis and crawling.
### Install
```bash
# via pip
git clone https://github.com/thewhiteh4t/FinalRecon.git
cd FInalRecon
pip3 install -r requirements.txt
chmod +x finalrecon.py
./finalrecon.py --help

# apt (kali)
sudo apt install finalrecon
```
### Usage
```bash
# Useful Flags:
# --url: target
# --headers
# --sslinfo
# --whois
# --crawl
# --dns
# --sub: enum subdomains
# --dir
# --wayback
# --ps: Fast Port Scan
# --full: Do everything
./finalrecon.py --headers --whois --url http://inlanefreight.com
```