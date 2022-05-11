# Shopify-Fall-2022-Data-Science-Intern
Fall 2022 Data Science Intern Challenge 

# Question 1: Given some sample data, write a program to answer the following: click here to access the required data set

### Question 1 a) Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.  
### Answer  
We will solve this question in two approaches 
1. Recheck formula calculations 
2. Remove outliers

### $ Average\ order\ value\ (AOV)  = \frac{Total\ Revenue}{Number\ of\ orders} $

|     Average order value (AOV)    	|  Value  	|
|:--------------------------------:	|:-------:	|
|       Given (in question)        	| 3145.13 	|
|  Original data (correct formula) 	|  357.92 	|
| Cleaned data (removing outliers) 	|  307.01 	|

 - So what went wrong was that we were calculating the Average order value in the wrong way, we didn't take number of orders into consideration and directly calculated the mean

 - Outliers - <b>Shop_id = 78</b> is the causing discrepancies as it was charging $25,725 for a pair of shoes
 
<hr style="border:2px solid gray">
 
### Question 1 b) What metric would you report for this dataset?    
### Answer
<b>Revenue per visitor (RPV)</b>: Revenue per visitor combines both conversions and AOV to give the whole picture. RPV is deceptively simple – it tells you how much revenue each unique visitor is driving.

### $ Revenue\ per\ visitor\ (RPV)  = \frac{Total\ Revenue}{Total\ Unique\ Visitors} $

And along with that we can use Average order value (AOV)

<hr style="border:2px solid gray">


### Question 1 c) What is its value?  
### Answer
Value of Revenue per visitor (RPV) and Average order value (AOV) Metrics

|    Metrics    	| Revenue per visitor (RPV) 	| Average order value (AOV) 	|
|:-------------:	|:-------------------------:	|:-------------------------:	|
| Original Data 	|          52244.65         	|           357.92          	|
|  Cleaned Data 	|          44723.72         	|           307.01          	|

<hr style="border:2px solid gray">
<hr style="border:2px solid gray">

# Question 2:
For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.  
  
### Question 2 a) How many orders were shipped by Speedy Express in total?  
  
SELECT COUNT(OrderID) as  'Orders by Speedy Express' FROM Orders
WHERE ShipperID =
(SELECT ShipperID FROM Shippers
WHERE ShipperName = 'Speedy Express'); 
  
Answer = 54  

<hr style="border:2px solid gray">

### Question 2 b) What is the last name of the employee with the most orders?  
  
SELECT LastName 
FROM Employees  
WHERE EmployeeID = (SELECT EmployeeID FROM   
						(SELECT EmployeeID, COUNT(OrderID) 
                        FROM Orders 
                        GROUP BY EmployeeID 
                        ORDER BY COUNT(OrderID) DESC) 
                        Limit 1);  
    
Answer = Peacock    
  
<hr style="border:2px solid gray">
  
### Question 2 c) What product was ordered the most by customers in Germany?   
  
SELECT ProductName FROM Products  
WHERE ProductID IN 
  (SELECT ProductID FROM OrderDetails  
    WHERE OrderID IN (  
      SELECT OrderID FROM Orders  
      WHERE CustomerID IN (SELECT CustomerID FROM Customers  
      WHERE Country = 'Germany'))  
    GROUP BY ProductID  
    ORDER BY COUNT(OrderDetailID) DESC
    Limit 1);  
      
Answer =  "Gorgonzola Telino"
