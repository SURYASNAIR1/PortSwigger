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

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/e7b3259e-d254-4ed5-a29a-8ae7fe89fe85)

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

**Lab #11: DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded**

This lab contains a DOM-based cross-site scripting vulnerability in a AngularJS expression within the search functionality.

AngularJS is a popular JavaScript library, which scans the contents of HTML nodes containing the ng-app attribute (also known as an AngularJS directive). When a directive is added to the HTML code, you can execute JavaScript expressions within double curly braces. This technique is useful when angle brackets are being encoded.

To solve this lab, perform a cross-site scripting attack that executes an AngularJS expression and calls the alert function.

Enter a random alphanumeric string into the search box.
View the page source and observe that your random string is enclosed in an ng-app directive.
Enter the following AngularJS expression in the search box:

{{$on.constructor('alert(1)')()}}
Click search.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/31c33455-d9c3-4674-b3b8-3955a426ce42)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9a36be84-4e7c-4d3e-91d1-3c5848439044)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/15e5c945-c6dc-4cfc-99dc-2a1c3673c714)

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

**Lab: Reflected DOM XSS**

This lab demonstrates a reflected DOM vulnerability. Reflected DOM vulnerabilities occur when the server-side application processes data from a request and echoes the data in the response. A script on the page then processes the reflected data in an unsafe way, ultimately writing it to a dangerous sink.

To solve this lab, create an injection that calls the alert() function.

In Burp Suite, go to the Proxy tool and make sure that the Intercept feature is switched on.
Back in the lab, go to the target website and use the search bar to search for a random test string, such as "XSS".
Return to the Proxy tool in Burp Suite and forward the request.
On the Intercept tab, notice that the string is reflected in a JSON response called search-results.
From the Site Map, open the searchResults.js file and notice that the JSON response is used with an eval() function call.
By experimenting with different search strings, you can identify that the JSON response is escaping quotation marks. However, backslash is not being escaped.
To solve this lab, enter the following search term:

\"-alert(1)}//
As you have injected a backslash and the site isn't escaping them, when the JSON response attempts to escape the opening double-quotes character, it adds a second backslash. The resulting double-backslash causes the escaping to be effectively canceled out. This means that the double-quotes are processed unescaped, which closes the string that should contain the search term.

An arithmetic operator (in this case the subtraction operator) is then used to separate the expressions before the alert() function is called. Finally, a closing curly bracket and two forward slashes close the JSON object early and comment out what would have been the rest of the object. As a result, the response is generated as follows:

{"searchTerm":"\\"-alert(1)}//", "results":[]}

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9dd62a34-8187-40a1-b564-b33d0ef704c0)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/5f422a3d-3433-4b7c-9cff-2e29d79a2619)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/dd90849b-23d7-4abe-add4-4b8d8e85fd11)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/e70d66c8-8ed9-4632-9cc1-c38377c2b02d)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/99640265-48b1-4ec0-a1fb-14fd4b682bb4)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/70eaa7b5-3697-4753-b5e9-68e8ebcf4100)

**Lab: Stored DOM XSS**

This lab demonstrates a stored DOM vulnerability in the blog comment functionality. To solve this lab, exploit this vulnerability to call the alert() function.

Post a comment containing the following vector:

<><img src=1 onerror=alert(1)>
In an attempt to prevent XSS, the website uses the JavaScript replace() function to encode angle brackets. However, when the first argument is a string, the function only replaces the first occurrence. We exploit this vulnerability by simply including an extra set of angle brackets at the beginning of the comment. These angle brackets will be encoded, but any subsequent angle brackets will be unaffected, enabling us to effectively bypass the filter and inject HTML.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/e4334f81-4c0c-421b-bf94-d9c4a0be3f7c)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1db781f9-2700-47ad-8f51-b5248257eab9)

**Lab: Reflected XSS into HTML context with most tags and attributes blocked**

This lab contains a reflected XSS vulnerability in the search functionality but uses a web application firewall (WAF) to protect against common XSS vectors.

To solve the lab, perform a cross-site scripting attack that bypasses the WAF and calls the print() function.

Inject a standard XSS vector, such as:

<img src=1 onerror=print()>
Observe that this gets blocked. In the next few steps, we'll use use Burp Intruder to test which tags and attributes are being blocked.
Open Burp's browser and use the search function in the lab. Send the resulting request to Burp Intruder.
In Burp Intruder, in the Positions tab, replace the value of the search term with: <>
Place the cursor between the angle brackets and click "Add §" twice, to create a payload position. The value of the search term should now look like: <§§>
Visit the XSS cheat sheet and click "Copy tags to clipboard".
In Burp Intruder, in the Payloads tab, click "Paste" to paste the list of tags into the payloads list. Click "Start attack".
When the attack is finished, review the results. Note that all payloads caused an HTTP 400 response, except for the body payload, which caused a 200 response.
Go back to the Positions tab in Burp Intruder and replace your search term with:

