# ODoH Benchmarks 

## 1. *benchmarks.go

One of the goals I set for myself was to successfully send ODoH requests, but also to be able to obtain performance measurement results, among other things, on this new protocol.

A simple ODoH command as I showed in the "README" document simply returns basic information such as the IP address of the domain name etc.
In the paper I studied on ODoH, the micro and macrobenchmarks were done with some of the code I used.
So I explored and tried to figure out this code to make measurements myself. 

In the file called *benchmarks*, there are some important parts in my opinion :  

### runningTime structure
<img width="310" alt="Capture d’écran 2021-06-14 à 17 55 32" src="https://user-images.githubusercontent.com/72855563/121922058-e690a080-cd39-11eb-978b-6df5cfe484db.png">

This runningTime structure contains the epoch timestamps for each of the operations taking place. The explanations are as follows:
1. Start => Epoch time at which the client starts to prepare the question
2. ClientQueryEncryptionTime => Epoch time at which the client completes the encryption and serialization of the question.
3. ClientUpstreamRequestTime => Epoch time indicating the start of the network request.
4. ClientDownstreamResponseTime => Epoch time indicating the receipt of the response and deserialization into ObliviousDNSMessage
5. EndTime => Epoch time indicating the end of all tasks for the request.

__*All timestamps are stored in NanoSecond granularity and need to be converted into microseconds (/1000.0) or milliseconds (/1000.0^2)*__

### experimentResult structure 

This structure defines the parameters which will be recorded and saved in an output file at .json format. 

<img width="589" alt="Capture d’écran 2021-06-14 à 17 58 38" src="https://user-images.githubusercontent.com/72855563/121922470-4c7d2800-cd3a-11eb-9dac-b6e19800abfd.png">

## 2. *commands.go

In this file, there are all the commands which the user could tape into the terminal. Each command has a particular usage. 

The command I focused on is this one : 

<img width="957" alt="Capture d’écran 2021-06-14 à 18 03 18" src="https://user-images.githubusercontent.com/72855563/121924876-9e26b200-cd3c-11eb-857d-8e5dbcd9e736.png">

The different parameters are the following : 

- data : this is a file which contains domain names. The default file is called "dataset.csv" but I couldn't find it and so edit it. That's why I created a new .csv file, which contains the 1500 first top domain names. 
- pick : this is the number of queries performed by the client instances during the measurements
- numclients : this is the number of client instances created by the function *benchmarkClient* 
- rate : the number of requests per minute uniformly distributed 
- logout : a file in .txt format in which all the steps about queries and answers are detailled (an exemple after)
- out : filename to save serialized JSON response from benchmark execution (eg. output.json).
- target : the ODoH target server
- proxy : the proxy server 
- dnstype : the record type of the requests (A, AAAA,...)

*__The function *benchmarkClient*, in the file *benchmarks* creates `--numclients` client instances performing `--pick` queries over `--rate` requests/minute uniformly distributed.__*

## 3. Using the bench command

For this example, I used the data file called *source.csv*, that I've put in the same folder as this file. I 
