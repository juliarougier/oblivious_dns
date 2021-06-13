# Issues with the ODoH requests/codes

## Issue 1 : No answer for some domain names

I used the different codes at disposal from the Cloudflare GitHub and I found some issues when I did tests. 
First of all, there are some domain names which don't answer any information after a ODoH request. 

Examples with the Rust code : 

<img width="570" alt="Capture d’écran 2021-06-13 à 14 50 52" src="https://user-images.githubusercontent.com/72855563/121807977-c20fc800-cc56-11eb-8036-5e9dff188c5d.png">

*amazon.com*, one of the most popular domain name and of the most used doesn't send any answer. It's only one example in many others, like *twitter.com*, *insa-lyon.fr*, ... 

After other tests, I think about an hypothesis to explain this problem of no-answering from these domain names.
I tried to request them with the Golang code but also with the _**dig**_ command, the shell-command used to send default *DNS Queries*. 

This is what I obtained with the Golang code :

<img width="1182" alt="Capture d’écran 2021-06-13 à 15 07 00" src="https://user-images.githubusercontent.com/72855563/121808513-292e7c00-cc59-11eb-9f34-d5ce97c22eb2.png">

Indeed, I did a ODoH query, via a proxy, with a AAAA record type (equal to the rust query just before). In the answer, we don't have any @IPv6 address for this domain name, but there is a different section, that isn't in all answers. 
This section is the _**AUTHORITY SECTION**_. 

And with the _**dig**_ command : 

<img width="904" alt="Capture d’écran 2021-06-13 à 15 43 28" src="https://user-images.githubusercontent.com/72855563/121809699-1cf8ed80-cc5e-11eb-8515-ecb53ce4ea94.png">

There's also the _**AUTHORITY SECTION**_

The Authority section indicates the server(s) that are the ultimate authority for answering DNS queries about that domain.

The reason for this section is that I can query any DNS server(s), which will accept my query, to answer a query for me. 
That server may choose though to answer the query from a cache. However, if I want to ensure I get an authoritative response - I should ask the server(s) in the authority section.

So, for this kind of domain names, those for which I did not get any response, it is possible that it is due to the fact that the server with which I am querying them is not the authoritative one for these domain names.
So I guess their information is only accessible through a certain DNS server. 

There are two others examples of domain names which answer with an _**AUTHORITY SECTION**_ and which don't send IP addresses we want to obtain.

<img width="1186" alt="Capture d’écran 2021-06-13 à 15 27 52" src="https://user-images.githubusercontent.com/72855563/121809211-3862f900-cc5c-11eb-88b1-e7d009d7a6a3.png">
<img width="1186" alt="Capture d’écran 2021-06-13 à 15 28 24" src="https://user-images.githubusercontent.com/72855563/121809212-39942600-cc5c-11eb-9cf3-dc1d7c9ca99a.png">

## Issue 2 : Change of the target and proxy servers 

### Rust code

In this code, the target and the proxy servers are available and editable in the *config.toml* file.

<img width="1186" alt="Capture d’écran 2021-06-13 à 15 37 59" src="https://user-images.githubusercontent.com/72855563/121809511-5715bf80-cc5d-11eb-9b61-e97e185d2444.png">

I found some others DNS servers free and available, and I wanted to try with them to send ODoH queries, in order to see (or not) if there are any differences, with query time, information... 

