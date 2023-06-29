**Lab #1: DOM XSS using web messages**

This lab demonstrates a simple web message vulnerability. To solve this lab, use the exploit server to post a message to the target site that causes the print() function to be called.

Notice that the home page contains an addEventListener() call that listens for a web message.
Go to the exploit server and add the following iframe to the body. Remember to add your own lab ID.
Store the exploit and deliver it to the victim.
When the iframe loads, the postMessage() method sends a web message to the home page. The event listener, which is intended to serve ads, takes the content of the web message and inserts it into the div with the ID ads. However, in this case it inserts our img tag, which contains an invalid src attribute. This throws an error, which causes the onerror event handler to execute our payload.
 
 ![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9dfa0342-32ec-407d-8c9d-c315cd565577)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/28fa3a82-2e92-437e-9522-3660c57acc4e)
