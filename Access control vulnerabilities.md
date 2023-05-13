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

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/3ca2a357-6f9a-4f8a-8627-e0719deb6cd7)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1cb4cad5-bb35-4e1a-a2ba-4efc8173cfbd)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/90e05622-6d0e-4ce2-a183-bde679c495d2)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4634a67b-faf2-43d9-aa06-72652dfae2fb)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/af0e339a-0c68-4619-8979-337d26345d2f)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/c2ffdacb-d88a-4d48-bd94-ce983cac4788)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f0a2d462-e56f-406b-9183-2b800e932da8)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b6f45abf-4be8-4e4d-a681-dff2656ae8f8)

**Lab #4: User role can be modified in user profile**

This lab has an admin panel at /admin. It's only accessible to logged-in users with a roleid of 2.

Solve the lab by accessing the admin panel and using it to delete the user carlos.

You can log in to your own account using the following credentials: wiener:peter.

Log in using the supplied credentials and access your account page.
Use the provided feature to update the email address associated with your account.
Observe that the response contains your role ID.
Send the email submission request to Burp Repeater, add "roleid":2 into the JSON in the request body, and resend it.
Observe that the response shows your roleid has changed to 2.
Browse to /admin and delete carlos.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/2fe8c073-df2b-4d0c-aa30-d66e01e1eb58)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/aa677078-d68d-43ca-afb8-424bcb0ada1f)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/ccd7cf25-6111-4357-8d25-e889cad1c2f6)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/3fe3d501-58b4-4621-9d18-05906b91b9fc)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/85c11cca-a7f7-4906-9134-95b7130227ab)

**Lab #5: User ID controlled by request parameter**

This lab has a horizontal privilege escalation vulnerability on the user account page.

To solve the lab, obtain the API key for the user carlos and submit it as the solution.

You can log in to your own account using the following credentials: wiener:peter.

Log in using the supplied credentials and go to your account page.
Note that the URL contains your username in the "id" parameter.
Send the request to Burp Repeater.
Change the "id" parameter to carlos.
Retrieve and submit the API key for carlos.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1c390a42-2233-4bbd-92c1-ae038643ce7d)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/53174ea8-8892-4971-88fc-47e4eda78cb9)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/994f407d-483e-4374-8db2-e4d5eaec56b0)

**Lab #6: User ID controlled by request parameter, with unpredictable user IDs**

This lab has a horizontal privilege escalation vulnerability on the user account page, but identifies users with GUIDs.

To solve the lab, find the GUID for carlos, then submit his API key as the solution.

You can log in to your own account using the following credentials: wiener:peter

Find a blog post by carlos.
Click on carlos and observe that the URL contains his user ID. Make a note of this ID.
Log in using the supplied credentials and access your account page.
Change the "id" parameter to the saved user ID.
Retrieve and submit the API key.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/18bcf60b-3824-441b-a1c9-6c535e84ebd8)

userId=d30bd329-041a-4065-82e6-21b543647070

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/0b6e6fb2-2f36-472d-aeda-e5d7709b6b52)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/da6415cb-2f04-443c-9f5f-e5ecd9f54c8b)
