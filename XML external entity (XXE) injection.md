**Lab: Exploiting XXE using external entities to retrieve files**

This lab has a "Check stock" feature that parses XML input and returns any unexpected values in the response.

To solve the lab, inject an XML external entity to retrieve the contents of the /etc/passwd file.

Visit a product page, click "Check stock", and intercept the resulting POST request in Burp Suite.
Insert the following external entity definition in between the XML declaration and the stockCheck element:

<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
Replace the productId number with a reference to the external entity: &xxe;. The response should contain "Invalid product ID:" followed by the contents of the /etc/passwd file.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4b659553-dd2e-4d5c-841a-1cab3610b62a)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/a68a9acb-e875-4d12-87af-d7e5c8796230)
