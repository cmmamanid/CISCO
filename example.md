# Apuntes CISCO

**Ejemplo1** :

 ```sql
	 select * 	        from dual;
	 --Dummy
	 --x	 
	 select sysdate,user from dual;
	 --sysdate   |user
	 --15/05/2018|HR
 ```
 **Distinct | unique**
 
 - Son sinónimos
 - Retornan valores únicos
 - No ignoran campos `null`
 - Cuando mas de una columna o expresión están en el distinct retorna combinaciones únicas
 - Siempre debe ir despues de la sentencia `select`
 
 ```sql
