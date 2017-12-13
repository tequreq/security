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
```

## Crack password of a zip without password

```
fcrackzip -u -D -p /usr/share/wordlists/rockyou.txt example.fileexample
```



