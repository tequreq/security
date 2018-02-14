### Encrypted Files[¶](http://bitvijays.github.io/LFC-VulnerableMachines.html#encrypted-files)

Many times during the challenges, we do find encrypted files encrypted by Symmetric key encryption or RSA Public-Private Key encryption

#### Symmetric Key

If we have the encrypted file and the key to it. However, we don’t know the encryption scheme such as aes-128-cbc, des-cbc.

We can use the code written by superkojiman in[De-ICE Hacking Challenge Part-1](https://blog.techorganic.com/2011/07/19/de-ice-hacking-challenge-part-1/), it would tell you what encryption scheme is used and then we can run the command to retrieve the plaintext.

    ciphers=`openssl list-cipher-commands`
    for i in $ciphers; do
     openssl enc -d -${i} -in 
    <
    encrypted-file
    >
     -k 
    <
    password/ keyfile
    >
    >
     /dev
    ull 2
    >
    &
    1
     if [[ $? -eq 0 ]]; then
      echo "Cipher is $i: openssl enc -d -${i} -in 
    <
    encrypted-file
    >
     -k 
    <
    password/ keyfile
    >
     -out foo.txt"
      exit
     fi
    done


#### RSA Public-Private Key encryption

If we have found a weak RSA public, we can use[RsaCtfTool](https://github.com/Ganapati/RsaCtfTool)uncipher data from weak public key and try to recover private key and then use

```
openssl rsautl -decrypt -inkey privatekey.pem -in 
<
encryptedfile
>
 -out key.bin

```

The ciphertext should be in binary format for RsaCtfTool to work. If you have your ciphertext in hex, for example

```
5e14f2c53cbc04b82a35414dc670a8a474ee0021349f280bfef215e23d40601a

```

Convert it in to binary using

```
xxd -r -p ciphertext 
>
 ciphertext3

```

#### RSA given q, p and e?

Taken from[RSA Given q,p and e](https://crypto.stackexchange.com/questions/19444/rsa-given-q-p-and-e)

```
def egcd(a, b):
   x,y, u,v = 0,1, 1,0
   while a != 0:
       q, r = b//a, b%a
       m, n = x-u*q, y-v*q
       b,a, x,y, u,v = a,r, u,v, m,n
       gcd = b
   return gcd, x, y

def main():

   p = 1090660992520643446103273789680343
   q = 1162435056374824133712043309728653
   e = 65537
   ct = 299604539773691895576847697095098784338054746292313044353582078965

   # compute n
   n = p * q

   # Compute phi(n)
   phi = (p - 1) * (q - 1)

   # Compute modular inverse of e
   gcd, a, b = egcd(e, phi)
   d = a

   print( "n:  " + str(d) );

   # Decrypt ciphertext
   pt = pow(ct, d, n)
   print( "pt: " + str(pt) )

if __name__ == "__main__":
   main()

```

#### SECCURE Elliptic Curve Crypto Utility for Reliable Encryption

If you see, something like this

```
'\x00\x146\x17\xe9\xc1\x1a\x7fkX\xec\xa0n,h\xb4\xd0\x98\xeaO[\xf8\xfa\x85\xaa\xb37!\xf0j\x0e\xd4\xd0\x8b\xfe}\x8a\xd2+\xf2\xceu\x07\x90K2E\x12\x1d\xf1\xd8\x8f\xc6\x91\t
<
w\x99\x1b9\x98'

```

it’s probably[SECCURE Elliptic Curve Crypto Utility for Reliable Encryption](http://point-at-infinity.org/seccure/)Utilize python module[seccure](https://pypi.python.org/pypi/seccure)to get the plaintext.



References:

http://bitvijays.github.io/LFC-VulnerableMachines.html\#rsa-public-private-key-encryption

