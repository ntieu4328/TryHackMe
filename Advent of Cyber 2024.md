<h1>
  
  [Advent of Cyber 2024](https://tryhackme.com/room/adventofcyber2024)
</h1>

Challenges delivered like an advent calendar with a storyline.<br>

<h2>Tools:</h2>

Elastic - cybersecurity threat detection, investigation, and response <br>
* learned how to filter for specific events and information <br>
* can use KQL (Kibana Query Language) to search <br>

CyberChef - simple and complex data manipulation <br>
* decode encoded data <br>

Atomic Red - collection of red team test cases that can be executed to test for detection gaps <br>
* runs on powershell
* if you want to run on linux and mac install PowerShell Core
* invoke-atomictest (technique)
* parameters:
  * -ShowDetails: shows details of each test
  * -Checkprereq: check that all required resources are in place
  * -testnumbers (# of test): specify which test you want done
  * -cleanup: clean up artifacts from the test
 
Event Viewer - Windows tool that displays information about significant events happening on computer <br>

Burp Suite - Web application security testing and penetration testing. Intercepting, analyzing and modifying network traffic <br>
Set up intercepting and modifying website requests: <br>
* Settings -> Allow Brup's browser to run without a sandbox
* Proxy -> Intercept -> Open Browser
* In browser -> browse website
* Proxy -> HTTP History
* Find request to exploit -> send to repeater -> edit request -> Send

<h2>Languages:</h2>

XML (Extensible Markup Language) - language used to transport and store data
* uses tags to label and organise information
* DTD (Document Type Definition) - set of rules that defines the structure of an XML document
* Entities - insertion of large chunks of data referencing internal or external files
  * ex: `<!DOCTYPE foo [ <!ENTITY ext SYSTEM "http://normal-website.com" > ]>`
  * reference entity: `&ext;`


<h2>Commands:</h2>

Kali Linux:
* file - determines the type of file and its data
* exiftool - software used for reading, writing, and editing metadata

<h2>Vulnerabilities:</h2>

XXE (XML External Entity) - Takes advantage of how XML handles external entities
* point external entity to malicious source or code
* Intercept requests with Burp Suite
* In browser -> browse website
* Proxy -> HTTP History
* Find request to exploit -> send to repeater -> edit request -> Send
