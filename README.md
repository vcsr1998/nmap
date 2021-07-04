# nmap


# COMMANDS 


# -p  => specified port

      nmap -p 80 10.20.1.1
      
          it only means that on 10.20.1.1 - we had selected to work on - it is not a complete command - it is usally mixed up up with other commands.
    
    
# -sn : only performs a host discovery  ( SCAN FOR NETWORK )
      
          A) eg : nmap -sn 10.20.1.1-30
            
                 Nmap only scans a subset of the network, it scans 30 hosts.   Using the above command, nmap pings each " host " to see if the host is up.
    
          B) eg : Limiting the number of scanned hosts using the network mask
              
                 The whole address is 32 bits. If we use 24 bits for the network mask, we will be left with 8 bits for the hosts.
                 The 8 bits represent hosts from address 10.10.20.1 to address 10.10.20.254 ( 1+2+4+...+128 = 255).
                 The 10.10.20.255 is a special address dedicated to broadcasting.
                 
                 nmap -sn 10.20.1.0/24
                 
                 The above command scans hosts from 10.20.1.1 to 10.20.1.254
   
# -PS  : TCP SYN ping scan 

        nmap -PS 10.20.1.1
        
        We can use the above command to check if any service is open on the host.   The command opens a connection on the port of a service and closes it before the connection is fully established (TCP SYN ping).  --- SYN - synchronize.
        
        We send an empty TCP packet with a SYN flag set and we wait for the usual SYN ACK response
# -PU : UDP ping scan:

         nmap -PU 10.20.1.1
         
         We could also use UDP scan, that by default it scans the port 40125 which is not likely to be used. The "port unreachable" response indicates the the host is up.
         
# -sV  : Scanning and version discovery:
 
         nmap -PS -sV -p 80 10.20.1.1
         
         -PS : does a TCP port scan 
         -sV  : scans for version ( on port 80 beacuse it is specified )
          The above command displays the version of the service running on port 80.
          
# -sU : does a UDP port scan.

          nmap -sU -P0 -F 10.20.1.1
          
          -P0 : assumes that the host is up but not responsive to host discovery (Ping scan =>  -PU : UDP ping scan:    ).
          
          -F : fast scan to a limited number of ports.
          
          -sU : does a UDP port scan.
          
          The above command displays a list of UDP ports and the services associated with them.
          
# -sSU : Scanning port ranges :
   
          nmap -sSU -p U:51,118,T:80,137 10.20.1.1
          
          -sSU : scans both TCP (T) and UDP (U) ports.
          
          -p U:51,118,T:80,137    => ports  
          
          The above command scans a range of UDP ( 51 to 118 ) and TCP ( 80 to 137 ) ports
          
# -O : checks the operating system  -  Discovering the operating system of a host:

          nmap -PS -O 10.20.1.1
          
          -PS : does a TCP port scan.
          
          -O : checks the operating system.
          
          
# -A : Aggressive mode:          
         
          nmap -PS -A 10.20.1.1
         
         -PS : does a TCP port scan (Ping Scan)
         
          -A : Aggressive mode which does OS detection (-O), software version detection (-sV), script scanning (-sC) and "traceroute" which records information about the route the packets take on their way to their destination (10.20.1.1).
          
          
          
# -s : script scan

        -s : stands for a script scan, it uses the default nmap scripts
         
