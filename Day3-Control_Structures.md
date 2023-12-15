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
#### Operator and
In Python **and** operator returns not a boolean value but a value of one of operands.If both operands are true, result is the last value. If one of operators is a false, result of expression will be the first false value.
```
print('string1' and 'string2')
print('string1' and 'string2' and 'string3')
print('' and 'string1')
print('' and [] and 'string1')
```

#### Operator or
Operator **or**, like operator and, returns one of operands value. When checking operands, the first true operand is returned. If all values are false, the last value is returned. An important feature of or operator - operands, which are after the true operand, are not calculated.
```
print('' or 'string1')
print('' or [] or 'string1')
print('string1' or 'string2')
print('' or [] or {})
print('' or sorted([44, 1, 67]))
print('' or 'string1' or sorted([44, 1, 67]))
```
#### Example of if/elif/else statement
An example of a check_password.py script that checks length of password and whether password contains username.
```
username = input('Enter username: ')
password = input('Enter password: ')
if len(password) < 8:
    print('Password is too short')
elif username in password:
    print('Password contains username')
else:
    print('Password for user {} is set. '.format(username))
```

#### Ternary expression
It is sometimes more convenient to use a ternary operator than an extended form:
```
s = [1, 2, 3, 4]
result = True if len(s) > 5 else False
```

Note: Python Tutor Website can visualize code execution and allows you to see what happens at every stage of code execution. https://pythontutor.com/python-compiler.html#mode=edit

-----
### for
Very often the same step should be performed for a set of the same data type. For example, convert all strings in list to uppercase. Python uses for loop for such purposes. For loop iterates elements of specified sequence and performs actions specified for each element. Examples of sequences of elements that can be iterated by for:
- string
- list
- dictionary
- range
- Any Iterable

An example of converting strings in a list to uppercase without for loop
```
words = ['list', 'dict', 'tuple']
upper_words = []
print(words[0])
words[0].upper() # converting word to uppercase
upper_words.append(words[0].upper()) # converting and adding to new list
print(upper_words)
upper_words.append(words[1].upper())
upper_words.append(words[2].upper())
print(upper_words)
```
The same steps with the for loop:
```
words = ['list', 'dict', 'tuple']
upper_words = []
for word in words:
    upper_words.append(word.upper())
    print(upper_words)
```
**For** loop can work with any sequence of elements. For example, the above code used a **list** and the loop iterated over the elements of the list. The for loop works in a similar way with **tuples**. When working with strings for loop iterates through **string** characters.
```
for letter in 'Test string':
    print(letter)
```
Sometimes it is necessary to use sequence of numbers in loop. In this case, it is best to use **range**
```
for i in range(10):
    print('interface FastEthernet0/{}'.format(i))
    #print(f'interface FastEthernet0/{i}')
```
loop runs through vlans **list**, so variable can be called vlan
```
vlans = [10, 20, 30, 40, 100]
for vlan in vlans:
    print('vlan {}'.format(vlan))
    print(f' name VLAN_{vlan}')
```
When a loop runs through dictionary, it actually goes through keys.
```
r1 = {
    'ios': '15.4',
    'ip': '10.255.0.1',
    'hostname': 'london_r1',
    'location': '21 New Globe Walk',
    'model': '4451',
    'vendor': 'Cisco'}
for k in r1:
    print(k)
```

If you want to print key-value pairs in loop, you can do this:
```
r1 = {
    'ios': '15.4',
    'ip': '10.255.0.1',
    'hostname': 'london_r1',
    'location': '21 New Globe Walk',
    'model': '4451',
    'vendor': 'Cisco'}
for key in r1:
    print(key + ' => ' + r1[key])
```
Or use **items()** method which allows you to run loop over a key-value pair. Method items() returns a special view object that displays key-value pairs.
```
r1 = {
    'ios': '15.4',
    'ip': '10.255.0.1',
    'hostname': 'london_r1',
    'location': '21 New Globe Walk',
    'model': '4451',
    'vendor': 'Cisco'}
for key, value in r1.items():
    print(key + ' => ' + value)
#print(r1.items())
```
#### Nested for
Loops for can be nested in each other.
In this example, commands is a list of commands to execute on each interface in the fast_int list. The first for loop passes through interfaces in the fast_int list and the second through commands in commands list.
```
commands = ['switchport mode access', 'spanning-tree portfast', 'spanning-tree bpduguard enable']
fast_int = ['0/1', '0/3', '0/4', '0/7', '0/9', '0/10', '0/11']
for intf in fast_int:
    print(f'interface FastEthernet {intf}')
    for command in commands:
        print(' {}'.format(command))
```
#### Combination for and if
```
access_template = [
    "switchport mode access",
    "switchport access vlan",
    "spanning-tree portfast",
    "spanning-tree bpduguard enable",
    ]
fast_int = {"access": {"0/12": 10, "0/14": 11, "0/16": 17, "0/17": 150}}
for intf, vlan in fast_int["access"].items():
    print("interface FastEthernet" + intf)
    for command in access_template:
        if command.endswith("access vlan"):
            print(" {} {}".format(command, vlan))
        else:
            print(" {}".format(command))
```

### while
A while loop is another type of loop in Python. In the while loop, as in the if statement, you need to write a condition. If the condition is true, the actions inside the while block are executed. In this case, unlike if, after executing the code in the
block, while returns to the beginning of the loop. 
```
a = 5
while a > 0:
    print(a)
    a -= 1         # This record is equal to: a = a - 1
```

### break, continue, pass
Python has several operators that allow to change default loop behavior.
#### Break operator
Operator break allows early termination of loop:
- break breaks current loop and continues executing the next expressions
- if multiple nested loops are used, break interrupts internal loop and continues to execute expressions following the block. Break can be used in loops for and while
```
for loop
for num in range(10):
    if num < 7:
        print(num)
    else:
        break

# while loop
i = 0
while i < 10:
    if i == 5:
        break
    else:
        print(i)
        i += 1
```
```
username = input('Enter username: ')
password = input('Enter password: ')
while True:
    if len(password) < 8:
        print('Password is too short\n')
    elif username in password:
        print('Password contains username\n')
    else:
        print('Password for user {} is set'.format(username))
        # exit while loop
        break
    password = input('Enter password once again: ')
```

#### Continue operator
Operator **continue** returns control to the beginning of loop. That is, continue allows to «jump» remaining expressions in loop and go to the next iteration.
```
for num in range(5):
    if num == 3:
        continue
    else:
        print(num)

#while
i = 0
while i < 6:
    i += 1
    if i == 3:
        print("Skip 3")
        continue
        print("No one will see it")
    else:
        print("Current value: ", i)
```

```
username = input('Enter username: ')
password = input('Enter password: ')
password_correct = False
while not password_correct:
    if len(password) < 8:
        print('Password is too short\n')
    elif username in password:
        print('Password contains username\n')
    else:
        print('Password for user {} is set'.format(username))
        password_correct = True
        continue
    password = input('Enter password once again: ')
```

#### Pass operator
Operator pass does nothing. Basically it is a placeholder. For example, pass can help when you need to specify a script  structure. It can be set in loops, functions, classes. And it won’t affect execution of code.
```
for num in range(5):
    if num < 3:
        pass
    else:
        print(num)
```
#### for/else, while/else
In loops for and while you may optionally use else block.
####for/else
In loop for:
- block else is executed if loop has completed iteration of list
- but it does not execute if break was applied in loop.

```
for num in range(5):
    print(num)
else:
    print("Run out of numbers")

#with break
for num2 in range(5):
    if num2 == 3:
        break
    else:
        print(num2)
else:
    print("Run out of numbers")
```
