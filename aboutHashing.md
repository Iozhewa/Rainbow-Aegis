# Encryption Algorithms: Hashing
Hashing is the process of assigning data to fixed values. These outputs are known as message digests, or `checksums`.

Explore some of the ways hash functions protect sensitive data with this CTF.
## Learning Intentions
- Exploring the integration of cryptography into Local Area Networks
- Applying the 'Hash & Salt' method into Email and FTP accounts
- Using checksums to observe file modifications
## Flag Criteria
- [ ] CALM 1st, 2nd SHAzam email (2 pts) [jump to](#CALM)
- [ ] CALM 1st, 2nd Bitwise email (2 pts)
- [ ] SystemSyster 1st, 2nd SHAzam FTP (2 pts) [jump to](#Syster)
- [ ] SystemSyster 1st, 2nd Bitwise FTP (2 pts)
- [ ] Quizard... Salt Q, Checksum Q, Bus Q, Ring Q (4 pts) [jump to](#some-section)
- [ ] ??? (4 pts) [jump to](#some-section)

Total flags: `16`
> Hey... this is a lot for one activity...

No need to rush! This CTF can be completed at any pace :]

Your progress through this project can be marked `complete` at any of the following achievements. If this is being `hosted` to you, perhaps you could even request the following prizes..!
| Achievement  | Host Recommended Prize | Conditions    |
| :----------- | :---------------------:| -----------:  |
| Guest        | A High Five..!         | 32% (5 pts)   |
| Ticketer     | A Kitkat               | 56% (9 pts)   |
| Analyst      | A Coffee Run           | 81% (13 pts)  |
| Superuser    | Hershey Chocolate Bar  | 100% (16 pts) |
***
<a name="CALM" />

## Everybody CALM down... 
*Resolve user logins with CALM for two flags*

[pkt]: https://www.google.com
Start by downloading the following Packet Tracer [network][pkt]:

![full view of network topology](image.jpg)

How's it looking? Here's the scenario:
```
You are AGATHA, an assistant network administrator. Assistant of CHAD, specifically.
  CHAD boasts he is able to support two demands:
  An EXPANDABLE network tested with an engineering client, and an EQUALLY DISTRIBUTED system for higher transfer speeds.

This has garnered the attention of the BITWISE JAZZ TROUPE, and the SHAzam AIRLINE WHISTLEBLOWERS.

Excited, CHAD registers the new users and leaves you to monitor one last SYSTEM UPDATE the night before launch.
  The office lights flicker. Your monitor alerts you of errors resequencing the server data. All PCs suddenly light up.

That's when you decide you should probably suspend all accounts...
```
We've situated you at a spot to interact with the `(1) 'Internet' Router` and the `(2) Server Room`. 
That is, all information relevant to your task will be here.

![diagram of YOU ARE HERE, focusing on the three admin devices](image.jpg)

### First: Check Chad's Configuration for Context Clues
Double-click on the router, and look for the `CLI tab` from the resulting pop-up. It should be near the top-left corner of that window.

![cursor hovers over router](image.jpg)
![zoom-in on the router interface tabs](image.jpg)
![command-line interface](image.jpg)

So... Chad did register his users right before the big ol' reboot.
Let's run some diagnostics to see what could've happened...
```
Press RETURN to get started!
  ...
Router> enable
Router#show ip dhcp pool
  ...
Router#show access-list
  ...
```
What are we noticing?
> I'm getting a lot of 10.13.37.xx and 192.168.1.xx...

Elementary!
What you're looking at are Class A and Class C IP addresses, respectfully. They're assigned depending on the network range of that network. That's our DHCP clue.

What about the access list clue?
> The Class C addresses are denied under 'Block Bus'... and Class C are denied under 'Block Ring'...

Excellent.
Chad's Hybrid network consists of a Bus-Ring topology.

LATER: Second should probably be a continuation md. I don't want this to look like a textbook.
### Second: Get to Know our Users

![ip dhcp brief](image.jpg)
![access list](image.jpg)

Bus topologies typically follow a `linear connection` for simple expansion. It's likely why Chad considered trialing the bottom network before offering to...?
Ring topologies, on the other hand, have a `hub of switches` to transfer data in one direction. This gives less collision chance, and offers higher transfer speeds. Chad would leave this for...?
> I assume you have a final quiz about all these somewhere...

You know me too well!
On that note, let's see just who is in these topologies-

![SHAzam AW server open](image.jpg) ![Landing window](image.jpg) ![Services window](image.jpg)
![BJT Records server open](image.jpg) ![Landing window](image.jpg) ![Services window](image.jpg)

Open the `Email` service for now, and keep that `FTP` one for later. Both have a list of users and passwords.
I suspect the Big Boot has altered `Email login details`. No biggie, Chad must've kept a copy somewhere. Can switching OS actually do this?
...you're reading into things.

![SHAzam AW email detals](image.jpg) ![SHAZAM AW FTP details](image.jpg)
![BJT Records email detals](image.jpg) ![BJT Records FTP details](image.jpg)

Alright. I think we're ready to consult... `The  C H A D  package`

### Third: Set things Right
It's time to check your monitoring package to see what you can do about the reboot. 
Assume in the scenario Chad has a post-it note somewhere, directing you to some case-specific actions if something goes awry. In reality, I'd like you to explore a Git.
```
# Note to novices: This does stay in your filesystem after the activity. However, it doesn't act independently. 
C:\Users\xxx> dir
  ...
C:\Users\xxx> cd Documents
C:\Users\xxx\Documents> mkdir ChadPackage
C:\Users\xxx\Documents\ChadPackage> cd ChadPackage
C:\Users\xxx\Documents\ChadPackage> git clone https://github.com/Iozhewa/RainbowAegis_cPack.git
```

![GitHub-side directory contents](image.jpg)

What we're looking for at the moment is the `CALM.py` program.
```
C:\Users\xxx> dir
  ...
C:\Users\xxx\Documents\ChadPackage> python CALM.py
  ...
```
> This one is also talking to me...

Yup!
Chad stores his passwords in a rainbow table, to account for a possible data breach. Rainbow tables store login details in "Username/Hash" format, so that they can access them securely.
If the server fails to protect them, the unique function making these hashes will be known only to us. You won't be able to enter an account, though, if he hid his salt well!

```python
"Chad's Algorithm for Liable Machinery" (omnicron 4.3.6)
# 'Command Number:' __
'EXPLORING NETWORK:' ___    'EXPLORING GROUP:' ___    'EXPLORING USER:' ___
## Commands: network [bus/ring], group [name], user [name], report [user]
## hash [complete all other commands, and press ENTER]
>>
. . .
>> report Chad
### Based on your assessment, hash (USER:GROUP:NETWORK) has compromised details. Verify? [y/n]
>> y
### Liable Machinery detected! (1/2 for NETWORK)
or
>> y
### No compromise detected. (3 tries left.)
```

![input-outputs of RainbowTables.py](image.jpg)

When you've CALMed all emails compromised (I believe there were four?) CALM will release its captured flag code. Something like:
`task complete! submit this... RainbowAegis_CTF(Reboot:Messed:Usernames:Confirmed:[gibberish so you don't copypaste this format])`
<a name="Syster" />

## Syster from another Myster? 
*Locate FTP user logins with CALM for two flags*
