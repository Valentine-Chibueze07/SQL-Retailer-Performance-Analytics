# SQL-Retailer-Performance-Analytics
SQL Retailer Performance Analytics 

**Overview**

This project focuses on analyzing retailer performance using SQL Server.

The objective was to simulate real commercial operations by evaluating:

Credit allocation

Order activity

Channel segmentation

State-level performance

Order statistics via views

All analysis was implemented in T-SQL (SQL Server).

**Business Questions Answered**

Which retailers have the highest credit limits?

How many retailers exist per distribution channel?

Which retailers have never placed an order?

What is the latest order activity for HoReCa retailers in Abuja?

What is the total and delivered GMV per retailer?

**Technical Skills Demonstrated**

CRUD Operations (INSERT, UPDATE, DELETE)

INNER JOIN / LEFT JOIN

GROUP BY & HAVING

Aggregate Functions (SUM, COUNT, AVG)

Filtering with conditions

View creation (vw_RetailerOrderStats)

Business rule implementation

NULL handling

Data validation logic

 **Sample SQL Highlights**
✔ Top 20 Retailers by Credit Limit
SELECT TOP 20 BusinessName, CreditLimit
FROM Retailers
ORDER BY CreditLimit DESC;

✔ Retailers Who Never Placed Orders
SELECT R.BusinessName
FROM Retailers R
LEFT JOIN SalesOrders S
    ON R.RetailerID = S.RetailerID
WHERE S.OrderID IS NULL;

✔ View Creation
CREATE VIEW vw_RetailerOrderStats AS
SELECT
    R.RetailerID,
    R.BusinessName,
    COUNT(S.OrderID) AS TotalOrders,
    SUM(CASE WHEN S.Status = 'Delivered' THEN 1 ELSE 0 END) AS DeliveredOrders,
    SUM(CASE WHEN S.Status = 'Delivered' THEN S.NetAmount ELSE 0 END) AS DeliveredGMV
FROM Retailers R
LEFT JOIN SalesOrders S
    ON R.RetailerID = S.RetailerID
GROUP BY R.RetailerID, R.BusinessName;

 **Key Business Insights**

Identified inactive retailers (zero orders)

Measured revenue contribution per channel

Monitored HoReCa performance in Abuja (FCT)

Evaluated credit exposure across states

Built reusable performance view for dashboards.


