Project B (Python)

You have been learning building blocks of Python programming language and now it is the time to
apply those skills by implementing and using techniques to solve a real-world network security related
issue, which you may face while working as a Security Professional in field.
You are hired in an organization as a security professional and your first task is to analyze a network
for vulnerabilities. There are many different servers on a network, running various services, to support
day to day business operations. You have been asked to gather the information about the possible
vulnerabilities on any specific server
Your task is to write a Python program that should test the given host and it should generate a list of
all the TCP Open ports within the range of 1 to 1025. You are required to accomplish this task by using
standard Python’s “socket” library. 

Project Python Code 

![image](https://user-images.githubusercontent.com/78877077/117553438-4a2afe00-b017-11eb-8e61-c6fead470c97.png)

import socket
import sys
from datetime import datetime

# Ask the user to enter a host to scan
host = input("Enter a host to scan: ")
hostIP = socket.gethostbyname(host)
print("Starting scan on host: ", hostIP)

scan_result = open("host scan results.txt", "w")
# The scan of the host is about to start
scan_result.write("Please wait, Starting the host scan: " + str(hostIP) + "\n")

# time when the scan started
time1 = datetime.now()
scan_result.write("Starting time: " + str(time1) + "\n")

try:
    for i in range(1, 1025):
        scan_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        scan_socket.settimeout(0.001)
        result = scan_socket.connect_ex((hostIP, i))
        if result == 0:
            scan_result.write("Port " + str(i) + " OPEN " + "\n")
            print("Port " + str(i) + " OPEN ")
            scan_socket.close()

except socket.gaierror:
    scan_result.write("Host is not available ")
    print("Host is not available ")
    sys.exit()

# Time when the scan end
time2 = datetime.now()
scan_result.write("Ending time: " + str(time2) + "\n")

# Calculates the total time it took for the scanning process
total = time2 - time1
scan_result.write("Total time it took for the port scanning process: " + str(total))
