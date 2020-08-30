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

![](/OWASP%20Juice%20Shop/images/bender_login.png)

A: fb364762a3c102b2db932069c0e6b78e738d4066

</p>
</details>

<details><summary>Task 4.1 to 4.2</summary>
<p>

## Task 4.1

### Q: Bruteforce the Administrator's password

A: c2110d06dc6f81c67cd8099ff0ba601241f1ac0e

Walkthrough: Capture a login request and then go to the `Positions` tab and select the `Clear` button in Intruder. In the password field, place two $$ inside the quotes

![](/OWASP%20Juice%20Shop/images/brute_intruder.png)

For the payload, we will be using the best1050.txt from SecLists - can be installed via the `apt-get install seclists` command

Can load the list from `/usr/share/seclists/Passwords/Common-Credentials/best1050.txt`

![](/OWASP%20Juice%20Shop/images/seclists.png)

Once the file is loaded into Burp, start the attack. Then, filter for the request by status. A failed request will receive a `401 Unauthorized` where as a sucessful request will return a `200 OK`

![](/OWASP%20Juice%20Shop/images/success_brute.png)

Once complete, login and get the flag

![](/OWASP%20Juice%20Shop/images/admin_creds.png)

## Task 4.2

### Q: Reset Jim's password

A: 094fbc9b48e525150ba97d05b942bbf114987257

Walkthrough: The reset password mechanism can also be exploited. When inputted into the email field in the Forgot Password page, Jim's security question is set to "Your elder siblings middle name"

![](/OWASP%20Juice%20Shop/images/eld_sibling.png)

In task 2, we found that Jim might have something to do with Star Trek. Googling "Jim Star Trek" gives us a wiki page for James T. Kirk from Star Trek

Looking through the wiki page, we see that he has a brother called George and his middle name is Samuel

![](/OWASP%20Juice%20Shop/images/george.png)

Inputting this information allows us to successfully change his password

![](/OWASP%20Juice%20Shop/images/jim_flag.png)

</p>
</details>

<details><summary>Task 5.1 to 5.3</summary>
<p>

## Task 5.1

### Q: Access the Confidential Document

A: edf9281222395a1c5fee9b89e32175f1ccf50c5b

Walkthrough: Navigate to the `About Us` page and hover over the "Check out our terms of use". You will see that it links to `/ftp/legal.md`. Navigating to that /ftp/ directory reveals that it is exposed to the public

![](/OWASP%20Juice%20Shop/images/ftp_directory.png)

Download all the interesting looking files and save it. After downloading, navigate to the home page to receive the flag

![](/OWASP%20Juice%20Shop/images/data_success.png)

## Task 5.2

### Q: Log into MC SafeSearch's account

A: 66bdcffad9e698fd534003fbb3cc7e2b7b55d7f0

