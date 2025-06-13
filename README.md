# Python Nmap Scanner

FOR EDUCATIONAL PURPOSES ONLY.

## Tools Used

- **Python 3**
- **Visual Studio Code**
- **Nmap** (installed and available in PATH)

> Practice target IP: `45.33.32.156` (This is Nmap's free scannable IP) 

---
## What is a Port Scanner and what is it used for?
A port scanner is a tool that checks which doors (ports) are open on a computer or server. It is used for security testing, network troubleshooting and learning/practice. It's important to secure systems, understand what is running and to find issues before attackers do.
---

## Installation
First you need to download Nmap and Python 3 if you haven't already. You can find instructions to those online.  

## Code with Explanations

```python
# Import the python-nmap module
import nmap

# Create a PortScanner object to interface with Nmap
nm = nmap.PortScanner()

# Define the target IP address (safe practice host)
target = "45.33.32.156"

# Define Nmap options:
# -sV: service version detection
# -sC: run default scripts
options = "-sV -sC"

# Perform the scan on the target with the specified options
nm.scan(target, arguments=options)

# Loop through all discovered hosts (should be one in this case)
for host in nm.all_hosts():
    # Print the IP and the resolved hostname (if available)
    print("Host: %s (%s)" % (host, nm[host].hostname()))

    # Print the host state (e.g., 'up' or 'down')
    print("State: %s" % nm[host].state())

    # Loop through all protocols found (typically just 'tcp')
    for protocol in nm[host].all_protocols():
        print("Protocol: %s" % protocol)

        # Get the dictionary of ports for this protocol
        port_info = nm[host][protocol]

        # Loop through each port and print its number and state
        for port, state in port_info.items():
            print("Port: %s\tState: %s" % (port, state))
