#  TryHackMe - Web Fundamentals (Room 005)

## Task 2.1

### Q: What request verb is used to retrieve page content?

A: GET

## Task 2.2

### Q: What port do web servers normally listen on?

A: Port 80

## Task 2.3

### Q: What is responsible for making websites look good?

A: CSS (Cascading Style Sheets)

## Task 3.1

### Q: What verb would be used for a login?

A: POST

## Task 3.2

### Q: What verb would be used to see your bank balance once logged in?

A: GET

## Task 3.3

### Q: Does the body of a GET request matter? Yea/Nay

A: Nay

## Task 3.4

### Q: What is the status code for "I'm a teapot"?

A: 418

## Task 3.5

### Q: What status code will you get if you need to authenticate to access some content, and you are unauthenticated?

A: 401

## Task 5.1

### Q: What's the GET flag?

A: thm{162520bec925bd7979e9ae65a725f99f}

Walkthrough: Perform a simple GET request using cURL to the website 

![](/Web%20Fundamentals/images/get_request.png)

## Task 5.2

### Q: What is the POST flag?

A: thm{3517c902e22def9c6e09b99a9040ba09}

Walkthrough: Perform a POST request using cURL with "flag_please" in the body using the `--data` flag

![](/Web%20Fundamentals/images/post_request.png)

## Task 5.3

### Q: What is the "Get a cookie" flag?

A: thm{91b1ac2606f36b935f465558213d7ebd}

Walkthrough: Perform a GET request using cURL with the `-c -` option to get the cookies. This prints out the cookies and does NOT store them in a file - instead printing it to the screen

![](/Web%20Fundamentals/images/get_cookie.png)

## Task 5.4

### Q: What is the "Set a cookie" flag?

A: 

Walkthrough: Perform a POST request using cURL with the `--cookie 'flagpls=flagpls'` flag which sends the cookie with the name and data of "flagpls"

![](/Web%20Fundamentals/images/post_cookie.png)
