-- -
A basic break in virtualization, when the spidey senses tingle when you see the docker group, keypoint isn't that docker is installed but that your current user is a part of the Docker group.
```bash
# run an id to see your group memebership
id

# should see something like
# 116(docker)
```
Easy exploit is to go to [GTFOBins](https://gtfobins.github.io/gtfobins/docker/)
Otherwise, go to my [[Dark Arts/Privesc/Linux/Exploits/Docker|Exploit Notes]]
