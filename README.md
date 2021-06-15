# Oblivious DNS 

In this repository, there is my study of oblivious DNS as part of a research initiation project on DNS and privacy in a French engineering school : INSA Lyon. 

__*Project's tutor : Mathieu CUNCHE*__

# What is Oblivious DNS ? 

As DNS operates today, queries and responses are viewable as plaintext at the recursive resolver, even if the client is using an encrypted channel between it and the recursive resolver. As a result, they can reveal significant information about the Internet destinations that a user or device is communicating with. For example, the domain names themselves reveal the websites that a user visits. Additionally, in the case of smart-home Internet of Things (IoT) devices, DNS queries may reveal the types of devices in user homes.

Recursive DNS resolver operators can readily associate and track IP addresses of the client and by the way their identities along with information about their DNS queries, creating a real point of privacy risk.

ODNS operates in the context of the existing DNS protocol, allowing the existing deployed infrastructure to remain unchanged. ODNS decouples client identity from queries by leveraging the behavior of the global DNS system itself. A client sends an encrypted query to a recursive resolver, which then forwards the query to a ODNS resolver (an authoritative DNS server that can resolve ODNS queries). The recursive resolver never sees the domains that the client queries, and the ODNS resolver never sees the IP address of the client.

The primary goal of ODNS is to disallow the recursive resolver to have access to both the client IP address and the DNS query information. ODNS must decouple these two pieces of information by hiding the client’s DNS query traffic from the recursive resolver.

<img width="604" alt="Capture d’écran 2021-06-12 à 11 00 51" src="https://user-images.githubusercontent.com/72855563/121771105-91079880-cb6d-11eb-82c5-172b71245a64.png"> 

For more informations about this protocol, everything is in the paper in the section *"papers"*. 

Althought this protocol isn't deployed at big scale, I chose to study more another one, which is pretty similar with this one. 
This is the ODoH protocol : Oblivious DNS-over-HTTPS. The paper which talks about it is also available in the section "papers". 

Engineers from Cloudflare, Apple and the Fastly distribution network have come up with Oblivious DoH, a new protocol that will make a major change to the current domain name system that translates domain names into IP addresses that computers need to find. other computers on the Internet.
The project is in collaboration with the Internet Engineering Task Force (IETF, for Internet Standards), in the hope that it will become an industry-wide standard. Short for ODoH, Oblivious DoH relies on a separate DNS enhancement called DNS-over-HTTPS (short for DoH), which is still in its early stages of adoption.

ODoH works by adding a layer of public key encryption, as well as a network proxy between clients and DoH servers such as 1.1.1.1. According to Cloudflare, the combination of these two added elements ensures that only the user has access to both DNS messages and their own IP address at the same time.

![image6-2](https://user-images.githubusercontent.com/72855563/121778066-73e6c000-cb95-11eb-92a6-85d0350f5156.png)

Here a scheme showing the ODoH dispositive. 

This protocol is neither stable nor officially deployed. However, Cloudflare does provide two ODoH tests.
The first is available at this address: the odoh client in Rust language, working with the odoh-rs server.
The second, in Go language, is available here:
With the client and the server as well.
In the section ODoH I show my experiments with these codes. 





