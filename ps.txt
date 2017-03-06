#!/usr/bin/env python
import socket
import subprocess
import sys
from datetime import datetime

#Startup and clear the CLI
subprocess.call('cls', shell=True)

#Takes a host IP and scans it.
def scan_host(host, lRange, uRange):
	#Enumerate the host name
	remoteServerIP  = socket.gethostbyname(host)
	#Fancy Printing
	print ("-" * 60)
	print ("Please wait, scanning remote host", remoteServerIP)
	print ("-" * 60)
	try:
		#Save open results to list
		list = []
		#Scan the range of ports given by user
		for port in range(int(lRange),int(uRange) + 1):  
			sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
			sock.settimeout(.001)
			result = sock.connect_ex((remoteServerIP, port))
			if result == 0:
				print (remoteServerIP + ":{}: 	 Open".format(port))
				list.append(remoteServerIP + ":{}: 	 Open".format(port))
			else:
				print (remoteServerIP + ":{}: 	 Closed".format(port))
			sock.close()

		#Output save to file.
		f = open(remoteServerIP + '.txt', 'w')
		f.truncate()
		for item in list:
			f.write("%s\n" % item)
		f.close()
	#Allow for interrupts
	except KeyboardInterrupt:
		sys.exit("You pressed Ctrl+C")

	except socket.gaierror:
		sys.exit("Hostname could not be resolved. Exiting")

	except socket.error:
		sys.exit("Couldn't connect to server")

hosts = ""
remoteServers = ""
#Dialog with end user
while hosts == "":
	hosts = input ("Use a List of Hosts? (Y/N): ")
#Sets the scan range
if hosts.lower() == "Y".lower():
	hosts = input ("File Name: ")
	f = open(hosts, 'r')
	content = f.read()
	f.close()
	remoteServers = content.split()
else:
	remoteServer    = input("Enter a remote host to scan: ")

lRange = input("Lower Range of Ports: ")
uRange = input ("Upper Ranger of Ports: ")

#Get time difference before and after the scan
t1 = datetime.now()

if remoteServers != "":
	for i in remoteServers:
		scan_host(i, lRange, uRange)
else:
	scan_host(remoteServer, lRange, uRange)

t2 = datetime.now()

total =  t2 - t1

print ('Scanning Completed in: ', total)