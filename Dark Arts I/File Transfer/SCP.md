- --
Think of it as `cp` over `ssh`
### Upload
```bash
# copy local file to remote host
scp <file> <user>@<target ip>:<path to upload>
scp reverse.exe ubuntu@10.10.10.10:~/
```
### Download
```bash
# copy remote file to local machine
scp <user>@<target ip>:<file path> <local path> 
scp ubuntu@10.10.10.10:/home/ubuntu/local.txt .
```
### Transfer Directory
```bash
# -r: recursive I'm assuming

# upload
scp -r <dir> <user>@<targetip>:<path>
scp -r rpivot ubutnu@10.10.10.10:/home/ubuntu
```
HTB{PeopleReuse_PWsEverywhere!}