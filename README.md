Build procedure : ```$ gcc soulkeeper.c -o soulkeeper -lcrypto```

#What is this about ?

The passwords in Apple OS X keychain file are encrypted many times over with various different keys. 
Some of these keys are encrypted using other keys stored in the same file, in a russian-doll fashion. 
The key that can open the outermost doll and kickstart the whole decryption cascade is derived from the user’s login password using PBKDF2. 
Here we call this the master key.

```
PBKDF2 (Password-Based Key Derivation Function 2) is a key derivation function that is part of RSA Laboratories'
Public-Key Cryptography Standards (PKCS) series, specifically PKCS #5 v2.0, also published as Internet Engineering 
Task Force's RFC 2898. 

It replaces an earlier standard, PBKDF1, which could only produce derived keys up to 160 bits long.

PBKDF2 applies a pseudorandom function, such as a cryptographic hash, cipher, or HMAC to the input password 
or passphrase along with a salt value and repeats the process many times to produce a derived key, which can 
then be used as a cryptographic key in subsequent operations. The added computational work makes password cracking
much more difficult, and is known as key stretching. When the standard was written in 2000, the recommended
minimum number of iterations was 1000, but the parameter is intended to be increased over time as CPU speeds
increase. Having a salt added to the password reduces the ability to use precomputed hashes (rainbow tables) 
for attacks, and means that multiple passwords have to be tested individually, not all at once. The standard 
recommends a salt length of at least 64 bits.
```

#### Execution of Soulkeeper.
```
$ sudo ./soulkeeper
[*] Searching process 15 heap range 0x7f80d9c00000-0x7f80da000000
[*] Searching process 15 heap range 0x7f80db800000-0x7f80dbc00000
[*] Found 12 master key candidates
[*] Trying to decrypt wrapping key in <keychain path is here>
[*] Trying master key candidate: 0000000000000***0000000000000***31***7474d7f0***
[*] Trying master key candidate: 00000000000000****00000*****004002***7474d7f0***
[*] Trying master key candidate: b***4c54a3678dbbf12***069d7bdf2817***1fd33d78***
[+] Found master key: b***4c54a3678dbbf12***069d7bdf2817***1fd33d78***
[+] Found wrapping key: <key here>
<List of passwords follows here>
```


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/Pixanor/soulkeeper/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