<body%20=1>
Place the cursor before the = character and click "Add §" twice, to create a payload position. The value of the search term should now look like: <body%20§§=1>
Visit the XSS cheat sheet and click "copy events to clipboard".
In Burp Intruder, in the Payloads tab, click "Clear" to remove the previous payloads. Then click "Paste" to paste the list of attributes into the payloads list. Click "Start attack".
When the attack is finished, review the results. Note that all payloads caused an HTTP 400 response, except for the onresize payload, which caused a 200 response.
Go to the exploit server and paste the following code, replacing YOUR-LAB-ID with your lab ID:

<iframe src="https://YOUR-LAB-ID.web-security-academy.net/?search=%22%3E%3Cbody%20onresize=print()%3E" onload=this.style.width='100px'>
Click "Store" and "Deliver exploit to victim".

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/bab973bc-6888-4764-b9cf-54a0bdd52333)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b495f566-87ac-4291-ae32-59a48e4ca3ba)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/a5005849-bfd0-43e6-9a29-3c4fe2d3039c)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b564d84e-9ed0-4491-81e2-2fcb99b7ce3e)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/ce9915e0-e93d-4468-a6dc-e696069722f0)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/76046dd2-ece3-4a77-acd5-f65e6a970d4e)

**Lab: Reflected XSS into HTML context with all tags blocked except custom ones**

This lab blocks all HTML tags except custom ones.

To solve the lab, perform a cross-site scripting attack that injects a custom tag and automatically alerts document.cookie.

Go to the exploit server and paste the following code, replacing YOUR-LAB-ID with your lab ID:

<script>
location = 'https://YOUR-LAB-ID.web-security-academy.net/?search=%3Cxss+id%3Dx+onfocus%3Dalert%28document.cookie%29%20tabindex=1%3E#x';
</script>
Click "Store" and "Deliver exploit to victim".
This injection creates a custom tag with the ID x, which contains an onfocus event handler that triggers the alert function. The hash at the end of the URL focuses on this element as soon as the page is loaded, causing the alert payload to be called.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/15bf7132-163a-4e07-b583-2c90631c8bf1)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/98cdeb01-b5c8-4622-97d8-9ce104a73041)

**Lab: Reflected XSS with some SVG markup allowed**

This lab has a simple reflected XSS vulnerability. The site is blocking common tags but misses some SVG tags and events.

To solve the lab, perform a cross-site scripting attack that calls the alert() function.

Inject a standard XSS payload, such as:

<img src=1 onerror=alert(1)>
Observe that this payload gets blocked. In the next few steps, we'll use Burp Intruder to test which tags and attributes are being blocked.
Open Burp's browser and use the search function in the lab. Send the resulting request to Burp Intruder.
In Burp Intruder, in the Positions tab, click "Clear §".
In the request template, replace the value of the search term with: <>
Place the cursor between the angle brackets and click "Add §" twice to create a payload position. The value of the search term should now be: <§§>
Visit the XSS cheat sheet and click "Copy tags to clipboard".
In Burp Intruder, in the Payloads tab, click "Paste" to paste the list of tags into the payloads list. Click "Start attack".
When the attack is finished, review the results. Observe that all payloads caused an HTTP 400 response, except for the ones using the <svg>, <animatetransform>, <title>, and <image> tags, which received a 200 response.
Go back to the Positions tab in Burp Intruder and replace your search term with:

<svg><animatetransform%20=1>
Place the cursor before the = character and click "Add §" twice to create a payload position. The value of the search term should now be:

<svg><animatetransform%20§§=1>
Visit the XSS cheat sheet and click "Copy events to clipboard".
In Burp Intruder, in the Payloads tab, click "Clear" to remove the previous payloads. Then click "Paste" to paste the list of attributes into the payloads list. Click "Start attack".
When the attack is finished, review the results. Note that all payloads caused an HTTP 400 response, except for the onbegin payload, which caused a 200 response.

Visit the following URL in the browser to confirm that the alert() function is called and the lab is solved:

https://YOUR-LAB-ID.web-security-academy.net/?search=%22%3E%3Csvg%3E%3Canimatetransform%20onbegin=alert(1)%3E

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/7086dee5-a1fb-460d-8d1f-fdc38dafdf6b)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/6adcf6a0-1234-4b6b-9069-b0b5ea57459b)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/cf2a9415-bd5e-4de7-b572-4592b8ac4758)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/80d3891b-3883-4ee1-96aa-242a4a31df56)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/a9ff6b87-bc4d-40d8-b722-9d918286c0cb)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/7b48c25c-f970-4b62-a54e-2a7b73f8f69d)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/c1920d35-106f-46a1-95b5-2374e09cbb5c)

