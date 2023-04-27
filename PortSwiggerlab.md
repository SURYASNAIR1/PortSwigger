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

**Lab #2 SQL injection vulnerability allowing login bypass**

Goal: Perform SQL attack and login as the administrator user.

SELECT firstname FROM user where username='admin' and password='admin'

![image](https://user-images.githubusercontent.com/123303806/234772974-4a526d65-4490-4ce4-bcf1-c6abdb8b581d.png)

User name is admin and password is admin.

![image](https://user-images.githubusercontent.com/123303806/234773131-77ebd11c-3cbe-47c9-9988-411d3ecda3ca.png)

The above is a non verbal generic error.User name is  invalid means the attacker would be able to enumerate usernames on the system and that's a vulnerability on its own.

![image](https://user-images.githubusercontent.com/123303806/234773260-372fada9-0b31-4234-ba75-6f09b809c4c3.png)

SELECT firstname FROM user where username=''' and password='admin'

If I try to add sql character as username and type any password and try to login it will show internal server error.Which means something happened at the back end that broke the application.Thus its a good indication that this is vulnerable to sql injection.The reason behind this is because this quote character interferedwith the query.

![image](https://user-images.githubusercontent.com/123303806/234773400-150e5652-7f98-4e38-85e8-73139d1b5b78.png)


SELECT firstname FROM user where username='admin'--' and password='admin'
 
![image](https://user-images.githubusercontent.com/123303806/234773480-a955a0ad-fd67-40bd-bdda-80c8e6970e46.png)

![image](https://user-images.githubusercontent.com/123303806/234773528-acd5960c-5957-4f89-9ff9-4a8d03e53143.png)

Because the user is not the admin here.

SELECT firstname FROM user where username='adminstrator'--'  and password='admin'

![image](https://user-images.githubusercontent.com/123303806/234773642-7a4a86f8-8f7b-407b-bebb-e236b4daa24b.png)

![image](https://user-images.githubusercontent.com/123303806/234773699-3abd6512-c642-4388-9cf9-13eead7b1a47.png)

![image](https://user-images.githubusercontent.com/123303806/234773767-ca717dcc-c296-4496-819d-d2b11f7f6172.png)

**Lab #3 SQLi UNION attack determining the number of columns returned by the query*

Extract information from the backend database.

SQLi-Product category filter

The way we wanna exploit this filter or this category parameter is by running a SQL injection union attack.sql injection union attack to extract information from the backend database. Determine the number of columns that are being returned by the query that filters on category and once we are done stop that.

Union attack returns an additional row containing null values.

End Goal: Determine the number of columns returned by the query.

Background Knowledge : How Union operator works.

![image](https://user-images.githubusercontent.com/123303806/234774260-642c992a-b1dd-4d35-8c61-ed841aa68950.png)

Suppose for example there contains two tables  table1 and table2.

Table1 has two columns a b and table2 has two columns c d and it contains values as listed in figure.

Here the UNION operator is concatenates the results of the two queries into a single result set.

![WhatsApp Image 2023-04-27 at 11 52 25](https://user-images.githubusercontent.com/123303806/234776901-d9516c85-4f69-452a-ad31-5fc375014a35.jpg)

Give me not only products in product table but also give me usernames and passwords from the users table.That allow me to extarct information from other tables that are used by the backend database.

Rule :

*The number and the order of the columns must be same in all queries.
*The data types must be compatible.

![image](https://user-images.githubusercontent.com/123303806/234779054-bb3d792b-d590-492e-ab38-60963aee66e8.png)

![image](https://user-images.githubusercontent.com/123303806/234779128-891824a7-6603-43ce-922c-58dcc6619cab.png)

![image](https://user-images.githubusercontent.com/123303806/234779349-529c0bb9-d05e-4b2c-8e67-700d1b9c7bfe.png)

![image](https://user-images.githubusercontent.com/123303806/234779403-003da14c-ba51-444c-a4f7-355d0fc3978b.png)

This shows that thee isn't only one column in the query.

https://0ac100c404344948849e7ce60068005c.web-security-academy.net/filter?category=Clothing%2c+shoes+and+accessories%27+UNION+SELECT+NULL,+NULL,NULL--

Add the above in the url as to solve the problem.

![image](https://user-images.githubusercontent.com/123303806/234789307-fc4ce8e8-ec92-4006-b685-35d8cba16cde.png)


