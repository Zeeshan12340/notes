# Theory
A DNS record is a database record used to map a URL to an IP address. DNS records are stored in DNS servers and work to help users connect their websites to the outside world.

The most common record types are A (address), CNAME (canonical name), MX (mail exchange), NS (name server), PTR (pointer), SOA (start of authority) and TXT (text record).

Different types of DNS records are as follows:

*   Name Server (NS) Record: Describes a name server for the domain that permits DNS lookups within several zones. Every primary as well as secondary name server must be reported via this record.
*   Mail Exchange (MX) Record: Permits mail to be sent to the right mail servers located in the domain. Other than IP addresses, MX records include fully-qualified domain names.
*   Address (A) Record: Used to map a host name to an IP address. Generally, A records are IP addresses. If a computer consists of multiple IP addresses, adapter cards, or both, it must possess multiple address records.
*   Canonical Name (CNAME) Record: Can be used to set an alias for the host name
*   Text (TXT) Record: Permits the insertion of arbitrary text into a DNS record. These records add SPF records into a domain.
*   Time-to-Live (TTL) Record: Sets the period of data, which is ideal when a recursive DNS server queries the domain name information
*   Start of Authority (SOA) Record: Declares the most authoritative host for the zone. Every zone file should include an SOA record, which is generated automatically when the user adds a zone.
*   Pointer (PTR) Record: Creates a pointer, which maps an IP address to the host name in order to do reverse lookups.