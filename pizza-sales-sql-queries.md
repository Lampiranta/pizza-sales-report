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
```
| Order Day | Total Orders |
|-----------|--------------|
| February  | 1685         |
| August    | 1841         |
| June      | 1773         |
| April     | 1799         |
| December  | 1680         |
| January   | 1845         |
| September | 1661         |
| May       | 1853         |
| October   | 1646         |
| November  | 1792         |
| March     | 1840         |
| July      | 1935         |

3. Percentage of sales by pizza category:
```SQL
SELECT
```

4. Percentage of sales by pizza size:
```SQL
SELECT
```

5. Total pizzas sold by pizza category:
```SQL
SELECT
```

6. Top 5 best sellers by revenue, total quantity and total orders:
```SQL
SELECT
```

7. Bottom 5 best sellers by revenue, total quantity and total orders:
```SQL
SELECT
```
