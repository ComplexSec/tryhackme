#  TryHackMe - OWASP Juice Shop (Room 007)

<details><summary>Task 2.1 to 2.3</summary>
<p>

## Task 2.1

### Q: What is the administrator's email address?

A: admin@juice-sh.op

Walkthrough: Look through the reviews and the emails attached to the reviews. A good guess for the one ending in `in@juice-sh.op` is the admin account

![](/OWASP%20Juice%20Shop/images/admin_email.png)

Can also check product reviews which reveal the full email address of the reviewer. On the `Apple Juice` product, we can see the admin email address

![](/OWASP%20Juice%20Shop/images/admin_email2.png)

## Task 2.2

### Q: What parameter is used for searching?

A: q

Walkthrough: Search for a product using the search function and the URL will reveal the parameter used

![](/OWASP%20Juice%20Shop/images/q.png)

## Task 2.3

### Q: What show does Jim reference in his review?

A: Star Trek

Walkthrough: Checking through more reviews of the products, we can see a review by `jim@juice-sh.op` referencing the Starfleet symbol. Googling this symbol reveals it is from the Star Trek universe

![](/OWASP%20Juice%20Shop/images/jim_startrek.png)

</p>
</details>

<details><summary>Task 3.1 to 3.2</summary>
<p>

## Task 3.1

### Q: Log into the administrator account and get the flag

A: 32a5e0f21372bcc1000a6088b93b458e41f0e02a 

Walkthrough: After navigating to the login page, enter some data into the email and password fields. Before clicking submit, make sure Intercept is turned on in Burp Suite

![](/OWASP%20Juice%20Shop/images/intercept.png)

We will now change the email to `' or 1=1--` and forward it to the server

![](/OWASP%20Juice%20Shop/images/or11.png)

Why does this work?

1. The character `'` will close the brackets in the SQL query
2. `'OR'` in a SQL statement will return true if either side of it is true. As 1=1 is always true, the whole statement is true. Thus, it tells the server that the email is valid and logs us into the user id 0, which happens to be the administrator account
3. The `--` character is used in SQL to comment out data. Any restrictions on the login will no longer work as they are interpreted as a comment

We should now be logged in as administrator

![](/OWASP%20Juice%20Shop/images/admin_login.png)

## Task 3.2

### Q: Log into the Bender account

Similiar to what we did before, capture the login request again, but this time put `bender@juice-sh.op` as the email

![](/OWASP%20Juice%20Shop/images/bender.png)

Why don't we put the 1=1? As the email address is valid which will return true, we do not need to force it to be true

We should now be logged in as Bender

![](/OWASP%20Juice%20Shop/images/bender.png)

A: fb364762a3c102b2db932069c0e6b78e738d4066