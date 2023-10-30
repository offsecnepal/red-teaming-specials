# Netcat Complete Guide
![netcat-tutorial](https://github.com/offsecnepal/red-teaming-specials/assets/111997815/5ca36c6f-0a8a-46c9-b0a9-e21d4e073f8b)
# Basic switches/flags used:
```
    -e program to execute after connect
    -l listen mode for inbound connects
    -p designates the locat port
    -u UDP mode
    -v verbose output
```
# Help Command
`nc -h`
> Prints every possible option that it can do for us.
# TCP Scan
```
nc -v –n –z <ip> <range min>-<range max>
```

- `[-v]`: indicates Verbose mode
- `[-n]`: indicates numeric-only IP addresses
- `[-z]`: indicates zero -I/O mode (we set the “-z” flag, which tells netcat, to scan listing daemon without sending
any data. )
# UDP scan
```
nc –vzu <ip> <port>
```
> -u flag invokes UDP mode. We'll capture if any service is running on the port or not.
 # Terminal Chatting
 > In its most basic form, Ncat simply moves bits from one place to another. This is all that is needed to set up a simple chat system. By default, Ncat reads from standard input and writes to standard output, meaning that it will send whatever is typed at the keyboard and will show on the screen whatever is received. With this setup, two users can communicate with each other.
## Listener
 ```
nc –lvp 4444
```

- `[l]`: Listen Mode
- `[v]`: Verbose Mode
- `[p]`: Local Port
## Initiator
```
nc <listener ip> <lport>
```
# Banner Grabbing
```
nc <ip> 80
HEAD / HTTP/1.0
```
> We can also use netcat to “grab” the banner on web servers by connecting to port 80 and then sending a HEAD / HTTP/1.0 or HEAD / HTTP/1.1 request depending upon the protocol which they’re using.
# File Transfer
> One of the simple wonders of netcat is its ability to transfer files between computers. By creating this simple connection, we can then use that connection to transfer files between two machines. This can be extremely useful as a network administrator and even more useful as a hacker. Netcat can be used to upload and download files from and to the target system.
## Listener:
```
nc –lvp 5555 < file.txt
```
> Sender sets up a listener at port number 5555, andshares file.txt using the “<” parameter.
# Remote System 
```
nc <ip> 5555 > file.txt
```
> Receiver system will download this file by the above command.
