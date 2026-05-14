# Operating Model

Understanding how DNS works with each record type and routing policy is essential for optimizing the performance and reliability of web applications. Below is a detailed explanation:

### How DNS Works with Different Record Types

When a user enters a domain name (for example: [www.example.com](http://www.example.com)) into a browser, the DNS resolution process occurs as follows:

#### Recursive Request

The user’s computer sends a domain name resolution request to the recursive DNS server configured on the computer or router.

#### Iterative Queries

The recursive DNS server begins a series of iterative queries to different DNS servers to find the IP address associated with the domain name. This process usually starts with the root server, followed by the top-level domain (TLD) server for `.com`, and then the authoritative name server for `example.com`.

#### Authoritative Response

The authoritative name server contains the DNS records for the `example.com` domain and returns the appropriate record based on the request.

Below is how different record types affect this process:

#### A Record

An A record maps a domain name to an IPv4 address. Example:

```
www.example.com.    A     192.0.2.1
```

When the DNS server receives a request for `www.example.com`, it returns the IP address `192.0.2.1`.

#### CNAME Record

A CNAME record creates an alias for another domain name. Example:

```
blog.example.com.   CNAME www.example.com.
```

When the DNS server receives a request for `blog.example.com`, it detects the CNAME record and continues querying for `www.example.com`, then returns the IP address associated with `www.example.com`.

#### MX Record

An MX record specifies the mail server responsible for receiving emails for a domain. Example:

```
example.com.        MX    10 mail.example.com.
```

The number `10` is the priority value. Lower numbers indicate higher priority. When a mail server wants to send an email to `user@example.com`, it queries the MX record and connects to the highest-priority mail server.

#### SRV Record

An SRV record specifies the location of specific services. Example:

```
_sip._tcp.example.com. SRV 10 0 5060 sipserver.example.com.
```

This record indicates that the SIP service over TCP is provided by the server `sipserver.example.com` on port `5060`.

#### PTR Record

A PTR record performs reverse DNS lookup, mapping an IP address back to a domain name. Example:

```
1.0.2.192.in-addr.arpa. PTR www.example.com.
```

When the DNS server receives a request for the IP address `192.0.2.1`, it returns the domain name `www.example.com`.

#### TXT Record

A TXT record contains arbitrary text. It is commonly used for purposes such as email authentication (SPF, DKIM, DMARC) or domain ownership verification.

```
example.com.        TXT   "v=spf1 mx -all"
```

### How DNS Works with Different Routing Policies

Routing policies determine how the DNS server selects which record to return when multiple records are available for the same domain name.

#### Simple Routing

This is the simplest routing policy. The DNS server returns records in the order they are listed. It is commonly used when there is only one server or when advanced routing features are unnecessary.

#### Geolocation Routing

This policy routes traffic based on the user’s geographic location. For example, users in Northern Vietnam may be routed to a server in Hanoi, while users in Southern Vietnam may be routed to a server in Ho Chi Minh City. This helps reduce latency and improve performance.

#### Weighted Routing (with Sticky Session)

This policy distributes traffic based on weights assigned to each resource (such as servers). For example, you can assign a weight of 70 to Server A and 30 to Server B, meaning that 70% of traffic will be routed to Server A and 30% to Server B.

The Sticky Session feature ensures that a specific user is consistently routed to the same server throughout their session. This is especially useful for applications that require session persistence, such as online shopping carts.
