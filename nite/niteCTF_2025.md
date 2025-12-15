# Database Reincursion:
   > First day as an intern at Citadel Corp and i'm already making strides!
Got rid of that bulky unnecessary security system and implemented my own simple solution.

## Flag: 
```
Didn't got
```

## Approach:
- As the challenge says that it got rid of bulky unnecessary security system and implemented own simple solution.
- I thought that those different types of filters have been removed so I tried using the SQL injection, I used earlier ``` ' OR '1'='1' -- ```, got to know that this injection is blocked,.
- After this, I tried with ``` AND ```, used ``` admin ``` and some more injection queries, nothing seems to work.
- I got to know that all of these queries have been blocked by the server.
- Used some normal queries like where 1=1 and some commenting queries but none of them worked.
- So, I used chatgpt to give me more of the queries to be used when these tautology queries are blocked, it gave me some with ``` null ```, I used them but none of them worked too.
- After trying for almost whole day, I gave up om that and moved to forensics.

## Concepts Learned:
- Got to know about some of the ``` null ``` SQL injection queries for bypass authentication.
