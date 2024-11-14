-- -
Scrapes web app for words and outputs a list
```bash
# -d: depth of spider, so 4 links deep
# -m: minimum word length, only include words of 6 letters or higher
# --lowercase: save results in all lowercase
# -w: output results to file called inalne.wordlist
cewl https://www.inlanefreight.com -d 4 -m 6 --lowercase -w inlane.wordlist
```