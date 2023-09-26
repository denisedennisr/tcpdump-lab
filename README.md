<h1>Capture Packet with TCPDump</h1>

 <h2>Description</h2>
In this lab activity, I’ll perform tasks associated with using tcpdump to capture network traffic from a Linux virtual machine. I’ll capture the data in a packet capture (p-cap) file and then examine the contents of the captured packet data to focus on specific types of traffic.
<br />

<h2>Identify network interfaces</h2>
In this task, I must identify the network interfaces that can be used to capture network packet data. I used "ifconfig" to identify the interfaces that are available.
<br>
<br>
<img src="https://imgur.com/P65RIlh.png" height="80%" width="80%" alt="TCPDump"/>
<br>
<br>
The Ethernet network interface is identified by the entry with the "eth" prefix. So, in this lab, I will use eth0 as the interface that I will capture network packet data from in the following tasks. Below I used tcpdump to identify the interface options available for packet capture, this command will also allow me to identify which network interfaces are available.
<br>
<br>
<img src="https://imgur.com/xTuo9S9.png" height="80%" width="80%" alt="TCPDump"/>
<br/>
<br>
<h2>Inspect the network traffic of a network interface with tcpdump</h2>
In this task,  I  used tcpdump to filter live network packet traffic on an interface. I filtered live network packet data from the eth0 interface with tcpdump
<br>
<br>
<img src="https://imgur.com/zeaY2MY.png" height="80%" width="80%" alt="TCPDump"/>
<br />
<br />
The command I used is "sudo tcpdump -i eth0 -v -c5" which runs tcpdump with the following options: <br />
-i eth0: Capture data specifically from the eth0 interface.<br />
-v: Display detailed packet data.<br />
-c5: Capture 5 packets of data.<br />
<h2> Exploring network packet details</h2>
In the above snapshot data, at the start of the packet output, tcpdump reported that it was listening on the eth0 interface, and it provided information on the link type and the capture size in bytes. On the next line, the first field is the packet's timestamp, followed by the protocol type, IP:23:00:06.357120. The verbose option, -v, has provided more details about the IP packet fields, such as TOS, TTL, offset, flags, internal protocol type (in this case, TCP (6)), and the length of the outer IP packet in bytes. In the next section, the data shows the systems that are communicating with each other. By default, tcpdump will convert IP addresses into names, as in the screenshot. The name of your Linux virtual machine, also included in the command prompt, appears here as the source for one packet and the destination for the second packet.The direction of the arrow (>) indicates the direction of the traffic flow in this packet. Each system name includes a suffix with the port number (.5000 in the screenshot), which is used by the source and the destination systems for this packet.The flags field identifies TCP flags. In this case, the P represents the push flag and the period indicates it's an ACK flag. This means the packet is pushing out data.
The next field is the TCP checksum value, which is used for detecting errors in the data.
This section also includes the sequence and acknowledgment numbers, the window size, and the length of the inner TCP packet in bytes.
<br>
<br>
<h2> Capture network traffic with tcpdump</h2>
In this task, I used tcpdump to save the captured network data to a packet capture file. I used a filter and other tcpdump configuration options to save a small sample that contains only web (TCP port 80) network packet data. In order to capture packet data into a file called capture.pcap, I used the following command: "sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &". Further down I used "curl" to generate some HTTP (port 80) traffic and "ls-l" to verify the packet data that has been captured.
<br>
<br>
<img src=https://imgur.com/UvFcul2.png" height="80%" width="80%" alt="TCPDump"/>
<br />
<br />
<h2> Filter the captured packet data</h2>
In this task, I used tcpdump to filter data from the packet capture file I saved previously. Here I used the tcpdump command to filter the packet header data from the capture.pcap capture file. This command runs tcpdump with the following options:<br/>
-nn: Disable port and protocol name lookup.<br/>
-r: Read capture data from the named file.<br/>
-v: Display detailed packet data.  <br/>

<img src="https://imgur.com/mmNrYbG.png" height="80%" width="80%" alt="TCPDump"/>
As in the previous example, you can see the IP packet information along with information about the data that the packet contains.
<br>
<br>
In this next snapshot I used the tcpdump command "sudo tcpdump -nn -r capture.pcap -X" to filter the extended packet data from the capture.pcap capture file:
<br/>
<br/>
<img src="https://imgur.com/fSGKyvD.png" height="80%" width="80%" alt="TCPDump"/>
<br />
<br />
This command runs tcpdump with the following options: <br />
-nn: Disable port and protocol name lookup. <br />
-r: Read capture data from the named file.<br />
-X: Display the hexadecimal and ASCII output format packet data. Security analysts can analyze hexadecimal and ASCII output to detect patterns or anomalies during malware analysis or forensic analysis.<br />
<h2>Summary</h2>
In this lab I identifed network interfaces, used the tcpdump command to capture network data for inspection, interpreted the information that tcpdump outputs regarding a packet, and lastly I saved and loaded packet data for later analysis.
