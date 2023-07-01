**Lab #1: Reflected XSS into HTML context with nothing encoded**

This lab contains a simple reflected cross-site scripting vulnerability in the search functionality.

To solve the lab, perform a cross-site scripting attack that calls the alert function.

Copy and paste the following into the search box:

<script>alert(1)</script>
Click "Search".

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/88093769-3c4a-4ccc-85d2-59746230a02d)

**Lab #2: Stored XSS into HTML context with nothing encoded**

This lab contains a stored cross-site scripting vulnerability in the comment functionality.

To solve this lab, submit a comment that calls the alert function when the blog post is viewed.

Enter the following into the comment box:

<script>alert(1)</script>
Enter a name, email and website.
Click "Post comment".
Go back to the blog.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b03ea046-1c12-449c-a835-b598f2359f6a)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/8d4792cd-b40e-40e2-bcbf-db082baeb8b9)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/7273dcab-b258-4895-b73a-7d3fad1d42d0)

**Lab #5: DOM XSS in jQuery anchor href attribute sink using location.search source**

This lab contains a DOM-based cross-site scripting vulnerability in the submit feedback page. It uses the jQuery library's $ selector function to find an On the Submit feedback page, change the query parameter returnPath to / followed by a random alphanumeric string.
Right-click and inspect the element, and observe that your random string has been placed inside an a href attribute.

Change returnPath to:

javascript:alert(document.cookie)
Hit enter and click "back".anchor element, and changes its href attribute using data from location.search.

To solve this lab, make the "back" link alert document.cookie.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/a8630541-a2b6-47ad-8c51-b9ec74b041bf)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/0c0e3841-f00e-46d0-9d08-c0ea6f6bb334)

**Lab #6: DOM XSS in jQuery selector sink using a hashchange event**

This lab contains a DOM-based cross-site scripting vulnerability on the home page. It uses jQuery's $() selector function to auto-scroll to a given post, whose title is passed via the location.hash property.

To solve the lab, deliver an exploit to the victim that calls the print() function in their browsers.

Notice the vulnerable code on the home page using Burp or the browser's DevTools.
From the lab banner, open the exploit server.
In the Body section, add the following malicious iframe:

<iframe src="https://YOUR-LAB-ID.web-security-academy.net/#" onload="this.src+='<img src=x onerror=print()>'"></iframe>
Store the exploit, then click View exploit to confirm that the print() function is called.
Go back to the exploit server and click Deliver to victim to solve the lab.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/64dd9017-1489-4af8-916b-f4d60571ea60)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/207fb1e4-793f-42fe-8067-b6e4ea562abb)

**Lab #7: Reflected XSS into attribute with angle brackets HTML-encoded**

This lab contains a reflected cross-site scripting vulnerability in the search blog functionality where angle brackets are HTML-encoded. To solve this lab, perform a cross-site scripting attack that injects an attribute and calls the alert function.

Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater.
Observe that the random string has been reflected inside a quoted attribute.
Replace your input with the following payload to escape the quoted attribute and inject an event handler:

"onmouseover="alert(1)
Verify the technique worked by right-clicking, selecting "Copy URL", and pasting the URL in the browser. When you move the mouse over the injected element it should trigger an alert.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1430bb24-42c4-4752-b8ac-90dcb781d7f9)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1b8d24cd-6fa7-4745-8510-d36b79c3a1bb)

**Lab #8: Stored XSS into anchor href attribute with double quotes HTML-encoded**

This lab contains a stored cross-site scripting vulnerability in the comment functionality. To solve this lab, submit a comment that calls the alert function when the comment author name is clicked.

Post a comment with a random alphanumeric string in the "Website" input, then use Burp Suite to intercept the request and send it to Burp Repeater.
Make a second request in the browser to view the post and use Burp Suite to intercept the request and send it to Burp Repeater.
Observe that the random string in the second Repeater tab has been reflected inside an anchor href attribute.
Repeat the process again but this time replace your input with the following payload to inject a JavaScript URL that calls alert:

javascript:alert(1)
Verify the technique worked by right-clicking, selecting "Copy URL", and pasting the URL in the browser. Clicking the name above your comment should trigger an alert.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/c779a839-4229-4d35-a5ef-616c78d7b672)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1c56356c-9a63-4a8c-8dfe-2536a1c5b890)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/5c6ef1b6-30db-4969-9879-c782bbf4b27c)

**Lab #10: DOM XSS in document.write sink using source location.search**

This lab contains a DOM-based cross-site scripting vulnerability in the search query tracking functionality. It uses the JavaScript document.write function, which writes data out to the page. The document.write function is called with data from location.search, which you can control using the website URL.

To solve this lab, perform a cross-site scripting attack that calls the alert function.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/91f52dbd-b55c-47dc-a6ec-b9e6cd08ad65)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/fa4d0925-a114-4f17-8934-3ecb70c1a879)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/0c87f355-95c6-4a0f-bcdc-86e9d2f90419)


**Lab #12: Reflected XSS into a JavaScript string with angle brackets HTML encoded**

This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality where angle brackets are encoded. The reflection occurs inside a JavaScript string. To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function.

Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater.
Observe that the random string has been reflected inside a JavaScript string.
Replace your input with the following payload to break out of the JavaScript string and inject an alert:

'-alert(1)-'
Verify the technique worked by right clicking, selecting "Copy URL", and pasting the URL in the browser. When you load the page it should trigger an alert.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9a59536c-fc11-4ca3-b60a-1b9c217afd63)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/82b6fee4-a559-4f78-a064-416fa02d65c0)

**Lab #13: DOM XSS in document.write sink using source location.search inside a select element**

This lab contains a DOM-based cross-site scripting vulnerability in the stock checker functionality. It uses the JavaScript document.write function, which writes data out to the page. The document.write function is called with data from location.search which you can control using the website URL. The data is enclosed within a select element.

To solve this lab, perform a cross-site scripting attack that breaks out of the select element and calls the alert function.

![WhatsApp Image 2023-05-31 at 12 08 57](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4d8fa456-ca33-4d3b-8d83-f4b11fb005c7)

![WhatsApp Image 2023-05-31 at 12 09 26](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d09e90b3-baea-4c49-8fb5-4014a6ff5105)
