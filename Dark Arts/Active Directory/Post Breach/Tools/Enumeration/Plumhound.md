-- -
Companion program that displays domain data in a web context. similar output to [[ldapdomaindump]]. The repo can be found [here](https://github.com/PlumHound/PlumHound).
### Setup
Make sure you started [[Bloodhound]] and ingested the domain data into it, then you can set this up. 
```bash
# Install tool into virtual environment
git clone https://github.com/PlumHound/PlumHound.git
cd PlumHound
python -m venv .venv
source .venv/bin/activate
pip install -r requirements

# install tool globally
cd /opt 
sudo git clone https://github.com/PlumHound/PlumHound.git
cd PlumHound
pip install -r requirements

# Establish connection w/ Bloodhound
sudo python3 PlumHound.py --easy -p <neo4j password>

# Basic ingestion/reporting
sudo python3 PlumHound.py -x tasks/default.tasks -p <neo4j password>
```