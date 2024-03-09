# Project
PIZZA DATA -ANALYST

Analyzing pizza dataset find insight for business  
## using big query (sql) for this project  

                                         KPI

1- This Fisrt Qustion We are looking for total revenue ?

## total_revenue	
   817860.05	

CODE:
SELECT sum(total_price) as total_revenue FROM `angular-geode-401511.123.pizza sales` ;					

2- Avarge Order Value ?

   ## avg_order_value						
   38.3072623	
   
CODE:
SELECT sum(total_price)/count(distinct order_id) as avg_order_value FROM `angular-geode-401511.123.pizza sales` ;						
				
3- Total Pizza Sales ?

## total_pizza_sales						
49574		

CODE:
SELECT sum(quantity) as total_pizza_sales FROM `angular-geode-401511.123.pizza sales` ;						

4- Total Order ?
## total_oder						
   21350		

CODE:
SELECT count(distinct order_id) as total_oder FROM `angular-geode-401511.123.pizza sales` ;						

5- Avarage Pizza Sold Per Order
## avag_pizza_sold_perOrder								
  2.321967213		

CODE:
SELECT sum(quantity)/count(distinct order_id) as avag_pizza_sold_perOrder FROM `angular-geode-401511.123.pizza sales` ;								
								

                         MORE INSIGHT

6- Weekly & Hourly Total Pizza Sold ?

weekly hourly trend for total pizza sold		
"SELECT EXTRACT(WEEK FROM order_date) AS week_number,
       EXTRACT(year from order_date) AS order_year,
       COUNT(DISTINCT order_id) AS total_order
FROM `angular-geode-401511.123.pizza sales`
group by EXTRACT(WEEK FROM order_date) ,EXTRACT(year from order_date);


week_number	order_year	total_order
1	2015	202
2	2015	427
3	2015	401
4	2015	422
5	2015	393
6	2015	456
7	2015	421
8	2015	411
9	2015	397
10	2015	407
11	2015	417
12	2015	428
13	2015	410
14	2015	437
15	2015	405
16	2015	417
17	2015	431
18	2015	430
19	2015	393
20	2015	464
21	2015	404
22	2015	399
23	2015	418
24	2015	425
25	2015	407
26	2015	422
27	2015	478
28	2015	400
29	2015	425
30	2015	429
31	2015	428
32	2015	419
33	2015	440
34	2015	409
35	2015	401
36	2015	391
37	2015	433
38	2015	424
39	2015	275
40	2015	442
41	2015	344
42	2015	383
43	2015	352
44	2015	361
45	2015	401
46	2015	403
47	2015	394
48	2015	488
49	2015	415
50	2015	420
51	2015	429
52	2015	316
53	2015	206

				
7- Pizza Sales By Size ?
		
select pizza_size ,sum(total_price) as total_sales,sum(total_price) * 100 / (select sum(total_price) from `angular-geode-401511.123.pizza sales` ) as total_sales		
from `angular-geode-401511.123.pizza sales`		
group by pizza_size ;		
		
pizza_size	total_sales	  parcent
L	         375318.7	          45.89033295
M	         249382.25	        30.49204445
S	         178076.5	          21.77346846
XL     	   14076	            1.721076852
XXL	       1006.6	             0.1230772918

extra -
for 2 decimal after number big query code below

select pizza_size ,sum(total_price) as total_sales,round(sum(total_price) * 100 / (select sum(total_price) from `angular-geode-401511.123.pizza sales` ),2) as total_sales_percent
from `angular-geode-401511.123.pizza sales`
group by pizza_size ;


