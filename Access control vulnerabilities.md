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

**Lab #7: User ID controlled by request parameter with data leakage in redirect**

This lab contains an access control vulnerability where sensitive information is leaked in the body of a redirect response.

To solve the lab, obtain the API key for the user carlos and submit it as the solution.

You can log in to your own account using the following credentials: wiener:peter

Log in using the supplied credentials and access your account page.
Send the request to Burp Repeater.
Change the "id" parameter to carlos.
Observe that although the response is now redirecting you to the home page, it has a body containing the API key belonging to carlos.
Submit the API key.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d47e5b8d-a694-4e26-ba93-3a0c319f077b)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d87a277c-24b0-4b49-be71-38fd537e6baa)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d128cd2b-a7c1-47c6-9870-2a06564cd0ba)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/74dc541b-f550-4bbc-8dc2-4c705d277d59)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/c01320e4-49d4-4fa2-b3c3-64cc9dad7092)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/3dc826f6-5efd-4746-a4b4-cf472418b277)

**Lab #8: User ID controlled by request parameter with password disclosure**

This lab has user account page that contains the current user's existing password, prefilled in a masked input.

To solve the lab, retrieve the administrator's password, then use it to delete carlos.

You can log in to your own account using the following credentials: wiener:peter

Log in using the supplied credentials and access the user account page.
Change the "id" parameter in the URL to administrator.
View the response in Burp and observe that it contains the administrator's password.
Log in to the administrator account and delete carlos.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/36478a5d-ca3e-4fd7-8a96-92b7d8ba8eb3)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/e866d424-c9d7-4ad7-8ccf-4849b34ad9b7)

**Lab #9: Insecure direct object references**

This lab stores user chat logs directly on the server's file system, and retrieves them using static URLs.

Solve the lab by finding the password for the user carlos, and logging into their account.

Select the Live chat tab.
Send a message and then select View transcript.
Review the URL and observe that the transcripts are text files assigned a filename containing an incrementing number.
Change the filename to 1.txt and review the text. Notice a password within the chat transcript.
Return to the main lab page and log in using the stolen credentials.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/8bdc1cc3-ab60-49a5-ad4b-a2b4f502c806)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/e24a0700-6791-45c3-b73e-12027c7fd920)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f8eb6be6-1247-4a7a-a052-337c00e5a089)

**Lab #10: URL-based access control can be circumvented**

This website has an unauthenticated admin panel at /admin, but a front-end system has been configured to block external access to that path. However, the back-end application is built on a framework that supports the X-Original-URL header.

To solve the lab, access the admin panel and delete the user carlos.

Try to load /admin and observe that you get blocked. Notice that the response is very plain, suggesting it may originate from a front-end system.
Send the request to Burp Repeater. Change the URL in the request line to / and add the HTTP header X-Original-URL: /invalid. Observe that the application returns a "not found" response. This indicates that the back-end system is processing the URL from the X-Original-URL header.
Change the value of the X-Original-URL header to /admin. Observe that you can now access the admin page.
To delete the user carlos, add ?username=carlos to the real query string, and change the X-Original-URL path to /admin/delete.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/fd0e85e9-9e6d-4290-a06b-4cb41db0be64)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/06ccc8bf-89a4-4364-b081-64b58c6581d7)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f65205be-0a47-4fa7-a889-c9f1b278a562)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d6e1e35b-4fe7-4669-8d66-f8870b4728f3)
