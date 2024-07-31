-- -
Hidden data. For example, when you cat out a file that would be the primary data stream. Someone can hide an alternate data stream for a file so that it holds data that is hidden as it is not part of the primary data stream. You can find a deeper explanation [here](https://www.malwarebytes.com/blog/101/2015/07/introduction-to-alternate-data-streams)

#### Get alternate data stream data
```powershell
# list out pwd including alternate data streams for each file
dir /R

# if you find an alternate data stream, data could be hidden
# in this example, the file in questions is:
# hm.txt
# and the alternate data stream is:
# hm.txt:root.txt:$DLATA
# to see what's in the alternate data stream:
more < hm.txt:root.txt:$DATA

# note that other ways to reveal the data are outlined in the deeper explanation link above. 
```