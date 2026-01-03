# What is SQL injection (SQLi)?
SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. This can allow an attacker to view data that they are not normally able to retrieve.
> In some situations, an attacker can escalate a SQL injection attack to compromise the underlying server or other back-end infrastructure. It can also enable them to perform denial-of-service attacks.

## How to detect SQL injection vulnerabilities
- The single quote character ``` ' ``` and look for errors or other anomalies.
- Some SQL-specific syntax that evaluates to the base (original) value of the entry point, and to a different value, and look for systematic differences in the application responses.
- Boolean conditions such as OR 1=1 and OR 1=2, and look for differences in the application's responses.
- Payloads designed to trigger time delays when executed within a SQL query, and look for differences in the time taken to respond.
- OAST payloads designed to trigger an out-of-band network interaction when executed within a SQL query, and monitor any resulting interactions.

## Retrieving hidden data
When the user clicks on the Gifts category, their browser requests the URL:
```
https://insecure-website.com/products?category=Gifts
```
> This causes the application to make a SQL query to retrieve details of the relevant products from the database:
```
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```
The restriction ``` released = 1 ``` is being used to hide products that are not released. We could assume for unreleased products, ``` released = 0 ```.

***Consider an example:***
```
https://insecure-website.com/products?category=Gifts'--
```
This results in SQL query as:
```
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
```
- ``` -- ``` is a comment indicator. This means anything after this will be treated as a comment and will be ignored.

You can use a similar attack to cause the application to display all the products in any category, including categories that they don't know about:
```
https://insecure-website.com/products?category=Gifts'+OR+1=1--
```
This results in SQL query as:
```
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```
***Warning***
```
Take care when injecting the condition OR 1=1 into a SQL query. Even if it appears to be harmless in the context you're
injecting into, it's common for applications to use data from a single request in multiple different queries.
If your condition reaches an UPDATE or DELETE statement, for example, it can result inan accidental loss of data.
```

# Lab-1: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
> This lab contains a SQL injection vulnerability in the product category filter. When the user selects a category, the application carries out a SQL query like the following:<br>
```
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```
> To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products.

## Solution:
- Accessed the lab and got usual dashboard.
- Selected a category and opened a product in it.
- Went to Burp and got a filter request of that category -> ``` filter?category=Accessories ```.
- Sent the current request and got the products in the server that were released on the server as Response.
- Modified the request by adding ``` '+OR+1=1-- ``` after Accessories and sent the request.

   <img width="1918" height="1193" alt="Screenshot 2025-12-31 173315" src="https://github.com/user-attachments/assets/d37caa48-b479-4f06-9e68-309c6eb9f5c0" />

- Got unreleased products displayed as Response and got the lab completed.

   <img width="1919" height="1198" alt="Screenshot 2025-12-31 173258" src="https://github.com/user-attachments/assets/42e98247-8882-4a1e-be14-31055a2023db" />

## Concepts Learned:
- Revised basic SQL injection.

## Wrong Tangents:
- Wasn't using ``` + ``` in my query, was writing ``` ' OR 1=1 ``` again and again and wondering why isn't workinng.
- Then went back to the theory and got to know ``` + ``` was the thing, I missed.

# Subverting application logic
If a user submits the username ``` wiener ``` and the password ``` bluecheese ```, the application checks the credentials by performing the following SQL query:
```
SELECT * FROM users WHERE username = 'wiener' AND password = 'bluecheese'
```

# Lab-2: SQL injection vulnerability allowing login bypass
> This lab contains a SQL injection vulnerability in the login function.<br>
To solve the lab, perform a SQL injection attack that logs in to the application as the ``` administrator ``` user.

## Solution:
- Accessed the lab and got usual dashboard.
- Went to ``` My Account ``` to login.
- In username, ran this query:
  ```
  administrator'--
  ```
- Typed any random thing in password field as it was a required field.

   <img width="1898" height="776" alt="Screenshot 2025-12-31 174857" src="https://github.com/user-attachments/assets/a1b59243-d762-446d-a3df-6ddaa15ccd10" />

- Loggen in successfully as administrator and completed the lab.

   <img width="1919" height="1199" alt="Screenshot 2025-12-31 174800" src="https://github.com/user-attachments/assets/d69c3817-0b77-4c75-b731-01e796eb3e0e" />

## Concepts  Learned:
- Revised basic SQL attack.






