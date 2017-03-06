Port Scanner will do many things

Currently it scans a specified host and port and presents simple response. 40pts
Allows for multiple hosts to be scanned from a text file. 5pts
Allows for multiple ports to be scanned. 10pts
Does all Protocols and searches for open ports that way. 15pts
Results print based on searched hosts to a text file. 10pts
Displays time took to scan. 5pts
Allows for Ctrl-C Interrupt (CHECK THAT USABILITY)

Prompts are as follows:
1. Enter Y or N if you are going to use a list of hosts.
  1.a If Y, enter a text file name with the hosts on separate lines
  1.b If N, enter the host IP that you want scanned
2.  Enter the lower bound of ports to scan
3.  Enter the upper bound of ports to scan
The Scanner will now print in CLI as it checks all the ports.
It will save a text file in this format "HostIP.txt" for each host IP


I used the following as a template
http://www.pythonforbeginners.com/code-snippets-source-code/port-scanner-in-python
