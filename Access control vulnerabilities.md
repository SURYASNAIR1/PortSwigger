**Lab #1: Unprotected admin functionality**

This lab has an unprotected admin panel.

Solve the lab by deleting the user carlos.

Go to the lab and view robots.txt by appending /robots.txt to the lab URL. Notice that the Disallow line discloses the path to the admin panel.
In the URL bar, replace /robots.txt with /administrator-panel to load the admin panel.
Delete carlos.

![WhatsApp Image 2023-05-09 at 12 11 01](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/825ebf27-2c90-4492-bff1-557b5bcc70e9)

![WhatsApp Image 2023-05-09 at 12 12 05](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/db4d5427-048d-46da-a9e0-c3a7683e51b9)

![WhatsApp Image 2023-05-09 at 12 12 38](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9efef74b-29df-4f57-ae99-e3bdceb1933b)

**Lab #2: Unprotected admin functionality with unpredictable URL**

This lab has an unprotected admin panel. It's located at an unpredictable location, but the location is disclosed somewhere in the application.

Solve the lab by accessing the admin panel, and using it to delete the user carlos.

Review the lab home page's source using Burp Suite or your web browser's developer tools.
Observe that it contains some JavaScript that discloses the URL of the admin panel.
Load the admin panel and delete carlos.

![WhatsApp Image 2023-05-09 at 12 23 32](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1b9c395f-c0a8-424e-8172-feec2294da48)

![WhatsApp Image 2023-05-09 at 12 24 07](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f59421de-b08c-4488-8cec-f16a5692705c)

**Lab #3: User role controlled by request parameter**

This lab has an admin panel at /admin, which identifies administrators using a forgeable cookie.

Solve the lab by accessing the admin panel and using it to delete the user carlos.

You can log in to your own account using the following credentials: wiener:peter

Browse to /admin and observe that you can't access the admin panel.
Browse to the login page.
In Burp Proxy, turn interception on and enable response interception.
Complete and submit the login page, and forward the resulting request in Burp.
Observe that the response sets the cookie Admin=false. Change it to Admin=true.
Load the admin panel and delete carlos.
