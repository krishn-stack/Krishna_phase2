# Containers - DoorDasher's Demise
 > Continue your Advent of Cyber journey and learn about container security.

## Task 1 -> Introduction
  > It seemed as the sun rose this morning, it had already been decided that today would be another day of chaos in Wareville. At least that’s the feeling all the folks at “DoorDasher” got. DoorDasher is Warevilles local food delivery site, a favourite of the workers in The Best Festival Company, especially on long days when they get home from work and just can’t bring themself to make dinner. We’ve all been there, I’m sure.

> Well, one Wareville resident was feeling particularly tired this morning and so decided to order breakfast. Only to find King Malhare and his bandit bunny battalions had seized control of yet another festive favourite. DoorDasher had been completely rebranded as Hopperoo. All of the ware’s favourite dishes had been changed as well. Reports started flooding into the DoorDasher call centre. And not just from customers. The health and safety food org was on the line too, utterly panicked. Apparently, multiple Wareville residents were choking on what turned out to be fragments of Santa’s beard. Wareville authorities were left tangled in confusion today as Hopperoo faced mounting backlash over reports of “culinary impersonation.” Customers across the region claim to have been served what appears to be authentic strands of Santa’s beard in place of traditional noodles.

> A spokesperson for the Health & Safety Food Bureau confirmed that several diners required “gentle untangling” and one incident involved a customer “achieving accidental facial hair synchronisation.”
> Immediately, one of the security engineers managed to log on and make a script that would restore DoorDasher to its original state, but just before he was able to run it, Sir CarrotBaine caught wind of his attempt and locked him out of the system. All was lost, until the SOC team realised they still had access to the system via their monitoring pod, an uptime checker for the site. Your job? As a SOC team member of DoorDasher, can you escape the container and escalate your privileges so you can finish what your team started and save the site!

- ``` Tell me more ``` marks the completion of Task 1.

## Task 2 -> Container Security
  ### Containers
   > To understand what a container is, we first need to understand the problem it fixes. Put plainly, modern applications can be quite complex:

> 1. ***Installation:*** Depending on the environment the application is being installed in, it’s not uncommon to run into “configuration quirks” which make the process time-consuming and frustrating. 
> 2. ***Troubleshooting:*** When an application stops working, a lot of time can be wasted determining if it is a problem with the application itself or a problem with the environment it is running in.
> 3. ***Conflicts:*** Sometimes multiple versions of an application need to be run, or perhaps multiple applications which need (for example) different versions of Python to be installed. This can sometimes lead to conflicts, complicating the process further.

```
Containerisation solves these problems by packing applications, along with their dependencies, in one isolated environment. This package is known as a container.
```
### Docker
 > Docker is an open-source platform for developers to build, deploy, and manage containers. Containers are executable units of software which package and manage the software and components to run a service. They are pretty lightweight because they isolate the application and use the host OS kernel.

## Solution:
- Followed the the given challenge steps.
- Run ``` docker ps ``` command in the terminal to list all the currently running containers with Docker.

  <img width="500" height="558" alt="image" src="https://github.com/user-attachments/assets/c9b059d0-9d77-4ac0-bae8-ea8e50d37834" />

- Opened the given site ``` http://MACHINE_IP:5001 ``` and saw site is defaced by Hopperoo.
- Run ``` docker exec -it uptime-checker sh ``` to check the uptime-checker container.
- Run ``` ls -la /var/run/docker.sock ``` to check for socket access.

  <img width="570" height="212" alt="image" src="https://github.com/user-attachments/assets/8619e73d-227c-4b40-aa73-a2f2d3b25c93" />

- Then checked for ``` deployer ``` container by running the command ``` docker exec -it deployer bash ```.
- Ran the ``` recovery_script ``` in the root directory by running command ``` sudo /recovery_script.sh ``` and got the flag.

  ***BONUS QUESTION***
- Opened this site ``` http://MACHINE_IP:5002 ```, got a news report and got the answer with the red marked text

## Flags and Answers:
- What exact command lists running Docker containers?
  ```
  docker ps
  ```
- What file is used to define the instructions for building a Docker image?
  ```
  Dockerfile
  ```
- What's the flag?
  ```
  THM{DOCKER_ESCAPE_SUCCESS}
  ```
-  There is a secret code contained within the news site running on port 5002; this code also happens to be the password for the deployer user! They should definitely change their password. Can you find it?
     ```
      DeployMaster2025!
     ```




