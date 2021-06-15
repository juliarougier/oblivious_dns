# Analyse of the messages on the network for the different requests

It seems interesting to observe what kind of messages are exchanged on the network when sending the different DNS requests.

### 1. *dig* command 

Firstly, I tried with the dig command in the terminal, with the domain name *"google.com"* and a AAAA record type : 

<img width="1426" alt="Capture d’écran 2021-06-15 à 16 38 31" src="https://user-images.githubusercontent.com/72855563/122073065-6aa95d80-cdf8-11eb-9bfd-35c6563c324b.png">

As was expected; there are DNS message request and answer and also TCP messages, because it's the transport protocol used in DNS. 

### 2. DoH request

With a DoH request : ```./odoh-client doh --domain www.google.com. --target odoh.cloudflare-dns.com --dnstype AAAA```
(*with the Go code*) we have : 

<img width="1426" alt="Capture d’écran 2021-06-15 à 16 48 21" src="https://user-images.githubusercontent.com/72855563/122074435-7fd2bc00-cdf9-11eb-956a-45b616444973.png">

We can see that there are also DNS messages, between the target (odoh-cloudflare.com) and my computer. I've added a column in Wireshark called *DNS Time* in which we could see the time between the request and the answer of DNS. For example, for this request the query time is __0.032 seconds__ for the A record type and __0.039 seconds__ for the AAAA record type.

### 3. ODoH request without proxy server 

With this command for a ODoH request directly send to target : ```./odoh-client odoh --domain www.google.com. --dnstype AAAA --target odoh.cloudflare-dns.com```

<img width="1426" alt="Capture d’écran 2021-06-15 à 16 55 45" src="https://user-images.githubusercontent.com/72855563/122075827-a5ac9080-cdfa-11eb-8296-2ac24cc8c312.png">

There are just TCP messages. I think that there are no DNS type messages since ODoH is not yet deployed and it turns out that it is not a protocol that is compatible with the existing dns infrastructure.

### 4. ODoH request via proxy server 

With this command : ```./odoh-client odoh --domain www.cloudflare.com. --dnstype AAAA --target odoh.cloudflare-dns.com --proxy odoh1.surfdomeinen.nl```

<img width="1426" alt="Capture d’écran 2021-06-15 à 17 14 34" src="https://user-images.githubusercontent.com/72855563/122078914-3ab08900-cdfd-11eb-97f4-79417812a124.png">

As for the last request, there are just TCP messages. 



