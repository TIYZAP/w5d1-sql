# w5d1-sql

#How many users are there? = 50

sqlite> .tables
addresses          orders             users
items              schema_migrations

sqlite> SELECT * From users;

1|Axel|Robel|ludie_reynolds@schaden.net
2|Missouri|Carroll|darby@rohan.org
3|Fatima|Toy|bertrand@langrunolfsdottir.info
4|Devyn|Bode|naomie_hilpert@hettinger.com
5|Eldon|Aufderhar|samantha_haley@effertz.org
6|Kacie|Johns|muhammad.crooks@white.name
7|Leann|Runte|bryana.sauer@buckridge.biz
8|Judge|Frami|deangelo@okuneva.net
9|Shane|Dibbert|santiago@crooksbayer.info
10|Cloyd|Maggio|koby.jerde@ullrichsenger.biz
11|Phoebe|Kshlerin|juvenal.effertz@ryan.name
12|Vilma|McCullough|janae.mitchell@weinatbruen.biz
13|Mekhi|Lakin|sienna.skiles@kshlerin.com
14|Orland|Effertz|finn_mcglynn@hamill.info
15|Frida|Hauck|tianna@mann.name
16|Amina|Boehm|sarai_abernathy@gusikowski.biz
17|Caitlyn|Murazik|van.auer@bahringerschowalter.com
18|Devonte|Schoen|kendrick@binawayn.biz
19|Hassan|Runte|weston.kautzer@hoppe.biz
20|Kendrick|Ward|rick@hoeger.org
21|Felicity|Carroll|rashawn@quigley.biz
22|Jovan|McClure|miller@harrishalvorson.net
23|Brian|Dooley|leon_feeney@cummings.name
24|Julien|Pfeffer|camron@bergnaum.info
25|Cleta|Adams|stanford@kertzmann.org
26|Verner|Schiller|audrey@hartmann.org
27|Monserrate|Legros|maggie.anderson@spinka.name
28|Dewitt|Gutkowski|bart@armstrongconn.com
29|Kennedi|McLaughlin|amy.hagenes@damorewalker.org
30|Cole|Walker|elfrieda@rogahn.org
31|Shany|Hodkiewicz|ivah_jacobs@kshlerinmarks.name
32|Ursula|Macejkovic|isaac@dietrich.info
33|Sanford|Pagac|tyrique_oconnell@upton.net
34|Jayme|Waters|ellsworth_kuhn@rogahn.net
35|Flavio|Schinner|diana.bauch@hodkiewicz.biz
36|Jennie|Smith|vivien@grady.com
37|Dee|Balistreri|kaya@walker.net
38|Marshall|Franecki|hyman@hamill.org
39|Virginie|Mitchell|daisy.crist@altenwerthmonahan.biz
40|Corrine|Little|rubie_kovacek@grimes.net
41|Dakota|McGlynn|marjolaine@herzog.net
42|Cleo|Effertz|hilario@bergnaum.net
43|Kyra|Kilback|demarcus.predovic@grimes.org
44|Randi|Kirlin|craig.berge@sauerweimann.net
45|Kayden|DuBuque|gage.langworth@millsturcotte.net
46|Derrick|Cummerata|libby.langosh@hodkiewicz.com
47|Colton|Crooks|declan_mclaughlin@carroll.biz
48|Roselyn|Zboncak|jeyca@pfannerstill.com
49|Ignacio|Buckridge|chance@wiegand.name
50|Norene|Bartell|natalie@cainkeeling.biz

#What are the 5 most expensive items? =

`sqlite> SELECT * From items ORDER BY "Price" DESC;`


25|Small Cotton Gloves|Automotive, Shoes & Beauty|Multi-layered modular service-desk|9984
83|Small Wooden Computer|Health|Re-engineered fault-tolerant adapter|9859
100|Awesome Granite Pants|Toys & Books|Upgradable 24/7 access|9790
40|Sleek Wooden Hat|Music & Baby|Quality-focused heuristic info-mediaries|9390
60|Ergonomic Steel Car|Books & Outdoors|Enterprise-wide secondary firmware|9341

#What's the cheapest book? =

sqlite> SELECT * From items WHERE category LIKE '%Books%' ORDER BY "Price" ASC;

id|title|category|description|price

`76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496`

#Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?

sqlite> SELECT * From addresses WHERE street LIKE '%Zetta%';

id|user_id|street|city|state|zip

43|40|6439 Zetta Hills|Willmouth|WY|15029

sqlite> SELECT * From addresses WHERE user_id LIKE '%40%';

id|user_id|street|city|state|zip

`43|40|6439 Zetta Hills|Willmouth|WY|15029`
44|40|54369 Wolff Forges|Lake Bryon|CA|31587

id|first_name|last_name|email

`43|Kyra|Kilback|demarcus.predovic@grimes.org`

#Correct Virginie Mitchell's address to "New York, NY, 10108".

sqlite> SELECT * From users WHERE last_name = 'Mitchell';

id|first_name|last_name|email

39|Virginie|Mitchell|daisy.crist@altenwerthmonahan.biz

sqlite> SELECT * From addresses WHERE id = 39;

id|user_id|street|city|state|zip

39|37|7503 Cale Grove|Robertoshire|PA|49744

sqlite> UPDATE addresses SET city = 'New York' WHERE user_id = 37;

sqlite> SELECT * From addresses WHERE id = 39;

id|user_id|street|city|state|zip

39|37|7503 Cale Grove|New York|PA|49744

sqlite> UPDATE addresses SET state  = 'NY' WHERE user_id = 37;

sqlite> SELECT * From addresses WHERE id = 39;

id|user_id|street|city|state|zip

39|37|7503 Cale Grove|New York|NY|49744

sqlite> UPDATE addresses SET zip  = '10108' WHERE user_id = 37;


`sqlite> SELECT * From addresses WHERE id = 39;
id|user_id|street|city|state|zip
39|37|7503 Cale Grove|New York|NY|10108`


#How much would it cost to buy one of each tool?

sqlite> SELECT SUM (price) From items WHERE category LIKE '%Tool%';
`SUM (price)
46477`


#How many total items did we sell?

sqlite> SELECT SUM (quantity) From orders;
`SUM (quantity)
2125`


#How much was spent on books?

sqlite> SELECT SUM(orders.quantity * items.price) FROM orders INNER JOIN items ON (item_id = items.id) WHERE items.category LIKE '%book%';
`SUM(orders.quantity * items.price)
1081352`

#Simulate buying an item by inserting a User for yourself and an Order for that User.

`INSERT INTO users (first_name, last_name, email) VALUES ("Zachary", "Pinner", "zapinner@gmail.com");`
sqlite> SELECT * From users WHERE first_name = "Zachary";
id|first_name|last_name|email
51|Zachary|Pinner|zapinner@gmail.com


`INSERT INTO orders (user_id, item_id, quantity, created_at) VALUES ("51", "21", "5", "2016-02-08 00:00:00.000000");`
sqlite> SELECT * From orders WHERE user_id = 51;
id|user_id|item_id|quantity|created_at
378|51|21|5|2016-02-08 00:00:00.000000
