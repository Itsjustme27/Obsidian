
## Findings summary

| #   | Finding                                                                                      | Evidence (excerpt)                                                                                              | Severity                       | Recommended remediation                                                                                                                                                                                                                                                                    |
| --- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | Missing / inconsistent security headers (HSTS, CSP, X-Frame-Options, X-Content-Type-Options) | `http-security-headers: HSTS not configured in HTTPS Server` + `http-headers` lacked CSP/X-Frame/X-Content-Type | **Low → Medium**               | Ensure consistent `Strict-Transport-Security` on all HTTPS responses (e.g., `Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`). Add `X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY` or CSP frame-ancestors, and a Content Security Policy tuned to app. |
| 2   | Slowloris DOS detection (likely false positive)                                              | `http-slowloris-check: VULNERABLE: Slowloris DOS attack` (CVE-2007-6750)                                        | **Medium (report, verify)**    | Treat as a scanner finding. Verify by checking connection & keepalive limits at edge (Vercel) and origin. Use connection limits, timeouts, and upstream protections (load balancer, WAF, Cloudflare/Vercel rate limits). Note: likely false positive on modern cloud platform.             |
| 3   | Strange redirects / 308 + 404 responses to odd paths                                         | `Location: https:///nice%20ports%2C/Tri%6Eity.txt%2ebak` and `X-Vercel-Error: DEPLOYMENT_NOT_FOUND` in 404 body | **Low → Medium (investigate)** | Search repo / deploy configs for leftover files/redirect rules. Remove or correct erroneous redirect rules and ensure 404s don’t leak internal IDs.                                                                                                                                        |
| 4   | Edge/hosting fingerprint + proxy behavior (Vercel, Cloudflare DNS)                           | `Name Server: lee.ns.cloudflare.com, val.ns.cloudflare.com` + `Server: Vercel` + ASN/netname VERCEL-05          | **Info**                       | Note hosting provider for escalation & support. Confirm desired exposure and WAF/page rules in Vercel/Cloudflare.                                                                                                                                                                          |
| 5   | TLS certificate validity window (short lifetime)                                             | `Not valid before: 2025-09-18 ... Not valid after: 2025-12-17`                                                  | **Info**                       | Certificate looks valid; ensure auto-renew is configured and that certificate matches subdomains used.                                                                                                                                                                                     |
| 6   | User-agent restrictions & automated scan blocking on HTTP                                    | `http-useragent-tester: Status for browser useragent: 308` and port 80 allowed UAs list                         | **Low**                        | Confirm intended bot-blocking/allowlist policy. Document any rate-limiting or bot challenge rules to avoid false positives during tests.                                                                                                                                                   |


# PoC (Proof of Concept):

