# PIZZA SALES SQL QUERIES

## A. KPI's

1. Total Revenue:
```SQL
SELECT SUM(total_price) AS [Total Revenue] FROM pizza_sales;
```
| Total Revenue   |
|-----------------|
| 817860.05083847 |

2. Average Order Value:
```SQL  
SELECT SUM(total_price)/COUNT(DISTINCT order_id) AS [Average Order Value] FROM pizza_sales;
```
| Average Order Value |
|---------------------|
| 38.3072623343546    |
 
3. Total Pizzas Sold:
```SQL
SELECT SUM(quantity) AS [Total Pizzas Sold] FROM pizza_sales;
```
| Total Pizzas Sold |
|-------------------|
| 49574             |
   
4. Total Orders:
```SQL
SELECT COUNT(DISTINCT order_id) AS [Total Orders] FROM pizza_sales;
```
| Total Orders |
|--------------|
| 21350        |
   
5. Average Pizzas Per Order:
```SQL
SELECT CAST(SUM(quantity) AS DECIMAL(10,2)) /
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) 
AS [Average Pizzas Per Order] FROM pizza_sales;
```
| Average Pizzas Per Order |
|--------------------------|
| 2.3219672131147          |

## B. CHARTS

1. Daily trend for total orders:
```SQL
SELECT DATENAME(DW, order_date) as [Order Day], COUNT(DISTINCT order_id) AS [Total Orders] 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)
ORDER BY 
     CASE DATENAME(DW, order_date)
      WHEN 'Monday' THEN 1
      WHEN 'Tuesday' THEN 2
      WHEN 'Wednesday' THEN 3
      WHEN 'Thursday' THEN 4
      WHEN 'Friday' THEN 5
      WHEN 'Saturday' THEN 6
      WHEN 'Sunday' THEN 7
     END ASC
```
| Order Day | Total Orders |
|-----------|--------------|
| Monday    | 2794         |
| Tuesday   | 2973         |
| Wednesday | 3024         |
| Thursday  | 3239         |
| Friday    | 3538         |
| Saturday  | 3158         |
| Sunday    | 2624         |

2. Monthly trend for total orders:
```SQL
SELECT DATENAME(M, order_date) as [Order Day], 
COUNT(DISTINCT order_id) AS [Total Orders] 
FROM pizza_sales
GROUP BY DATENAME(M, order_date)
ORDER BY COUNT(DISTINCT order_id) DESC
```
| Order Day | Total Orders |
|-----------|--------------|
| July      | 1935         |
| May       | 1853         |
| January   | 1845         |
| August    | 1841         |
| March     | 1840         |
| April     | 1799         |
| November  | 1792         |
| June      | 1773         |
| February  | 1685         |
| December  | 1680         |
| September | 1661         |
| October   | 1646         |

3. Percentage of sales by pizza category:
```SQL
SELECT pizza_category as [Pizza gategory],  
(SUM(total_price)/(SELECT SUM(total_price) FROM pizza_sales))*100 as [Percentage of Sales]
FROM pizza_sales
GROUP BY pizza_category
```
| Pizza gategory | Percentage of Sales |
|----------------|---------------------|
| Classic        | 26.9059602306976    |
| Chicken        | 23.9551375322885    |
| Veggie         | 23.6825910258677    |
| Supreme        | 25.4563112111462    |

4. Percentage of sales by pizza size:
```SQL
SELECT pizza_size as [Pizza size],  
(SUM(total_price)/(SELECT SUM(total_price) FROM pizza_sales))*100 as [Percentage of Sales]
FROM pizza_sales
GROUP BY pizza_size
Order by SUM(total_price) DESC
```
| Pizza size | Percentage of Sales |
|------------|---------------------|
| L          | 45.8903330244889    |
| M          | 30.492044420599     |
| S          | 21.7734684107037    |
| XL         | 1.72107684995364    |
| XXL        | 0.123077294254725   |

5. Total pizzas sold by pizza category:
```SQL
SELECT pizza_category as [Pizza Category],  
SUM(quantity) as [Pizzas Sold]
FROM pizza_sales
GROUP BY pizza_category
ORDER BY SUM(quantity) DESC
```
| Pizza Category | Pizzas Sold       |
|----------------|-------------------|
| Classic        | 14888             |
| Supreme        | 11987             |
| Veggie         | 11649             |
| Chicken        | 11050             |

6. Top 5 best sellers by revenue, total quantity and total orders:
```SQL
SELECT TOP 5 pizza_name as [Pizza Name],
SUM(total_price) as [Revenue],
SUM(quantity) as [Total Quantity],
COUNT(DISTINCT order_id) as [Total Orders]
FROM pizza_sales
GROUP BY pizza_name
ORDER BY SUM(total_price) DESC
```
| Pizza Name                   | Revenue  | Total Quantity | Total Orders |
|------------------------------|----------|----------------|--------------|
| The Thai Chicken Pizza       | 43434.25 | 2371           | 2225         |
| The Barbecue Chicken Pizza   | 42768    | 2432           | 2273         |
| The California Chicken Pizza | 41409.5  | 2370           | 2197         |
| The Classic Deluxe Pizza     | 38180.5  | 2453           | 2329         |
| The Spicy Italian Pizza      | 34831.25 | 1924           | 1822         |

7. Bottom 5 best sellers by revenue, total quantity and total orders:
```SQL
SELECT TOP 5 pizza_name as [Pizza Name],
SUM(total_price) as [Revenue],
SUM(quantity) as [Total Quantity],
COUNT(DISTINCT order_id) as [Total Orders]
FROM pizza_sales
GROUP BY pizza_name
ORDER BY SUM(total_price) ASC
```
| Pizza Name                | Revenue          | Total Quantity | Total Orders |
|---------------------------|------------------|----------------|--------------|
| The Brie Carre Pizza      | 11588.4998130798 | 490            | 480          |
| The Green Garden Pizza    | 13955.75         | 997            | 976          |
| The Spinach Supreme Pizza | 15277.75         | 950            | 918          |
| The Mediterranean Pizza   | 15360.5          | 934            | 912          |
| The Spinach Pesto Pizza   | 15596            | 970            | 945          |
