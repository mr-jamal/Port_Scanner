Building a Port Scanner in Python Using the Nmap Library
Introduction
In the realm of network security, port scanning is a crucial technique used to discover open ports on a target system, which can reveal potential vulnerabilities. While there are many tools available for port scanning, creating your own scanner using Python can be both an educational and practical experience. In this article, we will guide you through building a simple port scanner using the python-nmap library, leveraging the powerful Nmap tool within a Python script.

Prerequisites
Before we begin, ensure you have the following installed:

Python (version 3.6 or later)
Nmap (network scanning tool)
python-nmap library
To install the python-nmap library, use pip:

bash
Copy code
pip install python-nmap
Setting Up the Project
Create a new Python file, port_scanner.py, and import the nmap module:

python
Copy code
import nmap
Building the Port Scanner
Now, let's write the core functionality of our port scanner. We'll create a function, scan_ports, that takes a target IP address and a range of ports as input and scans for open ports.

Step 1: Initialize the Port Scanner
First, initialize the Nmap PortScanner object:

python
Copy code
def scan_ports(target, ports):
    nm = nmap.PortScanner()
Step 2: Perform the Scan
Next, use the scan method to perform the scan on the specified target and ports:

python
Copy code
    nm.scan(target, ports)
Step 3: Process the Scan Results
After scanning, iterate through the results to display the open ports and their states:

python
Copy code
    for host in nm.all_hosts():
        print(f'Host: {host} ({nm[host].hostname()})')
        print(f'State: {nm[host].state()}')

        for protocol in nm[host].all_protocols():
            print(f'Protocol: {protocol}')

            lport = nm[host][protocol].keys()
            for port in lport:
                print(f'Port: {port}\tState: {nm[host][protocol][port]["state"]}')
Full Code
Here's the complete code for our port scanner:

python
Copy code
import nmap

def scan_ports(target, ports):
    nm = nmap.PortScanner()
    nm.scan(target, ports)

    for host in nm.all_hosts():
        print(f'Host: {host} ({nm[host].hostname()})')
        print(f'State: {nm[host].state()}')

        for protocol in nm[host].all_protocols():
            print(f'Protocol: {protocol}')

            lport = nm[host][protocol].keys()
            for port in lport:
                print(f'Port: {port}\tState: {nm[host][protocol][port]["state"]}')

if __name__ == "__main__":
    target = input("Enter the target IP address: ")
    ports = input("Enter the range of ports to scan (e.g., '22-443'): ")
    scan_ports(target, ports)
Running the Port Scanner
To run your port scanner, execute the following command in your terminal:

bash
Copy code
python port_scanner.py
You'll be prompted to enter a target IP address and a range of ports to scan. For example:

css
Copy code
Enter the target IP address: 192.168.1.1
Enter the range of ports to scan (e.g., '22-443'): 22-443
The script will then output the open ports and their states:

makefile
Copy code
Host: 192.168.1.1 (example-hostname)
State: up
Protocol: tcp
Port: 22   State: open
Port: 80   State: open
Port: 443  State: closed
Conclusion
Creating a port scanner in Python using the Nmap library is a straightforward and educational project that introduces you to network scanning and Python scripting. This basic port scanner can be further enhanced with additional features such as multithreading for faster scans, advanced output formatting, and integration with other security tools.

Remember to use this port scanner responsibly and only on systems you have permission to test. Unauthorized scanning can be illegal and unethical. Happy scanning!
