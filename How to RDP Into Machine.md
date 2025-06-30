<h1>

How to RDP into Machine
</h1>

Install xfreerdp:

1. sudo apt search freerdp

2. sudo apt install (freerdp version you want (common is freerdp3-x11))

3. If using freerdp3-x11 have to install freerdp3-shadow-x11

4. For TryHackMe: If doesn't open -> `sudo killall openvpn`

RDP into Machine:

* xfreerdp3 /u:(username) /p:(password) /v:(machine IP)
