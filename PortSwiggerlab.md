                                                           **PORTSWIGGER LAB**
**Name : SURYA S NAIR**

**Roll Number : CB.EN.P2CYS22007**

PortSwigger offers tools for web application security, testing, & scanning.

**Lab #1 SQL injection vulnerability in WHERE clause allowing retrieval of hidden data**

Goal : Retrieve the hidden data.

Web App is a shopping application is shown here.

![image](https://user-images.githubusercontent.com/123303806/234769271-9d9e63f6-691d-4299-bdaa-e311d2af7057.png)

Refine your search option is also there.

If we select  clothing,shoes and accessories from the category , we will get the below url .

![image](https://user-images.githubusercontent.com/123303806/234769430-2fdb0cad-5969-4ea3-9426-f95f29452a4d.png)

Category with the value set to accessories.

![image](https://user-images.githubusercontent.com/123303806/234769567-d1345066-3568-4585-b3b7-2964b8d30712.png)

Select all the columns from the table of products where category =Accessories  AND released =1

To find hidden data , Set released to zero and to one so as to see the whole product.

![image](https://user-images.githubusercontent.com/123303806/234769687-4ea32ab1-1c1a-4063-923b-3f5db6f01155.png)

Below the category is closed with no string inside.
 
![image](https://user-images.githubusercontent.com/123303806/234769806-762651e3-6b9c-49f4-b76e-5a1fc08d8e0c.png)

![image](https://user-images.githubusercontent.com/123303806/234769942-29988eb8-f279-4fde-979f-2e162720505c.png)
