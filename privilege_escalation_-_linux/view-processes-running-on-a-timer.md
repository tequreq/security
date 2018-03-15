If see files with a timestamp but nothing is in cron maybe there is a rogue script running on a consistent basis try the following to find

IPPSEC--Nineveh

```
#!/bin/bash

#Loop by line
IFS=$'\n'

old_ps=$(ps -eo command)

#infinite loop
while true; do
  new_ps=$(ps -eo command)
  diff <(echo "$old_ps") <(echo "$new_ps")
  sleep 1
  old_ps=$new_ps
done
```

Note if trying to echo quotes to a script use single quotes

for example

echo ' "Hello World" ' &gt; test.txt

