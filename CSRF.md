**Lab #1: CSRF vulnerability with no defenses**

This lab's email change functionality is vulnerable to CSRF.

To solve the lab, craft some HTML that uses a CSRF attack to change the viewer's email address and upload it to your exploit server.

You can log in to your own account using the following credentials: wiener:peter

Open Burp's browser and log in to your account. Submit the "Update email" form, and find the resulting request in your Proxy history.
If you're using Burp Suite Professional, right-click on the request and select Engagement tools / Generate CSRF PoC. Enable the option to include an auto-submit script and click "Regenerate".

Alternatively, if you're using Burp Suite Community Edition, use the following HTML template. You can get the request URL by right-clicking and selecting "Copy URL".

<form method="POST" action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="anything%40web-security-academy.net">
</form>
<script>
        document.forms[0].submit();
</script>
Go to the exploit server, paste your exploit HTML into the "Body" section, and click "Store".
To verify that the exploit works, try it on yourself by clicking "View exploit" and then check the resulting HTTP request and response.
Change the email address in your exploit so that it doesn't match your own.
Click "Deliver to victim" to solve the lab.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/0d5e0cfc-bca9-4179-8d97-06918ea58457)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/baf6c953-a169-4df6-affe-7de336c09028)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f8e3a349-b18c-418b-9a35-6cd83f7bcbad)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d9ad1e5d-e473-4d7e-a5ec-d89d5bdf90ed)
