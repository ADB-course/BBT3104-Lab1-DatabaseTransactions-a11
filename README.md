[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/r-tQZu0l)
# BBT3104-Lab1of6-DatabaseTransactions


| **Key**                                                               | Value                                                                                                                                                                              |
|---------------|---------------------------------------------------------|
| **Group Name**                                                               | ? |
| **Semester Duration**                                                 | 19<sup>th</sup> August - 25<sup>th</sup> November 2024                                                                                                                       |
Group A11
## Flowchart

/opt/lampp/htdocs/gitHub/ADB/BBT3104-Lab1-DatabaseTransactions-a11-main/image-1.png
![alt text](image-1.png)
![alt text](image.png)
![alt text](image-2.png)
![alt text](image-3.png)

## Pseudocode
BEGIN TRANSACTION

SET @orderNumber = MAX(orderNumber) + 1 FROM orders
INSERT INTO orders VALUES (@orderNumber, CURRENT_DATE, DATE_ADD(CURRENT_DATE, INTERVAL 3 DAY), DATE_ADD(CURRENT_DATE, INTERVAL 2 DAY), 'In Process', 145)

SAVEPOINT before_product_1
INSERT INTO orderdetails VALUES (@orderNumber, 'S18_1749', 2724, '136', 1)
UPDATE products SET quantityInStock = quantityInStock - 2724 WHERE productCode = 'S18_1749'

SAVEPOINT before_product_2
INSERT INTO orderdetails VALUES (@orderNumber, 'S18_2248', 540, '55.09', 2)
UPDATE products SET quantityInStock = quantityInStock - 540 WHERE productCode = 'S18_2248'

ROLLBACK TO SAVEPOINT before_product_2

SAVEPOINT before_product_3
INSERT INTO orderdetails VALUES (@orderNumber, 'S12_1099', 68, '95.34', 3)
UPDATE products SET quantityInStock = quantityInStock - 68 WHERE productCode = 'S12_1099'

INSERT INTO payments VALUES (145, 'JM555210', CURRENT_DATE, 300000)

COMMIT TRANSACTION
## Support for the Sales Departments' Report
Link Payments to Orders - Add a foreign key in the payments table that references orderNumber from the orders table to allow each payment record to be directly associated with an order.

Add Payment Status - Introduce a paymentStatus column in either the payments or orders table to indicate whether an order is fully paid or partially paid.
Possible values could include "Paid", "Partially Paid", and "Pending".

Track Total Amount Due - Maintain a totalAmount field in the orders table to store the total amount due for each order, allowing one to easily compute any remaining balance by subtracting total payments received from this amount.

Create a Report View - Create a view or report that joins orders, payments, and potentially other relevant tables to summarize which orders are unpaid or partially paid along with their respective balances, thus generating reports helping sales teams follow up with clients regarding outstanding payments effectively and efficiently.
