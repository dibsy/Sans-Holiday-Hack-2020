# Sans-Holiday-Hack-2020
Sans Holiday Hack 2020

### 1) Uncover Santa's Gift List
```
There is a photo of Santa's Desk on that billboard with his personal gift list.
What gift is Santa planning on getting Josh Wright for the holidays?
Talk to Jingle Ringford at the bottom of the mountain for advice.
```
```
We can untwirl the image, and find the word Proxmark
```
### 2) Investigate S3 Bucket
```
When you unwrap the over-wrapped file, what text string is inside the package? 
Talk to Shinny Upatree in front of the castle for hints on this challenge.
```
### 3) Point-of-Sale Password Recovery
```
Help Sugarplum Mary in the Courtyard find the supervisor password for the point-of-sale terminal.
What's the password?
```
### 4) Operate the Santavator
```
Talk to Pepper Minstix in the entryway to get some hints about the Santavator.
```
<img src="images/elevator.PNG">

### 5) Open HID Lock
```
Open the HID lock in the Workshop.
Talk to Bushy Evergreen near the talk tracks for hints on this challenge. 
You may also visit Fitzy Shortstack in the kitchen for tips.
```
### 6) Splunk Challenge
```
Access the Splunk terminal in the Great Room. 
What is the name of the adversary group that Santa feared would attack KringleCon?
```
### 7) Solve the Sleigh's CAN-D-BUS Problem
```
Jack Frost is somehow inserting malicious messages onto the sleigh's CAN-D bus. 
We need you to exclude the malicious messages and no others to fix the sleigh. 
Visit the NetWars room on the roof and talk to Wunorse Openslae for hints.
```
```
Say, do you have any thoughts on what might fix Santa's sleigh?
Turns out: Santa's sleigh uses a variation of CAN bus that we call CAN-D bus.
And there's something naughty going on in that CAN-D bus.
The brakes seem to shudder when I put some pressure on them, and the doors are acting oddly.
I'm pretty sure we need to filter out naughty CAN-D-ID codes.
There might even be some valid IDs with invalid data bytes
```
```
First figuring out which CAN-ID associates to which vehicle actions 
02A#0000FF	; Stop
02A#00FF00	; Start
19B#000000000000	;Lock
19B#00000F000000	;Unlock
080#000000		;Brake
188#
019#			;Steering
244#			;Acceleration

So I tried the following process for each of the identified CAN ID
foreach CAN-ID in list{
  block other CAN-ID in the list,
  observe the can data,
  make the movement and validate the logs for each action
  for any unintended can message, note it down
  }
Based on the observation I noticed ,
- unusual data 0000F2097 coming for 19B ID - Lock
- unusual negative data coming for 080 ID - Brake
- unusual negative data coming for 019 ID - Steering

Feeding these information to block these ID with such conditions unlocks Santa's sleigh.
```
<img src="images/sleigh.PNG">

### 8) Broken Tag Generator
```
Help Noel Boetie fix the Tag Generator in the Wrapping Room. 
What value is in the environment variable GREETZ? 
Talk to Holly Evergreen in the kitchen for help with this.
```
### 9) ARP Shenanigans
```
Go to the NetWars room on the roof and help Alabaster Snowball get access back to a host using ARP. 
Retrieve the document at /NORTH_POLE_Land_Use_Board_Meeting_Minutes.txt. 
Who recused herself from the vote described on the document?
```
### 10) Defeat Fingerprint Sensor
```
Bypass the Santavator fingerprint sensor. 
Enter Santa's office without Santa's fingerprint.
```
```
When Santa logs in the url looks like this
https://elevator.kringlecastle.com/?challenge=santamode-elevator&id=908e3ccd-114c-XXXX-XXXX-6e222a550aee&username=heckthathack&area=santamode-santavator1&location=1,2&tokens=marble,nut2,nut,candycane,ball,yellowlight,elevator-key,greenlight,redlight,workshop-button,besanta

When the user logs in the url looks like this
https://elevator.kringlecastle.com/?challenge=santamode-elevator&id=908e3ccd-114c-XXXX-XXXX-6e222a550aee&username=heckthathack&area=santamode-santavator1&location=1,2&tokens=marble,nut2,nut,candycane,ball,yellowlight,elevator-key,greenlight,redlight,workshop-button,besanta

The only key difference is one extra parameter that is passed for santa , i.e besanta, so we can modify the html in the iframe something like this
<iframe title="challenge" src="https://elevator.kringlecastle.com?challenge=elevatorr&amp;id=5dd79c13-81de-48e0-b121-5714ca8ace80&amp;username=heckthathack&amp;area=santavator5&amp;location=1,2&amp;tokens=marble,nut,candycane,elevator-key,redlight,nut2,ball,yellowlight,greenlight,workshop-button,besanta"></iframe>
```
<img src="images/gotin.PNG">

### 11a) Naughty/Nice List with Blockchain Investigation Part 1
```
Even though the chunk of the blockchain that you have ends with block 129996, can you predict the nonce for block 130000? 
Talk to Tangle Coalbox in the Speaker UNpreparedness Room for tips on prediction and Tinsel Upatree for more tips and tools. 
(Enter just the 16-character hex value of the nonce)
```
### 11b) Naughty/Nice List with Blockchain Investigation Part 2
```
The SHA256 of Jack's altered block is: 58a3b9335a6ceb0234c12d35a0564c4e f0e90152d0eb2ce2082383b38028a90f. 
If you're clever, you can recreate the original version of that block by changing the values of only 4 bytes. 
Once you've recreated the original block, what is the SHA256 of that block?
```
