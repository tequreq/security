If see files with a timestamp but nothing is in cron maybe there is a rogue script running on a consistent basis try the following to find



```
#!/bin/bash

#Loop by line
IFS=$'\n'

old_process=$(ps -eo command)

#infinite loop
while true; do
 new_process=$(ps -eo command)
 diff <(echo "$old_process") <(echo "new_process")
 sleep 1
 old_process=$new_process
done
 
```



