## **Dont forget to check the file type **

```
file example.fileexample
```

## Metadata

```
exiftool example.fileexample
```

## Grab contents of files with weird sizes

```
foremost -v examplefile
or
binwalk -e examplefile
or
steghide extract -sf examplefile
```

## Crack password of a zip without password

```
fcrackzip -u -D -p /usr/share/wordlists/rockyou.txt example.fileexample
```

## Crack password of a rar without password

```
[root:~/Downloads]# rar2john crocs.rar
file name: artwork.jpg
crocs.rar:$RAR3$*1*35c0eaaed4c9efb9*463323be*140272*187245*0*crocs.rar*76*35:1::artwork.jpg
```

## Crack password of a KeePass Password Database without password

```
keepass2john user.kdbx
user:$keepass$*2*6000*222*f362b5565b916422607711b54e8d0bd20838f5111d33a5eed137f9d66a375efb*3f51c5ac43ad11e0096d59bb82a59dd09cfd8d2791cadbdb85ed3020d14c8fea*3f759d7011f43b30679a5ac650991caa*b45da6b5b0115c5a7fb688f8179a19a749338510dfe90aa5c2cb7ed37f992192*535a85ef5c9da14611ab1c1edc4f00a045840152975a4d277b3b5c4edc1cd7da

john --wordlist wordlist --format=keepass hashfile
```

## Crack password of a Truecrypt File without password

```
truecrack --truecrypt <Truecrypt File> -k SHA512 -w <Wordlist_File>
```

and Veracrypt or cryptsetup to open the file.

```
cryptsetup open --type tcrypt <Truecrypt> <MountName>
```



