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
#### Comparison operators
Comparison operators can be used in conditions. ( Note that equality is checked by double **==** )
```
print(5 > 6)
print(5 > 2)
print(5 < 2)
print(5 == 2)
print(5 == 5)
print(5 >= 5)
print(5 <= 10)
print(8 != 10)
```

```
a = 9
if a == 10:
    print('a equal to 10')
elif a < 10:
    print('a less than 10')
else:
    print('a greater than 10')
```
Operator **in** allows checking for the presence of element in a sequence (for example, element in a
list or substrings in a string):
```
print('Fast' in 'FastEthernet')
print('Gigabit' in 'FastEthernet')
vlan = [10, 20, 30, 40]
print(10 in vlan)
print(50 in vlan)
```

When used with dictionaries, in condition performs check by dictionary keys
```
r1 = {
    'IOS': '15.4',
    'IP': '10.255.0.1',
    'hostname': 'london_r1',
    'location': '21 New Globe Walk',
    'model': '4451',
    'vendor': 'Cisco'}
print('IOS' in r1)
print('4451' in r1)
```

Conditions can also use logical operators and, or, not:
```
r1 = {
    'IOS': '15.4',
    'IP': '10.255.0.1',
    'hostname': 'london_r1',
    'location': '21 New Globe Walk',
    'model': '4451',
    'vendor': 'Cisco'}
vlan = [10, 20, 30, 40]
print('IOS' in r1 and 10 in vlan)
print('4451' in r1 and 10 in vlan)
print('4451' in r1 or 10 in vlan)
print(not '4451' in r1)
print('4451' not in r1)
```
