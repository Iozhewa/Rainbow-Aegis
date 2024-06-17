## Syster from another Myster? 
*Locate FTP user logins with SystemSyster for four flags*

What else is in Chad's Package?
```
C:\Users\xxx\Documents\ChadPackage> cd FilesLog
C:\Users\xxx\Documents\ChadPackage\FilesLog> dir
    fileRoster_preboot
    fileRoster_postboot
```
> It's almost like he wanted the glitch to happen...

Perhaps the cost of toying with experimental operating systems :[
This task will be less guided for you, as the previous flags help you narrow down to what files were changed.
```
C:\Users\xxx\Documents\ChadPackage> cd fileRoster_preboot
    . . . <-- I recommend to keep things 'uniq' ;>
              Screenshot any big list of files for cross-checking

C:\Users\xxx\Documents\ChadPackage\fileRoster_preboot> cd ..
C:\Users\xxx\Documents\ChadPackage\fileRoster_preboot> cd fileRoster_postboot
    . . . <-- Try 'uniq' again
              Are they supposed to be near-identical to preboot data? What happened?
```

### First: SystemSyster, the (red) Flag Sniffer
```
C:\Users\xxx\Documents\ChadPackage\fileRoster_postboot> cd ..
C:\Users\xxx\Documents\ChadPackage> python SystemSyster.py
  .  .  . 
```
Since the postboot roster is in some kind of hash function, Chad must've kept a program somwhere to evaluate message digests.
Did you remember hashes are also message digests? This will be in the exam...
```python
"SystemSyster Checksum Modification Detector" (omnicron 4.3.6)
# 'Line Number:' __
'Encryption Functon:' hash(hash(text) + salt)  'Decryption Function:' unhash(unhash(text) - salt)
## Commands: ciphertext -salt __ [name], plaintext -salt __ [name], blametext [name]

>>
. . .
>> blametext Chad.txt
### Based on your assessment, file (NAME:TYPE:SALT) has compromised details. Verify? [y/n]
>> y
### Checksum Modification detected! (1/2 for NETWORK)
or
>> y
### No compromise detected. (3 tries left.)
```
![input-outputs of SystemSyster.py](image.jpg)

When you've Sysed all files compromised (I believe there were four?) Syster will release its captured flag code. Something like:
`task complete! submit this... RainbowAegis_CTF(Reboot:Messed:Files:Confirmed:[gibberish so you don't copypaste this format])`
***
#### This CTF has taught you...
- [x] Explored integration of cryptography into LANs
- [x] Applied hashing and salts to protect sensitive data
- [x] Using checksums to observe file modifications
#### Up next...
Pop quiz, and Random flags :anguished:

[<kbd>Previous Stage</kbd>](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/bFlags_onCALM.md)  [<kbd>Next Stage</kbd>](https://github.com/Iozhewa/Rainbow-Aegis/blob/main/CTF-Tutorial/dFlags_withQuizard.md)
