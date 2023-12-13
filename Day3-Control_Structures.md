All code has been executed sequentially - all lines of script have been executed in order in
which they are written in file. This section covers program flow control:
- branching with if/elif/else
- repeating actions using for and while loops
- exception handling with try/except

### if/elif/else
The if/elif/else statement allows make branches during program execution. The program goes
into branch when a certain condition is met.
In this statement only if is mandatory, elif and else are optional:
- if condition is always checked first.
- After if statement there must be some condition: if this condition is met (returns True), then actions in block if are executed.
- elif can be used to make multiple branches, that is, to check incoming data for different conditions.
- elif block is the same as if but it checked next. Roughly speaking, it is “otherwise if …”
- There can be many elif blocks.
- else block is executed if none of conditions if or elif were true

```
a = 9
if a == 10:
    print('a equal to 10')
elif a < 10:
   print('a less than 10')
else:
   print('a greater than 10')
```
