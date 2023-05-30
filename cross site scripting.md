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

**Lab: Reflected XSS into attribute with angle brackets HTML-encoded**

This lab contains a reflected cross-site scripting vulnerability in the search blog functionality where angle brackets are HTML-encoded. To solve this lab, perform a cross-site scripting attack that injects an attribute and calls the alert function.

Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater.
Observe that the random string has been reflected inside a quoted attribute.
Replace your input with the following payload to escape the quoted attribute and inject an event handler:

"onmouseover="alert(1)
Verify the technique worked by right-clicking, selecting "Copy URL", and pasting the URL in the browser. When you move the mouse over the injected element it should trigger an alert.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1430bb24-42c4-4752-b8ac-90dcb781d7f9)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1b8d24cd-6fa7-4745-8510-d36b79c3a1bb)

**Lab: Reflected XSS into a JavaScript string with angle brackets HTML encoded**

This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality where angle brackets are encoded. The reflection occurs inside a JavaScript string. To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function.

Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater.
Observe that the random string has been reflected inside a JavaScript string.
Replace your input with the following payload to break out of the JavaScript string and inject an alert:

'-alert(1)-'
Verify the technique worked by right clicking, selecting "Copy URL", and pasting the URL in the browser. When you load the page it should trigger an alert.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9a59536c-fc11-4ca3-b60a-1b9c217afd63)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/82b6fee4-a559-4f78-a064-416fa02d65c0)
