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

![image](https://user-images.githubusercontent.com/123303806/234771554-cad7c658-513a-4990-8b87-ae05ac0c91d2.png)

Below the category is closed with no string inside.
 
![image](https://user-images.githubusercontent.com/123303806/234771502-d21a78ad-1d1c-4cec-9df2-eed47106fe85.png)

![image](https://user-images.githubusercontent.com/123303806/234771253-13f8d8bc-3ecc-48c8-9730-c4659265bc73.png)

The above will result in internal server error.

Category is not existing string.

![image](https://user-images.githubusercontent.com/123303806/234770492-d6aa6e1b-02d2-4195-b032-5fa8d32e31c3.png)

![image](https://user-images.githubusercontent.com/123303806/234770546-879d2fb4-8221-4070-8788-7616cea19e67.png)

Always evaluates to true.-- indicates everything indicates after this is a comment.

![image](https://user-images.githubusercontent.com/123303806/234770911-e6547b7a-8884-4423-b6e6-505f8c293cc5.png)