Walkthrough: Searching MC SafeSearch brings up [this YouTube video](https://www.youtube.com/watch?&v=v59CX2DiX0Y&feature=emb_title). In this video, he reveals that his password is `Mr Noodles` but he replaced some vowels with zeroes. This must mean his password is `Mr N00dles` instead

We can now login using the email address of `mc.safesearch@juice-sh.op` and password of `Mr N00dles`

![](/OWASP%20Juice%20Shop/images/mrnoodles.png)

## Task 5.3

### Q: Download the Backup File

A:

Walkthrough: Go back to the /ftp directory and try to download `package.json.bak`. It seems we are met with a 403 which says that only .md and .pdf files can be downloaded

![](/OWASP%20Juice%20Shop/images/error.png)

To get around this, use a character bypass called "Poison Null Byte". A Poison Null Byte looks like `%00`. Note that we can download it using the URL, so we can encode this into a URL encoded format

The Poison Null Byte will now look like this - `%2500`. Adding this and then a .md will bypass the 403 error

![](/OWASP%20Juice%20Shop/images/poison.png)

How does this work?

A Poison Null Byte is actually a NULL terminator. By placing a NULL character in the string at a certain byte, the string will tell the server to terminate at that point, nulling the rest of the string

![](/OWASP%20Juice%20Shop/images/backup_success.png)

</p>
</details>

<details><summary>Task 6.1 to 6.3</summary>
<p>

## Task 6.1

### Q: Access the administration page

A: 946a799363226a24822008503f5d1324536629a0

Walkthrough: First, open the Network Viewer on Firefox. This can be done with the keyboard shortcut `Ctrl+Shift+E` and then refresh the page. Look for the GET request calling for `main-es2015.js`

![](/OWASP%20Juice%20Shop/images/js.png)

Open this file and search for the term "admin" - we are looking for the `app-administration` finding

![](/OWASP%20Juice%20Shop/images/app_admin.png)

This hints towards a page called `Administration` but going there while not logged in does not work. Because this is an admin page, it makes sense that we need to be in the Admin account

Logging in as admin and then navigating to the `/#/administration` page gives you the flag

![](/OWASP%20Juice%20Shop/images/admin_panel.png)

## Task 6.2

### Q: View another user's shopping basket

A: 41b997a36cc33fbe4f0ba018474e19ae5ce52121

Walkthrough: Log into the admin account and check the basket under `Your Basket`. Intercept this request via Burp and you should see a GET request for `/rest/basket/1`

![](/OWASP%20Juice%20Shop/images/burp_intercept.png)

Simply change the number after /basket/ from 1 to 2 and it will now show you the basket of UserID2. You can do this for other UserIDs as well, provided they have one

![](/OWASP%20Juice%20Shop/images/basket.png)

## Task 6.3

### Q: Remove all 5-star reviews

A: 50c97bcce0b895e446d61c83a21df371ac2266ef

Walkthrough: Navigate to the administration page again and click the bin icon next to the reviews with 5 stars

![](/OWASP%20Juice%20Shop/images/5star.png)

</p>
</details>

<details><summary>Task 7.1 to 7.3</summary>
<p>

## Task 7.1

### Q: Perform a DOM-based XSS

A: 9aaf4bbea5c30d00a1f5bbcfce4db6d4b0efe0bf

Walkthrough: In the search parameter on Juice Shop, use the iframe tag with a simple alert 

* <iframe src="javascript:alert(`xss`)">

![](/OWASP%20Juice%20Shop/images/dombased.png)

This type of XSS is also called XFS (Cross-Frame Scripting)

Once inputted, a popup will appear

![](/OWASP%20Juice%20Shop/images/dombased_result.png)

Websites that allow the user to modify the `iframe` will most likely be vulnerable to XSS

Once entered, you should be presented with the flag

![](/OWASP%20Juice%20Shop/images/dombased_flag.png)

## Task 7.2

### Q: Perform a Persistent XSS

A: 149aa8ce13d7a4a8a931472308e269c94dc5f156

Walkthrough: Navigate to the "Last Login IP" page for this attack

As it logs the last login IP, we will now logout so that it logs the new IP. Make sure that Burp intercept is on, so it will catch the logout request

Then, head over to the Headers tab where we will add a new Header:

* True-Client-IP			<iframe src="javascript:alert(`xss`)">

![](/OWASP%20Juice%20Shop/images/logout.png)

Then forward the request to the server. When signing back into the admin account and navigating to the last login IP page again, we will see the alert message

![](/OWASP%20Juice%20Shop/images/popup.png)

![](/OWASP%20Juice%20Shop/images/persistent_flag.png)

## Task 7.3

### Q: Perform a Reflected XSS 

A: 23cefee1527bde039295b2616eeb29e1edc660a0

Walkthrough: First, login to the admin account and navigate to the `Order History` page

From here, you will see a truck icon - clicking it will bring you to the track result page. You will also see that there is an id paired with the order in the URL

![](/OWASP%20Juice%20Shop/images/id_param.png)

Using the iframe XSS in place of the id parameter, we should be able to submit the URL, refresh the page and get the alert

![](/OWASP%20Juice%20Shop/images/url.png)

After refreshing the page, the popup should appear

![](/OWASP%20Juice%20Shop/images/xss_popup.png)

</p>
</details>
