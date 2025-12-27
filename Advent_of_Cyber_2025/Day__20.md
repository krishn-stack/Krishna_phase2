# Race Conditions - Toy to The World
 > Learn how to exploit a race condition attack to oversell the limited-edition SleighToy.

## Task 1 -> Introduction
 > The Best Festival Company (TBFC) has launched its limited-edition SleighToy, with only ten pieces available at midnight. Within seconds, thousands rushed to buy one, but something strange happened. More than ten lucky customers received confirmation emails stating that their orders were successful. Confusion spread fast. How could everyone have bought the "last" toy? McSkidy was called in to investigate.  

> She quickly noticed that multiple buyers purchased at the exact moment, slipping through the system’s timing flaw. Sir Carrotbane’s mischievous Bandit Bunnies had found a way to exploit this chaos, flooding the checkout with rapid clicks. By morning, TBFC faced angry shoppers, missing stock, and a mystery that revealed just how dangerous a few milliseconds could be during the holiday rush.

- ``` I can successfully connect to the machine. ``` marks the completion of Task 1.

## Task 2 -> Race Condition
> A race condition happens when two or more actions occur at the same time, and the system’s outcome depends on thebunny character showing car racing. order in which they finish. In web applications, this often happens when multiple users or automated requests simultaneously access or modify shared resources, such as inventory or account balances. If proper synchronisation isn’t in place, this can lead to unexpected results, such as duplicate transactions, oversold items, or unauthorised data change.

### Types of Race Conditions
- ***Time-of-Check to Time-of-Use (TOCTOU):*** A TOCTOU race condition happens when a program checks something first and uses it later, but the data changes in between. This means what was true at the time of the check might no longer be true when the action happens. It’s like checking if a toy is in stock, and by the time you click "Buy" someone else has already bought it. For example, two users buy the same "last item" at the same time because the stock was checked before it was updated.
- ***Shared resource:*** This occurs when multiple users or systems try to change the same data simultaneously without proper control. Since both updates happen together, the final result depends on which one finishes last, creating confusion. Think of two cashiers updating the same inventory spreadsheet at once, and one overwrites the other’s work.
- ***Atomicity violation:*** An atomic operation should happen all at once, either fully done or not at all. When parts of a process run separately, another request can sneak in between and cause inconsistent results. It’s like paying for an item, but before the system confirms it, someone else changes the price. For example, a payment is recorded, but the order confirmation fails because another request interrupts the process.


## Solution:
- Accessed the web app using ``` http://MACHINE_IP ```
- Changed ``` FoxyProxy ``` to Burp.
- Opened BurpSuite and started a new task.
- Switched off Intercept.
- Logined into the web app using given credentials, username -> ``` attacker ``` and password -> ``` attacker123 ```

   <img width="1142" height="275" alt="image" src="https://github.com/user-attachments/assets/1ecde2d1-ad96-409a-9bb6-97fdc8bde6fe" />

- Got the above dashboard.
- Added ``` SleighToy Limited Edition ``` to cart and proceed to checkout.
- Got order id.
- Opened BurpSuite and in ``` HTTP History ```, found ``` /process_checkout ``` and sent it to repeater.
- In Repater tab, created current tab group and then duplicated the order by the number of stock shown.
- Send the Request in parallel.
- Refreshed the web app and stock went to negative and got the flag.
- Did same for ``` Bunny Plush (Blue) ``` and got the flag for that too.

  ## Flags:
  ```
  THM{WINNER_OF_R@CE007}
  THM{WINNER_OF_Bunny_R@ce}
  ```
  
