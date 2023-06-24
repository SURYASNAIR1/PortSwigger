**Lab #1: Basic SSRF against the local server**

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9879f816-f5c9-4206-b862-c2779b59dae0)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/a81f2f3d-b307-4a79-8edb-dc3d0c6d2534)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1b2e37fa-5369-4304-8137-2dcbe05e5fb7)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/0c1423c0-b89b-46b6-ac0a-5af08421afd2)


**Lab #2: Basic SSRF against another back-end system**

![WhatsApp Image 2023-06-06 at 11 24 47](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b256d9f2-bb8c-4687-ac7f-003a1c4185bd)

![WhatsApp Image 2023-06-06 at 11 27 28](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d175e301-fa31-40a4-8742-ec1ef986e80e)

![WhatsApp Image 2023-06-06 at 11 30 34](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4d864f86-f688-4c92-8100-ecea82de5908)

![WhatsApp Image 2023-06-06 at 11 35 51](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f62370ad-ca28-4abb-95d0-fc76b46a0d23)

![WhatsApp Image 2023-06-06 at 11 36 51](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/fd34af5d-88eb-400d-8b7f-e28c6a0869f6)

![WhatsApp Image 2023-06-06 at 11 35 20](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/88f4d0cc-4485-48e1-84e7-2a49afb90422)

**Lab #3: SSRF with blacklist-based input filter**

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/247aabf5-4673-48c6-a2b3-7e2844a348f0)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/c737a26c-c676-439c-9cd9-7644fd95f417)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/2856236f-df87-4fb7-adc8-40a3ea5e57ba)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/ff6f2aa7-95a2-490e-918f-128d9348c344)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/dc49ece3-51a8-4838-a9d8-bff3a434dacf)

**Lab #4:  SSRF with filter bypass via open redirection vulnerability**

Visit a product, click "Check stock", intercept the request in Burp Suite, and send it to Burp Repeater.
Try tampering with the stockApi parameter and observe that it isn't possible to make the server issue the request directly to a different host.
Click "next product" and observe that the path parameter is placed into the Location header of a redirection response, resulting in an open redirection.
Create a URL that exploits the open redirection vulnerability, and redirects to the admin interface, and feed this into the stockApi parameter on the stock checker:

/product/nextProduct?path=http://192.168.0.12:8080/admin
Observe that the stock checker follows the redirection and shows you the admin page.
Amend the path to delete the target user:

/product/nextProduct?path=http://192.168.0.12:8080/admin/delete?username=carlos
This lab has a stock check feature which fetches data from an internal system.

To solve the lab, change the stock check URL to access the admin interface at http://192.168.0.12:8080/admin and delete the user carlos.

The stock checker has been restricted to only access the local application, so you will need to find an open redirect affecting the application first.

![WhatsApp Image 2023-06-24 at 18 19 11](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/33c1e7c3-d724-4da2-a342-16c729a61c53)

![WhatsApp Image 2023-06-24 at 18 25 49](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/6cea9fbe-6d2a-454e-92e2-c7b3ff0292dd)

![WhatsApp Image 2023-06-24 at 18 26 44](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f57dc7f0-7456-458f-bc2a-9bbc41de95db)

![WhatsApp Image 2023-06-24 at 18 28 12](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/118bd0e3-0c54-411f-9c99-779afa0f68ca)

![WhatsApp Image 2023-06-24 at 18 29 58](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/419fe548-a0d7-460f-9ee9-1860bd49016b)

![WhatsApp Image 2023-06-24 at 18 33 09](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/c9ee9dea-2c65-4e24-b5bf-e0c501b94043)

![WhatsApp Image 2023-06-24 at 18 33 32](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d8e89447-54ea-4cae-bec7-450f4d7f9305)

**Lab: SSRF with whitelist-based input filter**

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/ee902922-b998-4720-a41d-d93a12b019bf)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4d73d62e-71c1-4e50-bdad-6f9805a09679)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/1cf52189-23ce-4b14-89ec-3d667c54c2f3)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/fbb75006-6678-4b0e-9c98-08d07b1c0263)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/ea54b593-5753-4492-b0aa-cef983fe8577)
