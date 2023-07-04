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

![WhatsApp Image 2023-06-25 at 10 00 24](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f458f094-603b-4bad-99c3-b66ca08078c4)

![WhatsApp Image 2023-06-25 at 10 01 00](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/516ecc48-b74b-42ce-b89c-f0581cbb2ac6)

![WhatsApp Image 2023-06-25 at 10 02 42](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/38cacc78-db38-439c-ba15-7415238194de)

![WhatsApp Image 2023-06-25 at 10 09 06](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/276708de-b458-4d6c-b6f2-5780f68ec6e2)

![WhatsApp Image 2023-06-25 at 10 09 45](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/fc8f1e9a-cedb-4a2e-8511-f474e71f00fc)

![WhatsApp Image 2023-06-25 at 10 21 08](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/45127378-943c-4740-ab4a-5beaa8e71df5)

**Lab: CSRF where token validation depends on request method**

This lab's email change functionality is vulnerable to CSRF. It attempts to block CSRF attacks, but only applies defenses to certain types of requests.

To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.

You can log in to your own account using the following credentials: wiener:peter

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/028dbff1-9c0d-4f54-97c2-adf0bd4ebb49)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/39a3e570-db45-4ec6-ba82-5f1f7343595d)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/876438ff-ca58-4ab9-807a-05fe1b0e5d16)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/3e91c758-0108-4b50-8e44-ff830198be09)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/974465f5-80a9-404a-a846-042e042da492)
