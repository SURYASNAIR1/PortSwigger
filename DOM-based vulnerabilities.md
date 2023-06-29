**Lab #1: DOM XSS using web messages**

This lab demonstrates a simple web message vulnerability. To solve this lab, use the exploit server to post a message to the target site that causes the print() function to be called.

Notice that the home page contains an addEventListener() call that listens for a web message.
Go to the exploit server and add the following iframe to the body. Remember to add your own lab ID.
Store the exploit and deliver it to the victim.
When the iframe loads, the postMessage() method sends a web message to the home page. The event listener, which is intended to serve ads, takes the content of the web message and inserts it into the div with the ID ads. However, in this case it inserts our img tag, which contains an invalid src attribute. This throws an error, which causes the onerror event handler to execute our payload.
 
 ![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9dfa0342-32ec-407d-8c9d-c315cd565577)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/28fa3a82-2e92-437e-9522-3660c57acc4e)

**Lab #2: DOM XSS using web messages and a JavaScript URL**

This lab demonstrates a DOM-based redirection vulnerability that is triggered by web messaging. To solve this lab, construct an HTML page on the exploit server that exploits this vulnerability and calls the print() function.

Notice that the home page contains an addEventListener() call that listens for a web message. The JavaScript contains a flawed indexOf() check that looks for the strings "http:" or "https:" anywhere within the web message. It also contains the sink location.href.
Go to the exploit server and add the following iframe to the body, remembering to replace YOUR-LAB-ID with your lab ID:

<iframe src="https://YOUR-LAB-ID.web-security-academy.net/" onload="this.contentWindow.postMessage('javascript:print()//http:','*')">
Store the exploit and deliver it to the victim.
This script sends a web message containing an arbitrary JavaScript payload, along with the string "http:". The second argument specifies that any targetOrigin is allowed for the web message.

When the iframe loads, the postMessage() method sends the JavaScript payload to the main page. The event listener spots the "http:" string and proceeds to send the payload to the location.href sink, where the print() function is called.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4293ee4c-f6cd-4a54-86ca-b4971c22ec88)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/68a3d989-e025-439f-a076-219140d51148)

**Lab #3: Lab: DOM XSS using web messages and JSON.parse**

This lab uses web messaging and parses the message as JSON. To solve the lab, construct an HTML page on the exploit server that exploits this vulnerability and calls the print() function.

Notice that the home page contains an event listener that listens for a web message. This event listener expects a string that is parsed using JSON.parse(). In the JavaScript, we can see that the event listener expects a type property and that the load-channel case of the switch statement changes the iframe src attribute.
Go to the exploit server and add the following iframe to the body, remembering to replace YOUR-LAB-ID with your lab ID:

<iframe src=https://YOUR-LAB-ID.web-security-academy.net/ onload='this.contentWindow.postMessage("{\"type\":\"load-channel\",\"url\":\"javascript:print()\"}","*")'>
Store the exploit and deliver it to the victim.
When the iframe we constructed loads, the postMessage() method sends a web message to the home page with the type load-channel. The event listener receives the message and parses it using JSON.parse() before sending it to the switch.

The switch triggers the load-channel case, which assigns the url property of the message to the src attribute of the ACMEplayer.element iframe. However, in this case, the url property of the message actually contains our JavaScript payload.

As the second argument specifies that any targetOrigin is allowed for the web message, and the event handler does not contain any form of origin check, the payload is set as the src of the ACMEplayer.element iframe. The print() function is called when the victim loads the page in their browser.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/bcc347a5-fafb-4502-9723-0202ef2f4b62)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/5cbc5b42-2a9b-4b0b-be31-ddb4e37e7969)

**Lab #4: DOM-based open redirection**

This lab contains a DOM-based open-redirection vulnerability. To solve this lab, exploit this vulnerability and redirect the victim to the exploit server.

The blog post page contains the following link, which returns to the home page of the blog:

<a href='#' onclick='returnURL' = /url=https?:\/\/.+)/.exec(location); if(returnUrl)location.href = returnUrl[1];else location.href = "/"'>Back to Blog</a>
The url parameter contains an open redirection vulnerability that allows you to change where the "Back to Blog" link takes the user. To solve the lab, construct and visit the following URL, remembering to change the URL to contain your lab ID and your exploit server ID:

https://YOUR-LAB-ID.web-security-academy.net/post?postId=4&url=https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4ff98aa2-f368-4a2e-a6ed-f3a2ac2e55a9)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4ef23f46-25dc-485c-be30-a28a1312e62d)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b0be0f94-fd6e-43ee-8eff-f0c856063db7)