**Lab: Reflected XSS in canonical link tag**

This lab reflects user input in a canonical link tag and escapes angle brackets.

To solve the lab, perform a cross-site scripting attack on the home page that injects an attribute that calls the alert function.

To assist with your exploit, you can assume that the simulated user will press the following key combinations:

ALT+SHIFT+X
CTRL+ALT+X
Alt+X

Visit the following URL, replacing YOUR-LAB-ID with your lab ID:

https://YOUR-LAB-ID.web-security-academy.net/?%27accesskey=%27x%27onclick=%27alert(1)
This sets the X key as an access key for the whole page. When a user presses the access key, the alert function is called.

To trigger the exploit on yourself, press one of the following key combinations:
On Windows: ALT+SHIFT+X
On MacOS: CTRL+ALT+X
On Linux: Alt+X

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9bf75ec3-130e-4ccb-936c-ee37de63ccf8)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/6a689200-decd-4f30-b5fe-796ee5140b38)

**Lab: Reflected XSS into a JavaScript string with single quote and backslash escaped**

This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality. The reflection occurs inside a JavaScript string with single quotes and backslashes escaped.

To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function.

Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater.
Observe that the random string has been reflected inside a JavaScript string.
Try sending the payload test'payload and observe that your single quote gets backslash-escaped, preventing you from breaking out of the string.
Replace your input with the following payload to break out of the script block and inject a new script:

</script><script>alert(1)</script>
Verify the technique worked by right clicking, selecting "Copy URL", and pasting the URL in the browser. When you load the page it should trigger an alert.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b9c52be0-b276-4b61-a4dd-ecc373ea7039)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/2eaccec2-f391-4f07-bd2a-2f740fc8c31c)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/67be6c85-cedb-4b9e-a8ba-0665f709b074)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/530ef4bc-e86a-4e26-94e7-e9c273a30db6)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/e47431da-d208-4612-8e6c-1772963fa66a)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/7011b4ec-c295-466d-b695-d1ee40fba95b)

**Lab: Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped**

This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality where angle brackets and double are HTML encoded and single quotes are escaped.

To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function.

Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater.
Observe that the random string has been reflected inside a JavaScript string.
Try sending the payload test'payload and observe that your single quote gets backslash-escaped, preventing you from breaking out of the string.
Try sending the payload test\payload and observe that your backslash doesn't get escaped.
Replace your input with the following payload to break out of the JavaScript string and inject an alert:

\'-alert(1)//
Verify the technique worked by right clicking, selecting "Copy URL", and pasting the URL in the browser. When you load the page it should trigger an alert.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/6efba89d-61a5-4607-81f2-83950eb20323)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/e8807670-d62b-4b62-94ec-87d48b7d1c32)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/3572ddac-c99d-4158-81cf-49dfaf1bde92)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/2bdc5c57-69e6-4ef5-b5c0-c73b012abb8b)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/7817a575-a50e-4dd8-a3c2-dd744e6efb54)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b207e89f-2e86-420d-9ca6-ed997710b149)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/cb4e93e8-de7c-4c80-a665-93ae7e4e96bb)

**Lab: Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped**

This lab contains a stored cross-site scripting vulnerability in the comment functionality.

To solve this lab, submit a comment that calls the alert function when the comment author name is clicked.

Post a comment with a random alphanumeric string in the "Website" input, then use Burp Suite to intercept the request and send it to Burp Repeater.
Make a second request in the browser to view the post and use Burp Suite to intercept the request and send it to Burp Repeater.
Observe that the random string in the second Repeater tab has been reflected inside an onclick event handler attribute.
Repeat the process again but this time modify your input to inject a JavaScript URL that calls alert, using the following payload:

http://foo?&apos;-alert(1)-&apos;
Verify the technique worked by right-clicking, selecting "Copy URL", and pasting the URL in the browser. Clicking the name above your comment should trigger an alert.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/c86c30d6-49d7-4c71-90e9-332924e41b09)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/5797fb25-64e5-4ab3-a8ab-e498bf6c1433)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/e59fd7b8-fc04-45a1-913b-b12d75ca277c)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f3117f3a-9f70-46f9-9a78-60fb2f35f2e5)

**Lab: Reflected XSS into a template literal with angle brackets, single, double quotes, backslash and backticks Unicode-escaped**

This lab contains a reflected cross-site scripting vulnerability in the search blog functionality. The reflection occurs inside a template string with angle brackets, single, and double quotes HTML encoded, and backticks escaped. To solve this lab, perform a cross-site scripting attack that calls the alert function inside the template string.

Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater.
Observe that the random string has been reflected inside a JavaScript template string.
Replace your input with the following payload to execute JavaScript inside the template string: ${alert(1)}
Verify the technique worked by right clicking, selecting "Copy URL", and pasting the URL in the browser. When you load the page it should trigger an alert.
