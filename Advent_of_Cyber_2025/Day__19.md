# ICS/Modbus - Claus for Concern
 > Learn to identify and exploit weaknesses in ICS systems.

## Task 1 -> Introduction
The snow falls heavily over Wareville as chaos erupts at TBFC headquarters. What should be the busiest shipping day of the season has turned into a disaster.

``` "Another chocolate egg?!" ``` shouts a frustrated warehouse worker, holding up yet another Easter-themed package. ``` "We're supposed to be shipping Christmas presents!" ```

The delivery drones buzz overhead, their mechanical hums sounding almost... mocking. Each one returns from its route empty, having successfully delivered its cargo. But the cargo is all wrong.

You're called into the command centre, where screens flicker with delivery statistics. Everything looks normal on the surface—1,000 presents in stock, 98% success rate, and all systems are operational. But the phones won't stop ringing with confused citizens asking why they're receiving chocolate eggs instead of the toys and gifts they ordered.

The logistics manager pulls up a delivery manifest. ``` "Look at this" ```, she says, pointing at the screen.``` "The system indicates that we delivered a teddy bear to the Miller family, but they received a chocolate bunny instead. It's the same weight, exact dimensions, but completely different items." ```

### A Mysterious Discovery
 ```
 TBFC DRONE CONTROL - REGISTER MAP
(For maintenance use only)

HOLDING REGISTERS:
HR0: Package Type Selection
     0 = Christmas Gifts
     1 = Chocolate Eggs
     2 = Easter Baskets

HR1: Delivery Zone (1-9 normal, 10 = ocean dump!)

HR4: System Signature/Version
     Default: 100
     Current: ??? (check this!)

COILS (Boolean Flags):
C10: Inventory Verification
     True = System checks actual stock
     False = Blind operation

C11: Protection/Override
     True = Changes locked/monitored
     False = Normal operation

C12: Emergency Dump Protocol
     True = DUMP ALL INVENTORY
     False = Normal

C13: Audit Logging
     True = All changes logged
     False = No logging

C14: Christmas Restored Flag
     (Auto-set when system correct)

C15: Self-Destruct Status
     (Auto-armed on breach)

CRITICAL: Never change HR0 while C11=True!
Will trigger countdown!

- Maintenance Tech, Dec 19
```

- ``` The clock is ticking, investigator. Christmas is hanging by a thread, and only you can pull it back from the brink. ``` marks the completion of Task 1.

## Task 2 -> SCADA (Supervisory Control and Data Acquisition)
  ### SCADA
   > SCADA systems are the "command centres" of industrial operations. They act as the bridge between human operators and the machines doing the work. Think of SCADA as the nervous system of a factory—it senses what's happening, processes that information, and sends commands to make things happen.

> TBFC uses a SCADA system to oversee its entire drone delivery operation. Without it, operators would have no way to monitor hundreds of drones, manage inventory, or ensure packages reach the right destinations. It's the invisible orchestrator of Christmas logistics.

### Components of a SCADA System
A SCADA system typically consists of four key components:

- ***Sensors & actuators:*** These are the eyes and hands of the system. Sensors measure real-world conditions, such as temperature, pressure, position, and weight. Actuators perform physical actions—motors turn, valves open, robotic arms move. In TBFC's warehouse, sensors detect when a package is placed on the conveyor belt, and actuators control the robotic arms that load drones.
- ***PLCs (Programmable Logic Controllers):*** These are the brains that execute automation logic. They read sensor data, make decisions based on programmed rules, and send commands to actuators. A PLC might decide: If the package weight matches a chocolate egg AND the destination is Zone 5, load it onto Drone 7. We'll explore PLCs in detail in the next task.
- ***Monitoring systems:*** Visual interfaces like CCTV cameras, dashboards, and alarm panels where operators observe physical processes. TBFC's warehouse has security cameras on port 80 that show real-time footage of the packaging floor. These monitoring systems provide immediate visual feedback—you can literally watch what the automation is doing.
- ***Historians:*** Databases that store operational data for later analysis. Every package loaded, every drone launched, every system change gets recorded. This historical data helps identify patterns, troubleshoot problems, and—in incident response scenarios like ours—reconstruct what an attacker did.

### Why SCADA Systems Are Targeted?
- ``` legacy software ``` with known vulnerabilities.
- ``` Default credentials ``` are commonly left unchanged.
- They're designed for ``` reliability, not security ```.
- They control ``` physical processes ```.
- They're often ``` connected to corporate networks ```.
- Protocols like Modbus ``` lack authentication ```.

  ## Answers:
  ***What port is commonly used by Modbus TCP?***
  ```
  502
  ```

## Task 3 -> PLC & Modbus Protocol
 ### What is a PLC?
  > A PLC (Programmable Logic Controller) is an industrial computer designed to control machinery and processes in real-world environments. Unlike your laptop or smartphone, PLCs are purpose-built machines engineered for extreme reliability and harsh conditions.

PLCs are designed to:
- Survive harsh environments
- Run continuously without failure
- Execute control logic in real-time
- Interface directly with physical hardware

### What is Modbus?
 > Modbus is the communication protocol that industrial devices use to talk to each other. Created in 1979 by Modicon (now Schneider Electric), it's one of the oldest and most widely deployed industrial protocols in the world. Its longevity isn't due to sophisticated features—quite the opposite. Modbus succeeded because it's simple, reliable, and works with almost any device.
### Modbus Data Types
 
  <img width="1547" height="401" alt="image" src="https://github.com/user-attachments/assets/93c76cec-4b7c-4c2d-9947-72abefa8b685" />

Coils and Holding Registers are writable—you can change their values to control the system. Discrete Inputs and Input Registers are read-only—they reflect sensor measurements that you observe but cannot directly modify.

***Holding Registers***
- ***HR0:*** Package type selection (0=Gifts, 1=Eggs, 2=Baskets)
- ***HR1:*** Delivery zone (1-9 for normal zones, 10 for emergency disposal)
- ***HR4:*** System signature (a version identifier or, in this case, an attacker's calling card)

***Coils***
- ***C10:*** Inventory verification enabled/disabled
- ***C11:*** Protection mechanism enabled/disabled
- ***C12:*** Emergency dump protocol active/inactive
- ***C13:*** Audit logging enabled/disabled
- ***C14:*** Christmas restoration status flag
- ***C15:*** Self-destruct mechanism armed/disarmed

## Task 4 -> Practical
 > Now that you understand the basic concepts related to ICS and Modbus, we will analyse the compromised TBFC Drone Control System and learn how to safely restore it.

### Solution:
- Using ``` nmap ```, scanned ``` 22, 80, 502 ``` ports by running command ``` nmap -sV -p 22,80,502 MACHINE_IP ```
- Navigated to ``` http://MACHINE_IP ``` site, it was a CCTV camera footage where presents got replaced by easter eggs.
- Installed pymodbus by running ``` pip3 install pymodbus==3.6.8 ```
- Connected to PLC using the given code then started reading the all the ***Holding Registers*** and ***Coils***.
- For now ```C15``` was unarmed, noticed the critical given ``` not to chage HR0 when C11 = True ```. So, didn't changed HR0 or else it would self-destruct.
- Opened ```nano``` text editor and wrote ``` reconnaissance.py ``` as given and ran the script.
- Again opened nano and wrote ``` restore_christmas.py ``` and ran the script and got the flag.

  ## Flag:
  ```
  THM{eGgMas0V3r}
  ```




















