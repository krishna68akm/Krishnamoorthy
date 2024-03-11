

                         PIZZA SALES (SQL QUEIRES)

  KEY PERFORMANCE INDICATOR:

1. Total Revenue:
SELECT SUM(total_price) AS Total_Revenue 
FROM pizza_sales;

OUTPUT:
        Total Revenue:
           817860.05083847


2. Average Order Value:
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales

OUTPUT:
        Average Order Value:
            38.3072623343546


3. Total Pizzas Sold:
SELECT SUM(quantity) AS Total_pizza_sold 
FROM pizza_sale

OUTPUT:
        Total Pizzas Sold:
              49574


4. Total Orders:
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sale                                      
                
OUTPUT:
         Total Orders:  
                21350


5. Average Pizzas Per Order:
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales
                                                   
OUTPUT:
          Average Pizzas Per Order:
                   2.32



   TRENDS AND SALES REPORT:

A) DAILY TRENDS FOR TOTAL ORDERS:
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)

Output:
      DAILY TRENDS FOR TOTAL ORDERS:
        Order_Day           Total_Orders
1)       Monday              2794
2)       Tuesday             2973
3)       Wednesday           3024
4)       Thursday            3239
5)       Friday              3538
6)       Saturday            3158
7)       Sunday              2624

   

B) MONTH TRENDS FOR ORDERS:
select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
from pizza_sales
GROUP BY DATENAME(MONTH, order_date)

Output:
        MONTH TRENDS FOR ORDERS:
         Month_Name         Total_Orders
1)        February            1685
2)        June                1773
3)        August              1841
4)        April               1799
5)        May                 1853
6)        December            1680
7)        January             1845
8)        September           1861
9)        October             1646
10)       July                1935
11)       November            1792
12)       March               1840 



C) PERCENTAGE OF SALES BY PIZZA CATEGORY:
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category

Output:
        PERCENTAGE OF SALES BY PIZZA CATEGORY:
         Pizza_Category        Total_Revenue        PCT
1)       Classic                 220053.10           26.91
2)       Chicken                 195919.50           23.96
3)       veggie                  193690.45           23.68
4)       Supreme                 208197.00           25.46
           


D) PERCENTAGE OF SALES BY PIZZA SIZE:
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size

Output:
        PERCENTAGE OF SALES BY PIZZA SIZE:         
         Pizza_Size           Total_Revenue        PCT
1)        L                     375318.70           45.89
2)        XL                    249.382.25          30.49
3)        S                     178076.50           21.77
4)        XL                    14076.00            1.72
5)        XXL                   1006.00             0.12



E) TOTAL PIZZA SOLD BY PIZZA CATEGORY:
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC

Output:
         TOTAL PIZZA SOLD BY PIZZA CATEGORY:
           Pizza_Category          Total_Quantity_sold
1)          Classic                 14888
2)          Supreme                 11987
3)          Veggie                  11649
4)          Chicken                 11060
   


F) TOP 5 PIZZA BY REVENUE:
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC

Output:
         TOP 5 PIZZA BY REVENUE:
              Pizza_Name                  Total_Revenue
1)         Thai Chicken Pizza              43434.25
2)         Barbecue Chicken Pizza          42786
3)         California Chicken Pizza        41409.5
4)         Classic Deluxe Plaza            38180.5
5)         Spicy Italian Plaza             34381.25

            

G) BOTTOM 5 PIZZA BY REVENUE:
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC

Output:
        BOTTOM 5 PIZZA BY REVENUE:
          Pizza_Name                  Total_Revenue
1)         Brie Carre Pizza             11588.4998130798
2)         Green Garden Pizza           13955.75
3)         Spinach Supreme Pizza        15277.75
4)         Mediterranean Pizza          15360.5
5)         Spinach Pesto Pizza          15596
                             


H) TOP 5 PIZZA BY QUANTITY:
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
Output:
        TOP 5 PIZZA BY QUANTITY:
          Pizza_Name                Total_Pizza_Sold
1)         Classic Deluxe Plaza       2453
2)         Barbecue Chicken Pizza     2432
3)         Hawaiian Pizza             2422
4)         Pepperoni Pizza            2418
5)         Thai Chicken Pizza         2371
   


I) BOTTOM 5 PIZZA BY QUANTITY:
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC

Output:
          BOTTOM 5 PIZZA BY QUANTITY:
            Pizza_Name                Total_Pizza_Sold
1)           Brie Carre Pizza          490
2)           Mediterranean Pizza       934
3)           Calabrese Pizza           937
4)           Spinach Superme Pizza     950
5)           Soppressata Pizza         961



J) TOP 5 PIZZA BY TOTAL ORDER:
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC

Output:
        TOP 5 PIZZA BY TOTAL ORDER:
           Pizza_Name                   Total_Order
1)          Classic Deluxe Plaza          2239
2)          Hawaiian Pizza                2280
3)          Pepperoni Pizza               2278
4)          Barbecue Chicken Pizza        2273
5)          Thai Chicken Pizza            2225

           
        
K) BOTTOM 5 PIZZA BY TOTAL ORDER:
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC

Output:
        BOTTOM 5 PIZZA BY TOTAL ORDER:
          Pizza_Name                   Total_Order
1)         Brie Carre Pizza              480
2)         Mediterranean Pizza           912
3)         Spinach Superme Pizza         918
4)         Calabrese Pizza               918
5)         Chicken Pesto Pizza           938
        
 



