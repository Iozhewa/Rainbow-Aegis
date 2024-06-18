### Second: Get to Know our Users

![ip dhcp pool]([image.jpg](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/ipPool.png))
![access list]([image](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/privileges.png).jpg)

Bus topologies typically follow a `linear connection` for simple expansion. It's likely why Chad considered trialing the bottom network before offering to...?
Ring topologies, on the other hand, have a `hub of switches` to transfer data in one direction. This gives less collision chance, and offers higher transfer speeds. Chad would leave this for...?
> I assume you have a final quiz about all these somewhere...

You know me too well!
On that note, let's see just who is in these topologies-

![SHAzam AW server open]([image.jpg](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/openServer.png)) ![Landing window](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/servicesTab.png) ![Services window](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/emailSection.png)
***
![BJT Records server open](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/openServer(1).png) 

Open the `Email` service for now, and keep that `FTP` one also. Both have a list of users and passwords.
I suspect the Big Boot has altered `Email login details`. No biggie, Chad must've kept a copy somewhere. Can switching OS actually do this?
...you're reading into things.

![SHAzam AW email detals](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/emailAccounts.png) ![SHAZAM AW FTP details](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/ftpSection.png)
***
![BJT Records email detals](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/emailAccounts(1).png) ![BJT Records FTP details](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/ftpSection(1).png)

FTP will come later. For now, I think we're ready to consult... `The  C H A D  package`

### Third: Set things Right
It's time to check your monitoring package to see what you can do about the reboot. 
Assume in the scenario Chad has a post-it note somewhere, directing you to some case-specific actions if something goes awry. In reality, I'd like you to explore a Git.
```
# Note to novices: This does stay in your filesystem after the activity.
  However, it doesn't act independently. 
C:\Users\xxx> dir
  ...
C:\Users\xxx> cd Documents
C:\Users\xxx\Documents> mkdir ChadPackage
C:\Users\xxx\Documents\ChadPackage> cd ChadPackage
C:\Users\xxx\Documents\ChadPackage> git clone https://github.com/Iozhewa/RainbowAegis_cPack.git
```

![GitHub-side directory contents](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/hybridDirectory.png)

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
# 'Line Number:' __
'EXPLORING NETWORK:' ___    'EXPLORING GROUP:' ___    'USER NAMES:' Private/Public
## Commands: network [bus/ring], group [name], user [salt], report [user]
## hash -network __ -group __ (Fill in network, fill in group, and press ENTER)
## user [salt] <-- Salts are a random sequence of numbers, perhaps accompained by a random letter too.
                   Where have you seen that in Email/FTP?
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

![input-outputs of CALM.py]([image.jpg](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/assets/CALMprogram.png))

When you've CALMed all emails compromised (I believe there were four?) CALM will release its captured flag code. Something like:
`task complete! submit this... RainbowAegis_CTF(Reboot:Messed:Usernames:Confirmed:[gibberish so you don't copypaste this format])`
***
#### This CTF has taught you...
- [x] Explored integration of cryptography into LANs
- [x] Applied hashing and salts to protect sensitive data
#### Up next...
  Using checksums to observe file modifications

[<kbd>Previous Stage</kbd>](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/aHello_toNetwork.md)  [<kbd>Next Stage</kbd>](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/cFlags_withSyster.md)