```shell
Bug in http-security-headers: no string output.
PORT    STATE SERVICE  VERSION
80/tcp  open  http     Vercel
| http-headers: 
|   Content-Type: text/plain
|   Location: https://mushroomnepal.com/
|   Refresh: 0;url=https://mushroomnepal.com/
|   server: Vercel
|   
|_  (Request type: GET)
|_http-comments-displayer: Couldn't find any comments.
|_http-referer-checker: Couldn't find any cross-domain scripts.
| http-useragent-tester: 
|   Status for browser useragent: 308
|   Allowed User Agents: 
|     Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)
|     libwww
|     lwp-trivial
|     libcurl-agent/1.0
|     PHP/
|     Python-urllib/2.5
|     GT::WWW
|     Snoopy
|     MFC_Tear_Sample
|     HTTP::Lite
|     PHPCrawl
|     URI::Fetch
|     Zend_Http_Client
|     http client
|     PECL::HTTP
|     Wget/1.13.4 (linux-gnu)
|_    WWW-Mechanize/1.34
|_http-mobileversion-checker: No mobile version detected.
|_http-title: Site doesn't have a title (text/plain).
|_http-fetch: Please enter the complete path of the directory to save data in.
|_http-server-header: Vercel
|_http-xssed: No previously reported XSS vuln.
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.0 308 Permanent Redirect
|     Content-Type: text/plain
|     Location: https:///nice%20ports%2C/Tri%6Eity.txt%2ebak
|     Refresh: 0;url=https:///nice%20ports%2C/Tri%6Eity.txt%2ebak
|     server: Vercel
|     Redirecting...
|   GetRequest, HTTPOptions: 
|     HTTP/1.0 308 Permanent Redirect
|     Content-Type: text/plain
|     Location: https:///
|     Refresh: 0;url=https:///
|     server: Vercel
|_    Redirecting...
443/tcp open  ssl/http Golang net/http server
|_http-comments-displayer: Couldn't find any comments.
| http-slowloris-check: 
|   VULNERABLE:
|   Slowloris DOS attack
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2007-6750
|       Slowloris tries to keep many connections to the target web server open and hold
|       them open as long as possible.  It accomplishes this by opening connections to
|       the target web server and sending a partial request. By doing so, it starves
|       the http server's resources causing Denial Of Service.
|       
|     Disclosure date: 2009-09-17
|     References:
|       http://ha.ckers.org/slowloris/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750
|_http-xssed: No previously reported XSS vuln.
|_http-title: Site doesn't have a title (text/plain).
|_http-server-header: Vercel
| ssl-cert: Subject: commonName=mushroomnepal.com
| Subject Alternative Name: DNS:mushroomnepal.com
| Not valid before: 2025-09-18T13:39:31
|_Not valid after:  2025-12-17T13:39:30
|_http-fetch: Please enter the complete path of the directory to save data in.
|_http-mobileversion-checker: No mobile version detected.
| http-security-headers: 
|   Strict_Transport_Security: 
|     HSTS not configured in HTTPS Server
|   Cache_Control: 
|_    Header: Cache-Control: private, no-store, max-age=0
| http-headers: 
|   Cache-Control: private, no-store, max-age=0
|   Content-Type: text/html; charset=utf-8
|   Server: Vercel
|   X-Vercel-Challenge-Token: 2.1760537270.60.MmNmZDBkNzI0MWI5NTIwMjBkMzdjYzU2ZmY5MzFkMmE7MzYyODE4ZmU7ZDMxZDQ2Zjg0YTBkZWNkMmZlNmE3MjFjYmE1M2Y4MTA4ZDYwYTllZTszOy7oe6ZWZgU1Y0hmp0c3DuNB2StbI+Q8SoDqaZyr4wDJHCbxrM7vDAWwp5JkZovj6ZPcq5BD0C1DrA==.0b0ce836aa3ac57d44da2c8c350ef17c
|   X-Vercel-Id: bom1::1760537270-pWuiZ5hdzhVqLHKX0F91pJM3RXBcZgTw
|   X-Vercel-Mitigated: challenge
|   Date: Wed, 15 Oct 2025 14:07:50 GMT
|   Connection: close
|   Transfer-Encoding: chunked
|   
|_  (Request type: GET)
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.0 404 Not Found
|     Cache-Control: public, max-age=0, must-revalidate
|     Content-Length: 107
|     Content-Type: text/plain; charset=utf-8
|     Date: Wed, 15 Oct 2025 14:05:35 GMT
|     Server: Vercel
|     Strict-Transport-Security: max-age=63072000
|     X-Vercel-Error: DEPLOYMENT_NOT_FOUND
|     X-Vercel-Id: bom1::kft95-1760537135606-7c9d59a2937d
|     deployment could not be found on Vercel.
|     DEPLOYMENT_NOT_FOUND
|     bom1::kft95-1760537135606-7c9d59a2937d
|   GenericLines, Help, RTSPRequest: 
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   GetRequest: 
|     HTTP/1.0 404 Not Found
|     Cache-Control: public, max-age=0, must-revalidate
|     Content-Length: 107
|     Content-Type: text/plain; charset=utf-8
|     Date: Wed, 15 Oct 2025 14:05:34 GMT
|     Server: Vercel
|     Strict-Transport-Security: max-age=63072000
|     X-Vercel-Error: DEPLOYMENT_NOT_FOUND
|     X-Vercel-Id: bom1::xnhpj-1760537134866-93756f4d2560
|     deployment could not be found on Vercel.
|     DEPLOYMENT_NOT_FOUND
|     bom1::xnhpj-1760537134866-93756f4d2560
|   HTTPOptions: 
|     HTTP/1.0 404 Not Found
|     Cache-Control: public, max-age=0, must-revalidate
|     Content-Length: 107
|     Content-Type: text/plain; charset=utf-8
|     Date: Wed, 15 Oct 2025 14:05:35 GMT
|     Server: Vercel
|     Strict-Transport-Security: max-age=63072000
|     X-Vercel-Error: DEPLOYMENT_NOT_FOUND
|     X-Vercel-Id: bom1::sr6rm-1760537135272-55343c14c701
|     deployment could not be found on Vercel.
|     DEPLOYMENT_NOT_FOUND
|_    bom1::sr6rm-1760537135272-55343c14c701
|_http-referer-checker: Couldn't find any cross-domain scripts.
| http-useragent-tester: 
|   Status for browser useragent: 403
|   Allowed User Agents: 
|     Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)
|     lwp-trivial
|     libcurl-agent/1.0
|     PHP/
|     GT::WWW
|     Snoopy
|     MFC_Tear_Sample
|     HTTP::Lite
|     PHPCrawl
|     URI::Fetch
|     Zend_Http_Client
|     http client
|     PECL::HTTP
|     Wget/1.13.4 (linux-gnu)
|     WWW-Mechanize/1.34
|   Change in Status Code: 
|     Python-urllib/2.5: 308
|_    libwww: 308
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port80-TCP:V=7.95%I=7%D=10/15%Time=68EFAA28%P=x86_64-pc-linux-gnu%r(Get
SF:Request,8A,"HTTP/1\.0\x20308\x20Permanent\x20Redirect\r\nContent-Type:\
SF:x20text/plain\r\nLocation:\x20https:///\r\nRefresh:\x200;url=https:///\
SF:r\nserver:\x20Vercel\r\n\r\nRedirecting\.\.\.")%r(HTTPOptions,8A,"HTTP/
SF:1\.0\x20308\x20Permanent\x20Redirect\r\nContent-Type:\x20text/plain\r\n
SF:Location:\x20https:///\r\nRefresh:\x200;url=https:///\r\nserver:\x20Ver
SF:cel\r\n\r\nRedirecting\.\.\.")%r(FourOhFourRequest,D0,"HTTP/1\.0\x20308
SF:\x20Permanent\x20Redirect\r\nContent-Type:\x20text/plain\r\nLocation:\x
SF:20https:///nice%20ports%2C/Tri%6Eity\.txt%2ebak\r\nRefresh:\x200;url=ht
SF:tps:///nice%20ports%2C/Tri%6Eity\.txt%2ebak\r\nserver:\x20Vercel\r\n\r\
SF:nRedirecting\.\.\.");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port443-TCP:V=7.95%T=SSL%I=7%D=10/15%Time=68EFAA2E%P=x86_64-pc-linux-gn
SF:u%r(GetRequest,1B3,"HTTP/1\.0\x20404\x20Not\x20Found\r\nCache-Control:\
SF:x20public,\x20max-age=0,\x20must-revalidate\r\nContent-Length:\x20107\r
SF:\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nDate:\x20Wed,\x2015\
SF:x20Oct\x202025\x2014:05:34\x20GMT\r\nServer:\x20Vercel\r\nStrict-Transp
SF:ort-Security:\x20max-age=63072000\r\nX-Vercel-Error:\x20DEPLOYMENT_NOT_
SF:FOUND\r\nX-Vercel-Id:\x20bom1::xnhpj-1760537134866-93756f4d2560\r\n\r\n
SF:The\x20deployment\x20could\x20not\x20be\x20found\x20on\x20Vercel\.\n\nD
SF:EPLOYMENT_NOT_FOUND\n\nbom1::xnhpj-1760537134866-93756f4d2560\n")%r(HTT
SF:POptions,1B3,"HTTP/1\.0\x20404\x20Not\x20Found\r\nCache-Control:\x20pub
SF:lic,\x20max-age=0,\x20must-revalidate\r\nContent-Length:\x20107\r\nCont
SF:ent-Type:\x20text/plain;\x20charset=utf-8\r\nDate:\x20Wed,\x2015\x20Oct
SF:\x202025\x2014:05:35\x20GMT\r\nServer:\x20Vercel\r\nStrict-Transport-Se
SF:curity:\x20max-age=63072000\r\nX-Vercel-Error:\x20DEPLOYMENT_NOT_FOUND\
SF:r\nX-Vercel-Id:\x20bom1::sr6rm-1760537135272-55343c14c701\r\n\r\nThe\x2
SF:0deployment\x20could\x20not\x20be\x20found\x20on\x20Vercel\.\n\nDEPLOYM
SF:ENT_NOT_FOUND\n\nbom1::sr6rm-1760537135272-55343c14c701\n")%r(FourOhFou
SF:rRequest,1B3,"HTTP/1\.0\x20404\x20Not\x20Found\r\nCache-Control:\x20pub
SF:lic,\x20max-age=0,\x20must-revalidate\r\nContent-Length:\x20107\r\nCont
SF:ent-Type:\x20text/plain;\x20charset=utf-8\r\nDate:\x20Wed,\x2015\x20Oct
SF:\x202025\x2014:05:35\x20GMT\r\nServer:\x20Vercel\r\nStrict-Transport-Se
SF:curity:\x20max-age=63072000\r\nX-Vercel-Error:\x20DEPLOYMENT_NOT_FOUND\
SF:r\nX-Vercel-Id:\x20bom1::kft95-1760537135606-7c9d59a2937d\r\n\r\nThe\x2
SF:0deployment\x20could\x20not\x20be\x20found\x20on\x20Vercel\.\n\nDEPLOYM
SF:ENT_NOT_FOUND\n\nbom1::kft95-1760537135606-7c9d59a2937d\n")%r(GenericLi
SF:nes,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/pla
SF:in;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Reque
SF:st")%r(RTSPRequest,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Ty
SF:pe:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\
SF:x20Bad\x20Request")%r(Help,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nCo
SF:ntent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n
SF:\r\n400\x20Bad\x20Request");

Host script results:
|_ip-geolocation-geoplugin: coordinates: nil, nil
| qscan: 
| PORT  FAMILY  MEAN (us)  STDDEV    LOSS (%)
| 80    0       70822.56   21291.83  10.0%
|_443   0       80686.00   23823.20  0.0%
|_fcrdns: FAIL (No PTR record)
| asn-query: 
| BGP: 216.198.79.0/24 | Country: US
|   Origin AS: 16509 - AMAZON-02, US
|_    Peer AS: 174 2914 3257 6461
| port-states: 
|   tcp: 
|     open: 80,443
|_    filtered: 1-79,81-442,444-65535
| whois-ip: Record found at whois.arin.net
| netrange: 216.198.79.0 - 216.198.79.255
| netname: VERCEL-05
| orgname: Vercel, Inc
| orgid: ZEITI
|_country: US stateprov: CA
|_path-mtu: PMTU == 1484
| dns-blacklist: 
|   SPAM
|     list.quorum.to - SPAM
|_    l2.apews.org - FAIL
| whois-domain: 
| 
| Domain name record found at whois.verisign-grs.com
|    Domain Name: MUSHROOMNEPAL.COM\x0D
|    Registry Domain ID: 2266223060_DOMAIN_COM-VRSN\x0D
|    Registrar WHOIS Server: whois.PublicDomainRegistry.com\x0D
|    Registrar URL: http://www.publicdomainregistry.com\x0D
|    Updated Date: 2025-09-18T14:13:26Z\x0D
|    Creation Date: 2018-05-22T08:09:45Z\x0D
|    Registry Expiry Date: 2026-05-22T08:09:45Z\x0D
|    Registrar: PDR Ltd. d/b/a PublicDomainRegistry.com\x0D
|    Registrar IANA ID: 303\x0D
|    Registrar Abuse Contact Email: abuse-contact@publicdomainregistry.com\x0D
|    Registrar Abuse Contact Phone: +1.2013775952\x0D
|    Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited\x0D
|    Name Server: LEE.NS.CLOUDFLARE.COM\x0D
|    Name Server: VAL.NS.CLOUDFLARE.COM\x0D
|    DNSSEC: unsigned\x0D
|    URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/\x0D
| >>> Last update of whois database: 2025-10-15T14:07:30Z <<<\x0D
| \x0D
| For more information on Whois status codes, please visit https://icann.org/epp\x0D
| \x0D
| NOTICE: The expiration date displayed in this record is the date the\x0D
| registrar's sponsorship of the domain name registration in the registry is\x0D
| currently set to expire. This date does not necessarily reflect the expiration\x0D
| date of the domain name registrant's agreement with the sponsoring\x0D
| registrar.  Users may consult the sponsoring registrar's Whois database to\x0D
| view the registrar's reported date of expiration for this registration.\x0D
| \x0D
| TERMS OF USE: You are not authorized to access or query our Whois\x0D
| database through the use of electronic processes that are high-volume and\x0D
| automated except as reasonably necessary to register domain names or\x0D
| modify existing registrations; the Data in VeriSign Global Registry\x0D
| Services' ("VeriSign") Whois database is provided by VeriSign for\x0D
| information purposes only, and to assist persons in obtaining information\x0D
| about or related to a domain name registration record. VeriSign does not\x0D
| guarantee its accuracy. By submitting a Whois query, you agree to abide\x0D
| by the following terms of use: You agree that you may use this Data only\x0D
| for lawful purposes and that under no circumstances will you use this Data\x0D
| to: (1) allow, enable, or otherwise support the transmission of mass\x0D
| unsolicited, commercial advertising or solicitations via e-mail, telephone,\x0D
| or facsimile; or (2) enable high volume, automated, electronic processes\x0D
| that apply to VeriSign (or its computer systems). The compilation,\x0D
| repackaging, dissemination or other use of this Data is expressly\x0D
| prohibited without the prior written consent of VeriSign. You agree not to\x0D
| use electronic processes that are automated and high-volume to access or\x0D
| query the Whois database except as reasonably necessary to register\x0D
| domain names or modify existing registrations. VeriSign reserves the right\x0D
| to restrict your access to the Whois database in its sole discretion to ensure\x0D
| operational stability.  VeriSign may restrict or terminate your access to the\x0D
| Whois database for failure to abide by these terms of use. VeriSign\x0D
| reserves the right to modify these terms at any time.\x0D
| \x0D
| The Registry database contains ONLY .COM, .NET, .EDU domains and\x0D
|_Registrars.\x0D
|_ipidseq: All zeros
| resolveall: 
|   Host 'mushroomnepal.com' also resolves to:
|   Use the 'newtargets' script-arg to add the results as targets
|_  Use the --resolve-all option to scan all resolved addresses without using this script.

Post-scan script results:
| reverse-index: 
|   80/tcp: 216.198.79.1
|_  443/tcp: 216.198.79.1
	Service detection performed.
```