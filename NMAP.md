<h1>
  
  [NMAP](https://tryhackme.com/room/furthernmap)
</h1>

Teaches how to use NMAP effectively.

NMAP (Network Mapper) tool is used for network discovery. Used to find devices on network, check open/closed ports on target, services, OS, vulnerability scanning, firewall detection, etc.

example scan:
nmap --script=(script name) -Pn -sX -p1-999 (IP address)

* --script vuln - scans vulnerabilities
* -p- - scans all ports
* -T(0-5) - timing template. 0-5 slowest to fastest. Can speed up nmap.
