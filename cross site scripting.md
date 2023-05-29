**Lab #1: Reflected XSS into HTML context with nothing encoded**

This lab contains a simple reflected cross-site scripting vulnerability in the search functionality.

To solve the lab, perform a cross-site scripting attack that calls the alert function.

Copy and paste the following into the search box:

<script>alert(1)</script>
Click "Search".

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/88093769-3c4a-4ccc-85d2-59746230a02d)
