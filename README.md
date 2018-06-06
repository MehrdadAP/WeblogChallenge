# WeblogChallenge  
This is my solution for PaytmLabs Weblog Challenge.
You can find the detailed description of the challenge in challenge_description.md

## Tools
* Framework: Apache Spark
* Language: Scala
* Build Tool: SBT
* IDE: IntelliJ IDEA


## How to Run
Simply run run.sh and provide the path to the data file as argument.  
For efficiency purpose, if the input file is compressed in gz (i.e. ends with .gz), 
it will be uncompressed before passing to Spark job.

## Discussion
In this challenge, we are dealing with webserver log data which specifically coming from 
AWS (more information [here](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/access-log-collection.html#access-log-entry-format)). 
A core part of the solution is to sessionize users.  
In my solution, I've taken time-oriented approach to sessionize clients, i.e. for each user, 
if there is no request for X minutes, we assume user has terminated the session.
In the solution X has been set to 15 minutes. 
This number plays a crucial role in defning a session and can change all other calculations.  

Based on the challenge description, IP addresses do not guarantee distinct users. 
Therefore, in the solution, client ip, port and browser information have been used to make a better assumption of a distinct user.

 
## Result
* average duration of all sessions: 563.11 seconds
* most engaged user:   
user_ip_port: 103.29.159.138:57045  
user_agent: Mozilla/5.0 (Windows NT 6.1; rv:21.0) Gecko/20100101 Firefox/21.0  
Session time: 3007 seconds  

* result of number of unique urls visited per session is also provided in the solution but it's too huge to be provided here.