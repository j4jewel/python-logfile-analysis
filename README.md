# Log file Analysis using Python
You can use simple python codes to organize and analyze your log files like access_log. Here I am using logparser module Check [link](https://github.com/j4jewel/python-logparser)  for creating the logparser module. We can easily analyze access_log file in accordance with required conditions.

# Logparser Module

Logparser module parses a log file in to a proper dictionary, arranged in a systematic manner

Copy the logparser.py file to your current working directory for using the logparser module.

 Python code for listing the number of hits per IP

This code will list the number of hits per IP.

```sh
import logparser

logfile = "/root/jewel/python/access_log"

ipcounter = {}

with open(logfile,"r") as fh:
    
    for logline in fh:
        
        ip = logparser.parser(logline)["host"]
        
        if ip not in ipcounter:
            
            ipcounter[ip] = 1
        
        else:
            
            ipcounter[ip] = ipcounter[ip] + 1
            
for ip in ipcounter:
    hit = ipcounter[ip]
    print('{:20}:{}'.format(ip,hit))
```

##### Output 
```sh
185.39.146.215      :2229
140.143.183.24      :3319
76.164.234.170      :2519
76.72.167.154       :1228
23.111.152.74       :2228
46.246.122.10       :3581
81.17.62.205        :2585
185.173.35.49       :5210
```
### Finding the IPs per a given number of hit
We can find the IPs from which we recieved more hits on the basis of a given value. 

We just need to edit the last for loop of the above code. The last part is given below
```sh
for ip in ipcounter:
    hit = ipcounter[ip]
    if hit >2500:
        print('{:20}:{}'.format(ip,hit))
```
The output of above code will only prints IPs of Hit 2500+

## Python code for listing the hits per day

This code will list the number of hits per day
```sh
import logparser

datecounter = {}

logfile = "/root/jewel/python/access_log"

with open(logfile, "r") as fh:
    
    for logline in fh:
        
        date = logparser.parser(logline)["time"][0:11]
        
        if date not in datecounter:
            
            datecounter[date] = 1
        
        else:
            
            datecounter[date] = datecounter[date] + 1

for time in datecounter:
    hit = datecounter[time]
    print('Date: {:10} Hits: {}'.format(time,hit))
```
##### Output
```sh
Date: 01/Apr/2019 Hits: 3970
Date: 02/Apr/2019 Hits: 16271
Date: 03/Apr/2019 Hits: 12595
Date: 04/Apr/2019 Hits: 7897
Date: 05/Apr/2019 Hits: 8589
Date: 06/Apr/2019 Hits: 13769
Date: 07/Apr/2019 Hits: 19136
Date: 08/Apr/2019 Hits: 10676
Date: 09/Apr/2019 Hits: 11865
Date: 10/Apr/2019 Hits: 11486
Date: 11/Apr/2019 Hits: 17418
```

You can customize the code to find the IPs on the basis of error codes, or number of hits from agent like Mozilla , according to your requirement.