8- Pizza Category Wise Sales ?
#Resut Below		
			
			
pizza_name	total_price		
The Thai Chicken Pizza	43434.25		
The Barbecue Chicken Pizza	42768		
The California Chicken Pizza	41409.5		
The Classic Deluxe Pizza	38180.5		
The Spicy Italian Pizza	34831.25		
The Southwest Chicken Pizza	34705.75		
The Italian Supreme Pizza	33476.75		
The Hawaiian Pizza	32273.25		
The Four Cheese Pizza	32265.7		
The Sicilian Pizza	30940.5		
The Pepperoni Pizza	30161.75		
The Greek Pizza	28454.1		
The Mexicana Pizza	26780.75		
The Five Cheese Pizza	26066.5		
The Pepper Salami Pizza	25529		
The Italian Capocollo Pizza	25094		
The Vegetables + Vegetables Pizza	24374.75		
The Prosciutto and Arugula Pizza	24193.25		
The Napolitana Pizza	24087		
The Spinach and Feta Pizza	23271.25		
The Big Meat Pizza	22968		
The Pepperoni, Mushroom, and Peppers Pizza	18834.5		
The Chicken Alfredo Pizza	16900.25		
The Chicken Pesto Pizza	16701.75		
The Soppressata Pizza	16425.75		
The Italian Vegetables Pizza	16019.25		
The Calabrese Pizza	15934.25		
The Spinach Pesto Pizza	15596		
The Mediterranean Pizza	15360.5		
The Spinach Supreme Pizza	15277.75		
The Green Garden Pizza	13955.75		
The Brie Carre Pizza	11588.5		
			
			
			
SELECT pizza_name, round(sum(total_price),2) as total_price from `angular-geode-401511.123.pizza sales`			
group by pizza_name			
order by total_price desc;			
			

9- Top 7 Selling Pizza Category ?
	
	
SELECT pizza_name, round(sum(total_price),2) as total_revenue from `angular-geode-401511.123.pizza sales`	
group by pizza_name	
order by total_revenue desc	
limit 5;	


10 - Below Top 5 ?	
	
SELECT pizza_name, round(sum(total_price),2) as total_revenue from `angular-geode-401511.123.pizza sales`	
group by pizza_name	
order by total_revenue	
limit 5;	

11- Pizza Category Sales ?
	
select pizza_category ,sum(total_price) as total_sales,sum(total_price) * 100 / (select sum(total_price) from `angular-geode-401511.123.pizza sales`) as parcent		
from `angular-geode-401511.123.pizza sales`		
group by pizza_category ;		

**		
pizza_category	total_sales	parcent**
Classic	220053.1	26.90596026
Veggie	193690.45	23.68259093
Supreme	208197	25.45631126
Chicken	195919.5	23.95513756


12 - top 5 best pizza selling with respect to quantity ?	
	
pizza_name	total_quantity
The Classic Deluxe Pizza	2453
The Barbecue Chicken Pizza	2432
The Hawaiian Pizza	2422
The Pepperoni Pizza	2418
The Thai Chicken Pizza	2371

SELECT pizza_name, sum(quantity) as total_quantity from `angular-geode-401511.123.pizza sales`	
group by pizza_name	
order by total_quantity desc	
limit 5;	


13- below 5 best pizza selling quantity ?

SELECT pizza_name, sum(quantity) as total_quantity from `angular-geode-401511.123.pizza sales`
group by pizza_name
order by total_quantity
limit 5;


14- Best top 5 pizza order ?
		
SELECT pizza_name, count(distinct order_id) as total_order from `angular-geode-401511.123.pizza sales`		
group by pizza_name		
order by total_order desc		
limit 5;	


Row	pizza_name	total_order
1	The Classic Deluxe Pizza	2329
2	The Hawaiian Pizza	2280
3	The Pepperoni Pizza	2278
4	The Barbecue Chicken Pizza	2273
5	The Thai Chicken Pizza	2225

15- top 5 below pizza order	?		
			
SELECT pizza_name, count(distinct order_id) as total_order from `angular-geode-401511.123.pizza sales`			
group by pizza_name			
order by total_order			
limit 5;			
			
			
Row	pizza_name	total_order	
1	The Brie Carre Pizza	480	
2	The Mediterranean Pizza	912	
3	The Calabrese Pizza	918	
4	The Spinach Supreme Pizza	918	
5	The Chicken Pesto Pizza	938	

![image](https://github.com/AshrafXAsif/Project/assets/141871788/cc5c7c0a-97ec-4acc-a976-589d27a0df60)
