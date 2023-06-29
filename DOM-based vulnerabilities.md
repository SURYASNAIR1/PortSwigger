**Lab #1: DOM XSS using web messages**

This lab demonstrates a simple web message vulnerability. To solve this lab, use the exploit server to post a message to the target site that causes the print() function to be called.

Notice that the home page contains an addEventListener() call that listens for a web message.
Go to the exploit server and add the following iframe to the body. Remember to add your own lab ID.
Store the exploit and deliver it to the victim.
When the iframe loads, the postMessage() method sends a web message to the home page. The event listener, which is intended to serve ads, takes the content of the web message and inserts it into the div with the ID ads. However, in this case it inserts our img tag, which contains an invalid src attribute. This throws an error, which causes the onerror event handler to execute our payload.
 
 ![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9dfa0342-32ec-407d-8c9d-c315cd565577)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/28fa3a82-2e92-437e-9522-3660c57acc4e)

**Lab: DOM XSS using web messages and a JavaScript URL**

This lab demonstrates a DOM-based redirection vulnerability that is triggered by web messaging. To solve this lab, construct an HTML page on the exploit server that exploits this vulnerability and calls the print() function.

Notice that the home page contains an addEventListener() call that listens for a web message. The JavaScript contains a flawed indexOf() check that looks for the strings "http:" or "https:" anywhere within the web message. It also contains the sink location.href.
Go to the exploit server and add the following iframe to the body, remembering to replace YOUR-LAB-ID with your lab ID:

<iframe src="https://YOUR-LAB-ID.web-security-academy.net/" onload="this.contentWindow.postMessage('javascript:print()//http:','*')">
Store the exploit and deliver it to the victim.
This script sends a web message containing an arbitrary JavaScript payload, along with the string "http:". The second argument specifies that any targetOrigin is allowed for the web message.

When the iframe loads, the postMessage() method sends the JavaScript payload to the main page. The event listener spots the "http:" string and proceeds to send the payload to the location.href sink, where the print() function is called.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4293ee4c-f6cd-4a54-86ca-b4971c22ec88)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/68a3d989-e025-439f-a076-219140d51148)
