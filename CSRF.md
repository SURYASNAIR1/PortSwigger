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

**Lab: CSRF where token validation depends on token being present**

This lab's email change functionality is vulnerable to CSRF.

To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.

You can log in to your own account using the following credentials: wiener:peter

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4dc3ea4d-7e1f-4cb6-a066-132eb539c1ef)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/efc06d94-69c4-4636-98ca-811043b4aefb)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/0e0c5d4a-82a7-4a6d-9a96-20b566bbe1b6)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f95b883f-6c82-419f-ac58-4d624ac39cc7)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f9a083c7-ca09-419f-950a-ad564558a781)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/3d75ad9b-19ff-4943-9288-11b2c10fa5a7)

**Lab: CSRF where token is not tied to user session**

This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF attacks, but they aren't integrated into the site's session handling system.

To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.

You have two accounts on the application that you can use to help design your attack. The credentials are as follows:

wiener:peter
carlos:montoya

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/6a522a69-d33c-4d51-92dd-02006f9c6520)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/09c780e4-6bd1-4021-bd6c-0330e16a1522)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/acc6e110-a39a-4d0a-80b4-c40f6cc9fc46)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/a732fea6-d512-425a-abc0-d92f6e9f63aa)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1dd0ff1b-3f11-4d59-8632-164ec7af5c1b)
