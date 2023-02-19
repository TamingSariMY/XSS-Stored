# XSS-Stored
![image](https://user-images.githubusercontent.com/106005322/219943091-239a975d-4152-4d1b-821b-7be33defb98e.png)

#

## Stored XSS Attacks
#### Stored attacks are those where the injected script is permanently stored on the target servers, such as in a database, in a message forum, visitor log, comment field, etc. The victim then retrieves the malicious script from the server when it requests the stored information. Stored XSS is also sometimes referred to as Persistent or Type-II XSS.

#
#
## This is a Stored-XSS simulation that i did on DVWA(Damn Vulnerable Web Application) from low to high stages
#
#

## Low
![Screenshot (46)](https://user-images.githubusercontent.com/106005322/219943555-1bd0edb1-d4ee-4c81-a4fe-16206240612e.png)
#### at this low level, if we look at the source code, there is a filter on the message input, which is ```stripslashes```, but this code does not interfere with the payload that is to be injected because stripslashes only work on backslashes

#

![Screenshot (47)](https://user-images.githubusercontent.com/106005322/219943700-5576a16b-9ea6-46b6-b4c6-bd23324d4e73.png)
#### so now I'm going to enter the payload

#

![Screenshot (48)](https://user-images.githubusercontent.com/106005322/219944091-8f382922-cfa2-413a-a8fb-72a15eeef34f.png)
#### as you can see the payload can trigger an xss vulnerability on this page

#
#

## Medium

![Screenshot (49)](https://user-images.githubusercontent.com/106005322/219945439-38e0e42c-c0e3-4266-bc49-66a2d2f8091f.png)
#### if we look at the message section there are ```strip_tags``` and ```htmlspecialchars``` where this filter will delete payloads that have ```<>``` symbols and also payloads that are html/xml and php

#

![Screenshot (52)](https://user-images.githubusercontent.com/106005322/219945455-1bef0b6d-0e22-4239-b907-093fdf56034f.png)
#### so now we only have an opportunity in the name section where we only need to change any letter to uppercase to bypass ```str_replace```, but in the name text box there is a filling limit where this will fail our payload, so here we just need to press inspect and change the maxlength to 33 or more

#

![Screenshot (53)](https://user-images.githubusercontent.com/106005322/219945463-cadb0989-bca6-4c2d-ad13-17d3ee3a673f.png)
![Screenshot (54)](https://user-images.githubusercontent.com/106005322/219945485-25d9f3ef-d913-4927-a536-efb8148050f8.png)
#### so now if I execute the payload we will be able to see that the page has an xss vulnerability

#
#

## High

![Screenshot (56)](https://user-images.githubusercontent.com/106005322/219945537-17e03e67-e82e-4982-bbce-f46a8a5f2f35.png)
#### here if you look at the name section again there is the same filter at the medium level, so we only have a chance at the name but in the name section there is preg_replace this means we cannot inject js payload on the name, but we can inject the payload in the form of html

#

![Screenshot (57)](https://user-images.githubusercontent.com/106005322/219945544-df3254d8-8da6-4443-8240-26e65b5adcbc.png)
#### so now I will inject the payload in html form

#

![Screenshot (58)](https://user-images.githubusercontent.com/106005322/219945555-5e259345-5669-4843-b72b-f80dfdc4d499.png)
#### as you can see i can bypass this page with payload in html form

