# ⚙️ w_nslookup

Tags: #⚙️
Related to:
See also:
Previous:

## Description

Active Directory Domain Services (AD DS) uses DNS to allow clients (workstations, servers, and other systems that communicate with the domain) to locate Domain Controllers and for Domain Controllers that host the directory service to communicate amongst themselves. DNS is used to resolve hostnames to IP addresses and is broadly used across internal networks and the internet. Private internal networks use Active Directory DNS namespaces to facilitate communications between servers, clients, and peers. AD maintains a database of services running on the network in the form of service records (SRV). These service records allow clients in an AD environment to locate services that they need, such as a file server, printer, or Domain Controller. Dynamic DNS is used to make changes in the DNS database automatically should a system's IP address change. Making these entries manually would be very time-consuming and leave room for error. If the DNS database does not have the correct IP address for a host, clients will not be able to locate and communicate with it on the network. When a client joins the network, it locates the Domain Controller by sending a query to the DNS service, retrieving an SRV record from the DNS database, and transmitting the Domain Controller's hostname to the client. The client then uses this hostname to obtain the IP address of the Domain Controller. DNS uses TCP and UDP port 53. UDP port 53 is the default, but it falls back to TCP when no longer able to communicate and DNS messages are larger than 512 bytes.

![[dns_highlevel.png]]

## Usage Examples

### Forward DNS Lookup

Let's look at an example. We can perform a `nslookup` for the domain name and retrieve all Domain Controllers' IP addresses in a domain.

	nslookup INLANEFREIGHT.LOCAL

```text
Server:  172.16.6.5
Address:  172.16.6.5

Name:    INLANEFREIGHT.LOCAL
Address:  172.16.6.5
```

### Reverse DNS Lookup

If we would like to obtain the DNS name of a single host using the IP address, we can do this as follows:

	nslookup 172.16.6.5

```text
Server:  172.16.6.5
Address:  172.16.6.5

Name:    ACADEMY-EA-DC01.INLANEFREIGHT.LOCAL
Address:  172.16.6.5
```

### Finding IP Address of a Host

If we would like to find the IP address of a single host, we can do this in reverse. We can do this with or without specifying the FQDN.

	nslookup ACADEMY-EA-DC01

```text
Server:   172.16.6.5
Address:  172.16.6.5

Name:    ACADEMY-EA-DC01.INLANEFREIGHT.LOCAL
Address:  172.16.6.5
```

# References

For deeper dives into DNS, check out the [DNS Enumeration Using Python](https://academy.hackthebox.com/course/preview/dns-enumeration-using-python) module and the DNS section of the [Information Gathering - Web Edition](https://academy.hackthebox.com/course/preview/information-gathering---web-edition) module.