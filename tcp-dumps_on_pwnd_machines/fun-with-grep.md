# FUN with GREP

#### Syntax

```
grep [options] [regexp] [filename]

   -i, --ignore-case     : 'it DoesNt MatTTer WhaT thE CAse Is'
   -v, --invert-match    : 'everything , BUT that text'
   -A 
<
NUM
>
              : Print NUM lines of trailing context after matching lines.
   -B 
<
NUM
>
              : Print NUM lines of trailing context before matching lines.
   -C 
<
NUM
>
              : Print additional (leading and trailing) context lines before and after the match.
   -a, --text            : Process a binary file as if it were text; this is equivalent to the --binary-files=text option.
   -w                    : Whole-word search
   -L --files-without-match : which outputs the names of files that do NOT contain matches for your search pattern.
   -l --files-with-matches  : which prints out (only) the names of files that do contain matches for your search pattern.

   -H 
<
pattern
>
 filename    : Print the filename for each match.
       example: grep -H 'a' testfile
                testfile:carry out few cyber-crime investigations

       Now, let’s run the search a bit differently:
               cat testfile | grep -H 'a'
               (standard input):carry out few cyber-crime investigations
```

#### Line and word anchors

* The ^ anchor specifies that the pattern following it should be at the start of the line:

> ```
> grep '^th' testfile
> this
>
> ```

* The $ anchor specifies that the pattern before it should be at the end of the line.

> ```
> grep 'i$' testfile
> Hi
>
> ```

* The operator &lt; anchors the pattern to the start of a word.

> ```
> grep '\
> <
> fe' testfile
> carry out few cyber-crime investigations
>
> ```

* &gt;anchors the pattern to the end of a word.

> ```
> grep 'le\
> >
> ' testfile
> is test file
>
> ```

* The b \(word boundary\) anchor can be used in place of &lt; and &gt; to signify the beginning or end of a word:

> ```
> grep -e '\binve' testfile
> carry out few cyber-crime investigations
>
> ```

# References:

https://bitvijays.github.io/LFF-ESS-P0B-LinuxEssentials.html



