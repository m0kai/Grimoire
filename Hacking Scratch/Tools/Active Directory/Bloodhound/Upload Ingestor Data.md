-- -
After running [[bloodhound.py]] or SharpHound, we need to setup Bloodhound and upload the output JSON files to visualize the domain.
#### Setup
First, we need to start the neo4j database service:
```bash
sudo neo4j start
```
Then, we can consolidate the JSON files into a zip archive to upload the findings to bloodhound in one go, rather than uploading each file individually:
```bash
zip -r <filename>.zip *.json
```
#### Upload
Then just upload to the Bloodhound GUI as shown below:
![[Pasted image 20240607090602.png]]*Note: Your file will obviously be named differently, and be named to whatever you named the zip in the above command.*