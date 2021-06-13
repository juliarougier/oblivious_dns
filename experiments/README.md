# Oblivious DNS experiments 

The sources used for these experiments with ODoH come from these github: 
- https://github.com/cloudflare/odoh-rs (server Rust)
- https://github.com/cloudflare/odoh-client-rs/ (client Rust) 
- https://github.com/cloudflare/odoh-go (server Golang)
- https://github.com/cloudflare/odoh-client-go (client Golang)

# 1 . ODoH simple requests 

## Rust code 

Before doing some ODoH requests, I had to install Rust with this link : https://www.rust-lang.org/tools/install. 

The following code allows to do a ODoH request : 

```sh
cargo run -- example.com <record type>
```

First, I tried to do simples requests with different famous domain names with the AAAA record type (@IPv6 addresses) 
<img width="1194" alt="Capture d’écran 2021-06-12 à 17 33 35" src="https://user-images.githubusercontent.com/72855563/121781721-68e85b80-cba6-11eb-8cfa-12fa7257da00.png">
<img width="1194" alt="Capture d’écran 2021-06-12 à 17 34 02" src="https://user-images.githubusercontent.com/72855563/121781725-6a198880-cba6-11eb-83de-0588ca957a13.png">
<img width="1194" alt="Capture d’écran 2021-06-12 à 17 40 08" src="https://user-images.githubusercontent.com/72855563/121781728-6c7be280-cba6-11eb-9992-42601f6cc164.png">
<img width="1194" alt="Capture d’écran 2021-06-12 à 17 46 53" src="https://user-images.githubusercontent.com/72855563/121781729-6c7be280-cba6-11eb-9167-8da67faa7b85.png">
<img width="1194" alt="Capture d’écran 2021-06-12 à 17 47 13" src="https://user-images.githubusercontent.com/72855563/121781730-6d147900-cba6-11eb-871b-3828f39629f4.png">

Also with A record type (@IPv4 addresses) ; with the same domain names 

<img width="1194" alt="Capture d’écran 2021-06-13 à 09 49 34" src="https://user-images.githubusercontent.com/72855563/121799501-db9c1a00-cc2c-11eb-9172-c9a850c96bf7.png">
<img width="1194" alt="Capture d’écran 2021-06-13 à 09 49 50" src="https://user-images.githubusercontent.com/72855563/121799503-dccd4700-cc2c-11eb-86b1-d2ce380a3abc.png">
<img width="1194" alt="Capture d’écran 2021-06-13 à 09 50 02" src="https://user-images.githubusercontent.com/72855563/121799504-ddfe7400-cc2c-11eb-91a4-73e94b6643c2.png">
<img width="1194" alt="Capture d’écran 2021-06-13 à 09 50 12" src="https://user-images.githubusercontent.com/72855563/121799505-de970a80-cc2c-11eb-9233-48452fbb0839.png">
<img width="1194" alt="Capture d’écran 2021-06-13 à 09 50 45" src="https://user-images.githubusercontent.com/72855563/121799507-de970a80-cc2c-11eb-9ced-a0eea26ca811.png">


## Signification of the answers 

In these answer to ODoH request with the Rust code, we could see different informations. 
The answer takes this syntax : 

```sh
Response: [Record { name_labels: Name { is_fqdn: true, label_data: [113, 117, 97, 100, 57, 110, 101, 116], label_ends: [5, 8] }, rr_type: A, dns_class: IN, ttl: 1200, rdata: A(216.21.3.77) }]
```
In this one : 

- name_labels 
- is_fqdn : true/false --> this boolean condition checks if the domain name given in the command is *fqdn*
- label_data : 
- label_ends : 
- rr_type : the type of record used (A, AAAA, etc)
- dns_class :
- ttl : the time to live of the message in seconds ? 
- rdata : the data returned by the record type used --> here is the IPv4 address corresponding to this domain name


*fqdn : A fully qualified domain name (FQDN, or fully qualified domain name) is a domain name that gives the exact position of its node in the DNS tree, indicating all the top-level domains.



## Golang code (odoh-client-go) 

This client code in Go language offers several features. It is possible to make DoH requests, ODoH requests via a proxy or without a proxy as well. So I tested these several possibilities with these commands proposed by clouflare : 

- [x] DoH Query: `odoh-client doh --domain www.cloudflare.com. --dnstype AAAA --target <target>` where `<target>` is the name of the target resolver, e.g., `odoh.cloudflare-dns.com`.
- [x] ODoH Query: `odoh-client odoh --domain www.cloudflare.com. --dnstype AAAA --target <target>`
- [x] ODoH Query via Proxy: `odoh-client odoh --domain www.cloudflare.com. --dnstype AAAA --target <target> --proxy <proxy>` where `<proxy>` is the name of a proxy server

Before doing queries, I had to build the executable file with this command : 

```sh
go build 
```

### 1. DoH Query test 

```sh
./odoh-client doh --domain www.cloudflare.com. --target odoh.cloudflare-dns.com --dnstype AAAA
```

<img width="1026" alt="Capture d’écran 2021-06-13 à 14 34 17" src="https://user-images.githubusercontent.com/72855563/121807467-955ab100-cc54-11eb-8d52-bee1930945e6.png">


### 2. ODoH Query to target test 

```sh
./odoh-client odoh --domain www.cloudflare.com. --dnstype AAAA --target odoh.cloudflare-dns.com
```

<img width="1032" alt="Capture d’écran 2021-06-13 à 14 34 32" src="https://user-images.githubusercontent.com/72855563/121807490-ac999e80-cc54-11eb-96cd-448b25dcc0a6.png">


### 3. ODoH Query to target via proxy test 

```sh
./odoh-client odoh --domain www.cloudflare.com. --dnstype AAAA --target odoh.cloudflare-dns.com --proxy odoh1.surfdomeinen.nl
```
<img width="1190" alt="Capture d’écran 2021-06-13 à 14 35 00" src="https://user-images.githubusercontent.com/72855563/121807507-bd4a1480-cc54-11eb-9696-94ab6561f380.png">

In the three commands, there are the same informations at the end : the record type (here AAAA), the status, the opcode and in the ANSWER Section the result of the record type asked (here the IPv6 addresses). 




