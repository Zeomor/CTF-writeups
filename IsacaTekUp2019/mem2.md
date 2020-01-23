This task uses the same memory file from the first task.

We're require to find what the rogue employee wrote before he deleted it.

At first i tried using the command "bioskbd" in volatility in hopes of getting a history of keystrokes:
volatility -f mem.dump --profile=Win7SP1x64 bioskbd
but there was no result.

Next i looked at the processes , maybe there was some sort of a keylogging software/malware or notepad open : 
volatility -f mem.dump --profile=Win7SP1x64 pslist
but there wasn't any suspecious/interesting process.

Finally i tried using strings and grepping what's in \AppData\Local\Temp :
strings mem.dump | grep -E "AppData.Local.Temp"
while inspecting the results i find a lot of files related to visual studio , and then 
... ,"rangeLength":0,"text":"ZmxhZ3t0aDFzXzFzX015X1MzY3lzdH0=","rangeOffset" ...
that was obviously a base64 encoded string 
echo "ZmxhZ3t0aDFzXzFzX015X1MzY3lzdH0=" | base64 -d 
--> flag{th1s_1s_My_S3cyst}    :D
( there was a typo , it was actually S3cr3t )
