-- -
Attacking/enumerating images
```bash
# basics
file <file>
strings <file>
exiftool <file>

# Then if the above don't seem to obviously hide data within the image
# you can use steghide to try to extract data from the file,
# EVEN IF both file and exiftool show it as a legitimate JPG/PNG/Whatever
steghide --extract -sf <file>
steghide --extract -sf trytofind.jpg
```
##### Installing tools
```bash
sudo pacman -S perl-image-exiftool
```