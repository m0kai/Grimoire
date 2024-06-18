-- -
This is for those annoying situations where the CTF gives you large amounts of text and you know you need to sift through it with a fine toothed comb to find some hidden credentials
```bash
# this will pull all the text from a webpage and output each unique word so you can find that one string that is obviously an encoded string or credentials or something like that
curl http://<ip or host>/<uri> | grep -oE '\w+' | sort -u -f | more
curl http://10.0.2.62/iamGaara | grep -oE '\w+' | sort -u -f | more
```