DNS
===

The Domain Name System (DNS) is a hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet or a private network. It associates various information with domain names assigned to each of the participating entities. Most prominently, it translates more readily memorized domain names to the numerical IP addresses needed for locating and identifying computer services and devices with the underlying network protocols.

![Domain Name Space](https://upload.wikimedia.org/wikipedia/commons/b/b1/Domain_name_space.svg)

### Resolution Process

In theory, authoritative name servers are sufficient for the operation of the Internet. However, with only authoritative name servers operating, every DNS query must start with recursive queries at the root zone of the Domain Name System and each user system would have to implement resolver software capable of recursive operation.

![Concept figure](https://upload.wikimedia.org/wikipedia/commons/a/a5/Example_of_an_iterative_DNS_resolver.svg)

#### Sequence Diagram

![Resolution Process](https://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/yidas/web-service-principles/main/dns/resolution-process.plantuml&v=1)

> DNS Resolver for example: [Google Public DNS - 8.8.8.8](https://developers.google.com/speed/public-dns)

### Client lookup - DNS resolution sequence

![DNS resolution sequence](https://upload.wikimedia.org/wikipedia/commons/thumb/6/60/DNS_Architecture.svg/2560px-DNS_Architecture.svg.png)

---

References
----------

[Wikipedia - Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System)

[DNS Name Resolution Process](http://www.tcpipguide.com/free/t_DNSNameResolutionProcess-2.htm)
