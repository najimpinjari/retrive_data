# how-to-retreve-the-data-using-three-different-tables-in-SQL
To retrieve the three tables or there values  you can use the following SQL query

fist af all we create three tables 1.customers1  2.product1  3.order1 okey as follow

create table product1 (
id int primary key,
name varchar(50),
unitprice int 
)
go
insert into product1 values (1,'TV', 450),(2,'LAPTOP',500),(3,'DESKTOP',1000)

SELECT * FROM product1

create table Customer1 (
	custId int primary key,
	custname varchar(50)
) 
insert into Customer1 values (1, 'ASHIS'),(2,'RITESH'),(3,'JYOTI'),(4,'ARCHNA'),(5,'SATISH')


CREATE table order1(
orderid int ,
productid int foreign key references product1(id),
custid int foreign key references customer1(custId),
quantity int  
) go 

insert into order1 values(1,1,1,10), (2,1,2,15),(3,2,3,5),(4,3,2,1)     ,  analize this tables i give you some question i want the answer of my question 
ChatGPT
Certainly, let's analyze the tables and answer your questions.

Product1 Table:

diff
Copy code
+----+----------+-----------+
| id |   name   | unitprice |
+----+----------+-----------+
| 1  | TV       | 450       |
| 2  | LAPTOP   | 500       |
| 3  | DESKTOP  | 1000      |
+----+----------+-----------+
Customer1 Table:

diff
Copy code
+--------+----------+
| custId | custname |
+--------+----------+
| 1      | ASHIS    |
| 2      | RITESH   |
| 3      | JYOTI    |
| 4      | ARCHNA   |
| 5      | SATISH   |
+--------+----------+
Order1 Table:

diff
Copy code
+--------+-----------+--------+----------+
| orderid| productid | custid | quantity |
+--------+-----------+--------+----------+
| 1      | 1         | 1      | 10       |
| 2      | 1         | 2      | 15       |
| 3      | 2         | 3      | 5        |
| 4      | 3         | 2      | 1        |
+--------+-----------+--------+----------+


question ; Retreve all customer names with product name and total price [ consider only those customers who has brought product ]
answer with explanation =

To retrieve all customer names with their associated product names and the total price, considering only those customers who have bought products, you can use the following SQL query:

sql
Copy code
SELECT c.custname, p.name as product_name, SUM(o.quantity * p.unitprice) as total_price
FROM Customer1 c
JOIN order1 o ON c.custId = o.custid
JOIN Product1 p ON o.productid = p.id
GROUP BY c.custname, p.name;
Explanation of the query:

The SELECT statement selects the customer name (c.custname), product name (p.name), and the sum of the total price of each product (SUM(o.quantity * p.unitprice)).

The FROM clause specifies the tables used in the query: Customer1, order1, and Product1.

The JOIN keyword is used to join the tables based on the specified conditions. Here, we join the Customer1 table with the order1 table on the condition c.custId = o.custid, and then join the order1 table with the Product1 table on the condition o.productid = p.id.

The GROUP BY clause groups the result set by customer names (c.custname) and product names (p.name), which allows the aggregation function SUM to calculate the total price for each combination of customer and product.

This query will provide you with the customer names, the names of the products they purchased, and the total price for each product, considering only the customers who have bought products.


