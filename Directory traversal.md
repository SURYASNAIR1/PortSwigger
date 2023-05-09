**Lab #1: File path traversal, simple case**

This lab contains a file path traversal vulnerability in the display of product images.

To solve the lab, retrieve the contents of the /etc/passwd file.

Use Burp Suite to intercept and modify a request that fetches a product image.
Modify the filename parameter, giving it the value:

../../../etc/passwd
Observe that the response contains the contents of the /etc/passwd file.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/c326b0ec-4372-493e-a951-02182d553c63)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9cc0b252-494d-48a6-af75-584c3a052732)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/82dcf6a3-23fd-42c6-84be-01f396921186)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/adfe9a3e-4e4c-49c0-a8bf-770304d0eeac)

**Lab #2: File path traversal, traversal sequences blocked with absolute path bypass**

This lab contains a file path traversal vulnerability in the display of product images.

The application blocks traversal sequences but treats the supplied filename as being relative to a default working directory.

To solve the lab, retrieve the contents of the /etc/passwd file.

Use Burp Suite to intercept and modify a request that fetches a product image.
Modify the filename parameter, giving it the value /etc/passwd.
Observe that the response contains the contents of the /etc/passwd file.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/7bccde60-ec2c-4fc7-9ba8-ef33194713be)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/228818ba-93cb-4a4f-8022-cc1aef434e96)

![WhatsApp Image 2023-05-09 at 14 43 36](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/0102fbcf-cdd2-4160-a1bd-184c047a9526)

**Lab #3: File path traversal, traversal sequences stripped non-recursively**

This lab contains a file path traversal vulnerability in the display of product images.

The application strips path traversal sequences from the user-supplied filename before using it.

To solve the lab, retrieve the contents of the /etc/passwd file.

Use Burp Suite to intercept and modify a request that fetches a product image.
Modify the filename parameter, giving it the value:

....//....//....//etc/passwd
Observe that the response contains the contents of the /etc/passwd file.

**Lab #4: File path traversal, traversal sequences stripped non-recursively**

This lab contains a file path traversal vulnerability in the display of product images.

The application strips path traversal sequences from the user-supplied filename before using it.

To solve the lab, retrieve the contents of the /etc/passwd file.

Use Burp Suite to intercept and modify a request that fetches a product image.
Modify the filename parameter, giving it the value:

....//....//....//etc/passwd
Observe that the response contains the contents of the /etc/passwd file.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/bb8f65ad-cfd8-45ff-941e-2f6bd9d42167)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/929b157b-32b5-4884-aa9f-3a4c974b6b18)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/5dd61519-8d1a-4c82-a0a3-fa9139909c97)
