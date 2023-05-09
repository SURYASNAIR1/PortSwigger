**Lab #1: OS command injection, simple case**

This lab contains an OS command injection vulnerability in the product stock checker.

The application executes a shell command containing user-supplied product and store IDs, and returns the raw output from the command in its response.

To solve the lab, execute the whoami command to determine the name of the current user.

Use Burp Suite to intercept and modify a request that checks the stock level.
Modify the storeID parameter, giving it the value 1|whoami.
Observe that the response contains the name of the current user.

![WhatsApp Image 2023-05-08 at 15 14 59](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/50318e69-526e-4929-a0a9-3a4127068cb1)

![WhatsApp Image 2023-05-08 at 15 16 28](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/fe9a14b0-c371-4f44-b300-1afa01fbc3db)

**Lab #2: Blind OS command injection with time delays**

This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response.

To solve the lab, exploit the blind OS command injection vulnerability to cause a 10 second delay.

Use Burp Suite to intercept and modify the request that submits feedback.
Modify the email parameter, changing it to:

email=x||ping+-c+10+127.0.0.1||

![WhatsApp Image 2023-05-08 at 15 39 07](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b46b1f1c-0f96-47ec-9791-c867b71ba66c)

![WhatsApp Image 2023-05-08 at 15 40 04](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/7f7bd698-c766-4b9f-be68-9e8a3abb5770)

**Lab #3: Blind OS command injection with output redirection**

This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response. However, you can use output redirection to capture the output from the command. There is a writable folder at:

/var/www/images/
The application serves the images for the product catalog from this location. You can redirect the output from the injected command to a file in this folder, and then use the image loading URL to retrieve the contents of the file.

To solve the lab, execute the whoami command and retrieve the output.

Use Burp Suite to intercept and modify the request that submits feedback.
Modify the email parameter, changing it to:

email=||whoami>/var/www/images/output.txt||
Now use Burp Suite to intercept and modify the request that loads an image of a product.
Modify the filename parameter, changing the value to the name of the file you specified for the output of the injected command:

filename=output.txt
Observe that the response contains the output from the injected command.

Observe that the response takes 10 seconds to return.

![WhatsApp Image 2023-05-08 at 15 47 44](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/c2211b39-1d7c-449c-8009-68a0f6d15653)

![WhatsApp Image 2023-05-08 at 21 32 25](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/cb318b94-0d01-4748-822e-379a8b830ed4)

![WhatsApp Image 2023-05-08 at 21 39 58](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/0b31994f-e8b7-4ee8-aba4-c4ea84b944cc)

![WhatsApp Image 2023-05-08 at 21 56 28](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/f40a1d95-fa72-430b-8cce-741b3ac84e72)

![WhatsApp Image 2023-05-08 at 21 57 12](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/2ae9d46d-2138-4076-9688-c28168f82458)

**Lab #4: Blind OS command injection with out-of-band interaction**

This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The command is executed asynchronously and has no effect on the application's response. It is not possible to redirect output into a location that you can access. However, you can trigger out-of-band interactions with an external domain.

To solve the lab, exploit the blind OS command injection vulnerability to issue a DNS lookup to Burp Collaborator.

Use Burp Suite to intercept and modify the request that submits feedback.
Modify the email parameter, changing it to:

email=x||nslookup+x.BURP-COLLABORATOR-SUBDOMAIN||
Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated in the modified email parameter.

![WhatsApp Image 2023-05-08 at 22 05 17](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/fdae3724-184c-4221-893a-4cd596f7bf89)

![WhatsApp Image 2023-05-08 at 22 22 26](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/ed33436a-ba01-4398-b803-d63af20905db)

![WhatsApp Image 2023-05-08 at 22 23 19](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/da13756a-d278-4206-ae2c-3ff396788e2c)
