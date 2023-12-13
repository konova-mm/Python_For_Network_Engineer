## Python Data Types
Python has several data types:
- Numbers
- Strings
- Lists
- Dictionaries
- Tuples
- Sets
- Boolean

These data types, in turn, can be classified by several criteria:
- mutable (lists, dictionaries and sets)
- immutable (integers, strings and tuples)
- ordered (lists, tuples, strings and dictionaries)
- unordered (sets)
-----
### Numbers
To perform various mathematical operations.
#### Integer

`print(1+2)`

`print(10-7)`

`print(12*5)`

`print(2**3)`

`print(10%7)`

-----
#### Float

`print(10/3)`

-----
#### Round() Function

 Round a number to a given precision in decimal digits.
 
`print(round(10/3.0, 2)`

`print(round(10/3.0, 4))`

-----
#### Comparison operators
`print(10 > 3.0)`

`print(10 >= 10)`

`print(10 < 3)`

`print(10 <= 10)`

`print(10 == 3)`

`print(10 != 10)`

-----
The int() function allows converting to int type.

```
a="11"
print(a)
print(int(a))
```

Convert To Integer
```
b=5.555
print(int(b))
```

bin() function produces a binary representation of a number (note that the result is a string).
```
b = bin(8)
print(b)
print(bin(255)
```

function hex() produces a hexadecimal value
```
print(hex(10))
```

-----
For more complex mathematical functions, Python has a math module:
```
import math
a = math.sqrt(9)
b = math.sqrt(10)
c = math.factorial(3)
d = math.pi
print(a)
print(b)
print(c)
print(d)
```

-----
### Strings
- sequence of characters enclosed in quotes
- immutable ordered data type

```
name = "konova"
print(name)

i = """
interface Tunnel0
 ip address 10.10.10.1 255.255.255.0
 ip mtu 1416
 ip ospf hello-interval 5
 tunnel source FastEthernet1/0
 tunnel protection ipsec profile DMVPN
 """
print(i)
```

Merge and repeats into one string
```
intf = 'interface'
tun = 'Tunnel0'
x = intf + tun
print(x)

y = intf + ' ' + tun
print(y)

z = intf * 5
print(z)

z = '#' * 40
print(z)
```

Strings are an ordered data type allows to refer to characters in a string by a number
starting from zero.
```
str1 = 'interface FastEthernet1/0'
print(str1[0])
print(str1[11])
```

To refer to a character from the
end, you can specify negative values.

```
str1 = 'interface FastEthernet1/0'
print(str1[-1])
```

Make string slices by specifying a number range. Slicing starts with first number (included) and ends at second number (excluded).
```
str1 = 'interface FastEthernet1/0'
print(str1[0:9])
print(str1[10:22])
```

If no second number is specified, slice is until the end of string.
```
print(str1[10:])
```
Slice last three character of string.
```
print(str1[-3:])
```
Specify a step in slice. You can get odd numbers:
```
a = '0123456789'
print(a[1::2])
```
you can get even numbers:
```
print(a[::2])
```

Get a string in reverse order.
```
a = '0123456789'
print(a[::])
print(a[::-1])
```
len() function allows you to get number of characters in a string
```
line = 'interface Gi0/1'
print(len(line))
```
*****
Note: Function and method differ in that method is tied to a particular type of object and function is
generally more universal and can be applied to objects of different types. For example, len function
can be applied to strings, lists, dictionaries and so on, but startswith method only applies to strings.
*****

#### String methods
When automating, very often it will be necessary to work with strings, since config file, command output and commands sent - are strings. Knowledge of various methods (actions) that can be applied to strings helps to work with them more efficiently. Strings are immutable data type, so all methods that convert string returns a new string and the original string remains unchanged.

#### Methods upper, lower, swapcase, capitalize
```
string1 = 'FastEthernet'
print(string1.upper())
print(string1.lower())
print(string1.swapcase())

string2 = 'tunnel 0'
print(string2.capitalize())
```

#### Method count
Method count used to count how many times a character or substring occurs in a string.
```
string1 = 'Hello, hello, hello, hello'
print(string1.count('hello'))
print(string1.count('ello'))
print(string1.count('l'))
```

#### Method find
You can pass a substring or character to find and it will return the lowest index where first character
of the substring is (for the first match). If no match is found, find method returns -1.
```
string1 = 'interface FastEthernet0/1'
print(string1.find('Fast'))
print(string1[string1.find('Fast')::])
```

#### Methods startswith, endswith
Checking if a string starts or ends with certain symbols
```
string1 = 'FastEthernet0/1'
print(string1.startswith('Fast'))
print(string1.startswith('fast'))
print(string1.endswith('0/1'))
```

#### Method replace
Replacing a sequence of characters in a string with another sequence.
```
string1 = 'FastEthernet0/1'
print(string1.replace('Fast', 'Gigabit'))
```

#### Method strip
By default, strip method removes blank characters. This character set includes: \t\n\r\f\v
```
string1 = '\n\tinterface FastEthernet0/1\n'
print(string1)
interface FastEthernet0/1
print(string1)
print(string1.strip())
```

Method strip can be passed as an argument of any characters. Then at the beginning and at the
end of the line all characters that were specified in the line will be removed.
Method strip removes special characters at the beginning and at the end of the line. If you want
to remove characters only on the left or only on the right, you can use lstrip and rstrip.
```
ad_metric = '[110/1045]'
print(ad_metric.strip('[]'))
```

#### Method split
Method split splits the string using a symbol (or symbols) as separator and returns a list of strings:
```
string1 = 'switchport trunk allowed vlan 10,20,30,100-200'
commands = string1.split()
print(commands)
```

By default, separator is a space symbol (spaces, tabs, new line), but you can specify any separator
in parentheses:
```
string1 = 'switchport trunk allowed vlan 10,20,30,100-200'
vlans = commands[-1].split(',')
print(vlans)
c = commands.split(',')
print(c)
```

Not by one whitespace character, but by any number. 
```
sh_ip_int_br = "FastEthernet0/0               15.0.15.1 YES       manual up           up"
print(sh_ip_int_br.split())
print(sh_ip_int_br.split(' '))
```
#### f-format String
F-string is a literal line with a letter f in front of it. Inside f-string, in curly braces there are names of
variables that will be substituted:
```
ip = '10.1.1.1'
mask = 24
print(f"IP: {ip}, mask: {mask}")
```

```
first_name = 'William'
second_name = 'Shakespeare'
print(f"{first_name.upper()} {second_name.upper()}")
```

```
oct1, oct2, oct3, oct4 = [10, 1, 1, 1]
print(f'''
IP address:
{oct1:<8} {oct2:<8} {oct3:<8} {oct4:<8}
{oct1:08b} {oct2:08b} {oct3:08b} {oct4:08b}''')
```

#### strings concatenation
Literal strings concatenation
Python has very convenient functionality — literal strings concatenation
s = ('Test' 'String')
print(s)
s = 'Test' 'String'
print(s)
s = ('Test'
     'String')
print(s)     


### List
List in Python is:
- sequence of elements separated by comma and enclosed in square brackets
- mutable ordered data type

#### Creating a list using a literal
```
vlan = [10, 20, 30, 50]
print(vlans)
print(vlan[1::]
print(vlan[-1]
print(vlan[::-1]
print(lent(vlan))
print(sorted(vlan))
```

#### Create a list using list function
```
list1 = list('router')
print(list1)
```

lists are mutable, list elements can be changed.
```
list = [1, 20, 4.0, 'word']
list[0] = nova
print(list)
```

#### nested lists
```
interfaces = [['FastEthernet0/0', '15.0.15.1', 'YES', 'manual', 'up', 'up'],
              ['FastEthernet0/1', '10.0.1.1', 'YES', 'manual', 'up', 'up'],
              ['FastEthernet0/2', '10.0.2.1', 'YES', 'manual', 'up', 'down']]
interfaces[0][0]
print(interfaces[2][0])
print(interfaces[2][1])
```

len() function returns number of items in list. And sorted function sorts list items in ascending order and returns a new list with sorted items
```
items = [1, 2, 3]
print(len(items))

names = ['John', 'Michael', 'Antony']
print(sorted(names))
```

### List methods
List is a mutable data type, so it is important to note that most list methods change a list in place
without returning anything.

Method **join** collects a list of strings into one string with separator specified before join. Method **append** adds specified item to the end of list.
```
vlans = ['10', '20', '30']
','.join(vlans)
print(vlans)
vlans.append('40')
print(vlans)
```

To combine two lists you can use one of two methods: **extend** method or **addition** operation. These methods have an important difference: extend changes list to which method is applied and addition returns a new list that consists of two.
```
vlans = ['10', '20', '30', '100-200']
vlans2 = ['300', '400', '500']
vlans.extend(vlans2)
print(vlans)

result = vlans + vlans2
print(result)
```

Method **pop** removes item that corresponds to specified number. Method **remove** removes specified item.
```
vlans = ['10', '20', '30', '100-200']
vlans.pop(-1)
print(vlans)
vlans.remove('30')
print(vlans)
```

Method **index*** - returns the first index of the passed value
```
vlans = ['10', '20', '30', '100-200']
i = vlans.index('30')
print(i)
```

Method **insert** allows to insert an item into a specific place in list
```
vlans = ['10', '20', '30', '100-200']
vlans.insert(1, '15')
print(vlans)
```
Method **sort** sorts list in place
```
vlans = [1, 50, 10, 15]
vlans.sort()
print(vlans)
```

### Dictionary
Dictionaries are mutable ordered data type:
- data in dictionary are pairs key: value
- values are accessible by key, not by number as in lists
- entries in dictionary stored in order they were added
- since dictionaries are mutable, dictionary items can be changed, added, removed
- key must be an immutable object: number, string, tuple
- value can be data of any type
**Note**: In other programming languages a similar dictionary can be called an associative array,
hash, or hash table.

```
london = {'name': 'London1', 'location': 'London Str'}
print(london['name'])
print(london['location'])
```
a new key-value pair could be added, or rewritten
```
london = {'name': 'London1', 'location': 'London Str'}
london['vendor'] = 'Cisco'
print(london)

london['vendor'] = 'cisco ios'
print(london)
```

#### Nested dictionary
```
london_co = {
   'r1': {
         'hostname': 'london_r1',
         'location': '21 New Globe Walk',
         'vendor': 'Cisco',
         'model': '4451',
         'ios': '15.4',
         'ip': '10.255.0.1'
         },
   'r2': {
        'hostname': 'london_r2',
        'location': '21 New Globe Walk',
        'vendor': 'Cisco',
        'model': '4451',
        'ios': '15.4',
        'ip': '10.255.0.2'
        },
   'sw1': {
       'hostname': 'london_sw1',
       'location': '21 New Globe Walk',
       'vendor': 'Cisco',
       'model': '3850',
       'ios': '3.6.XE',
       'ip': '10.255.0.101'
       }
   }

print(london_co['r1']['ios'])
print(london_co['r1']['model'])
print(london_co['sw1']['ip'])
```

### Dictionary methods
Method **clear** allows to clear dictionary
```
london = {'name': 'London1', 'location': 'London Str'}
london.clear()
print(london)
```

Method **get** queries for key and if there is no key, returns None instead. Method get() also allows you to specify another value instead of None
```
london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}
print(london.get('ios'))
print(london.get('ios', 'Ooops'))
```

Methods keys, values, items
```
london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}
print(london.keys())
print(london.values())
print(london.items())
```

Remove key and value
```
london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}
del london['name']
print(london)
```

Method **update** allows you to add contents of one dictionary to another dictionary. Values can be updated in the same way.
```
r1 = {'name': 'London1', 'location': 'London Str'}
r1.update({'vendor': 'Cisco', 'ios':'15.2'})
print(r1)

r1.update({'name': 'london-r1', 'ios':'15.4'})
print(r1)
```

A dictionary can be created with help of a **literal** and Construction **dict** allows you to create a dictionary.
```
r1 = {'model': '4451', 'ios': '15.4'}            #litral

r1 = dict(model='4451', ios='15.4')
r1 = dict([('model','4451'), ('ios','15.4')])
```

### Tuple
Tuple in Python is:
- a sequence of elements separated by a comma and enclosed in parentheses
- immutable ordered data type
Roughly speaking, a tuple is a list that can’t be changed. We can say that the tuple has read-only
permissions. It could be a defense against accidental change.
```
tuple1 = tuple()  #empty tuple
print(tuple1)
tuple2 = ('password',)  ## with element
print(tuple2)
```

#### Tuple from list
```
list_keys = ['hostname', 'location', 'vendor', 'model', 'ios', 'ip']
tuple_keys = tuple(list_keys)
print(tuple_keys)
print(tuple_keys[0])

# tuple_keys[1] = 'test'  ## will get error, that's immutable mean
```

### Set
Set is a mutable unordered data type. Set always contains only unique elements. Set in Python is a
sequence of elements that are separated by a comma and placed in curly braces. Set can easily remove repetitive elements:
```
vlans = [10, 20, 30, 40, 100, 10]
s= set(vlans)
print(s)
```

#### Set methods
Method **add** adds an item to set
```
set1 = {10,20,30,40}
set1.add(50)
print(sorted(set1))
```

Method **discard** allows deleting elements without showing an error if there is no element in set. Method **clear** empties set.
```
set1 = {10, 20, 30, 40, 50}
set1.discard(55)
print(set1)

set1.discard(50)
print(set1)

set1.clear()
print(set1)
```

#### Operations with sets
Union of sets can be obtained by **union** or operator **|**
Intersection of sets can be obtained by **intersection** or operator **&**
```
vlans1 = {10,20,30,50,100}
vlans2 = {100,101,102,102,200}
u = vlans1.union(vlans2)
print(u)
print(vlans1 | vlans2)

i = vlans1.intersection(vlans2)
print(i)
print(vlans1 & vlans2)
```

You cannot create an empty set using a literal set (in this case it will not be a set but a dictionary)
```
set1 = {}
print(type(set1))

#an empty set can be created in this way
set2 = set()
print(type(set2))

#Set from string
s = set('long long long long string')
print(s)

#Set from list:
l = set([10, 20, 30, 10, 10, 30])
print(l)
```

### Boolean values
Boolean values in Python are two constants True and False.
In Python, not only True and False are considered True and False values.
**True value**
- any non-zero number
- any non-empty string
- any non-empty object
  
 **False value:**
- 0
- None
- empty string
- empty object

To check boolean value of object you can use bool
```
items = [1, 2, 3]
empty_list = []
print(bool(empty_list))
print(bool(items))
print(bool(0))
print(bool(1))
```

### Types conversion
Python has several useful built-in features that allow data to be converted from one type to another.

**int** converts a string to int. Using int function you can convert a binary number into a decimal number (binary number must
be written as a string)
```
print(int("10"))
print(int("11111111", 2))
```

Function **list** converts an argument to a list
```
print(list("string"))
print(list({1, 2, 3}))
print(list((1, 2, 3, 4)))
```

Function **set** converts an argument into a set
```
print(set([1, 2, 3, 3, 4, 4, 4, 4]))
print(set((1, 2, 3, 3, 4, 4, 4, 4)))
print(set("string string"))
```

Function **tuple** converts argument into a tuple
```
print(tuple([1, 2, 3, 4]))
print(tuple({1, 2, 3, 4}))
print(tuple("string"))
#This can be useful if you want an immutable object.
```

Function **str** converts an argument into a string:
```
print(str(10))
```

### Types checking
**isdigit** method can be used to check whether a string consists only of digits
```
print("a".isdigit())
print("a10".isdigit())
print("10".isdigit())
```

Method **isalpha** makes it possible to check whether a string consists only of letters
```
print("a".isalpha())
print("a100".isalpha())
print("a-- ".isalpha())
print("a ".isalpha())
```

Method **isalnum** makes it possible to check whether a string consists of letters or numbers
```
print("a".isalnum())
print("a10".isalnum())
```
-----
### Tasks (Task များအားလုံးအား သင်ထားပြီးသော သင်ခန်းစာများကိုသာ အသုံးချ ဖြေဆိုရမည်)
#### ၁။ အောက်ပါ string (nat) မှ FastEthernet နေရာတွင် GigabitEthernet ကို အစားထိုးပြီး print ထုတ်ပြပါ။
```
nat = "ip nat inside source list ACL interface FastEthernet0/1 overload"
```

#### ၂။ အောက်ပါ mac မှ semicolon (:) နေရာတွင် dot(.) အစားထိုးပြီး print ထုတ်ပြပါ။
```
mac = "AAAA:BBBB:CCCC"
```

#### ၃။ အောက်ပါ config string ထဲမှ ["1", "3", "10", "20", "30", "100"] ကို list ပုံစံဖြင့် variable တစ်ခုထဲ ထည့်သွင်းပြီး print ထုတ်ပြပါ။
```
config = "switchport trunk allowed vlan 1,3,10,20,30,100"
```

#### ၄။ Netowrk Device များမှ ထုတ်ထားသော အောက်ပါ vlan list အတွင်းတွင် ထပ်နေသော vlan များကို ဖြတ်ထုတ်ပါ။ ဖြတ်ထုတ်ထားသော unique vlan များအား ascending order ဖြင့် စီပြီး print ထုတ်ပြပါ။
```
vlans = [10, 20, 30, 1, 2, 100, 10, 30, 3, 4, 10]
```

#### ၄။ အောက်ပါ cmd နှစ်ခုမှ ဘုံပါဝင်နေသော vlan နံပတ်(intersection)ကို list အနေဖြင့် variable ထဲထည့်သွင်းပြီး ထုတ်ပြပါ။ ( vlan နံပတ်သာ ဖြစ်ရမည်၊ ['1', '3', '8'] ကဲ့သို့ ဖြစ်ရမည်။
```
cmd1 = "switchport trunk allowed vlan 1,2,3,5,8"
cmd2 = "switchport trunk allowed vlan 1,3,8,9"
```

#### ၅။ အောက်ဖော်ပြပါ ospf_route string အား ဒုတိယပုံစံကဲ့သို့ ဖြစ်အောင် ဖော်ပြပါ။
```
ospf_route = " 10.0.24.0/24 [110/41] via 10.0.13.3, 3d18h, FastEthernet0/0"
```
Answer be Like..
```
Prefix 10.0.24.0/24
AD/Metric 110/41
Next-Hop 10.0.13.3
Last update 3d18h
Outbound Interface FastEthernet0/0
```

#### ၆။ mac string အား binary format string အဖြစ် ဖော်ပြပါ။ ( 101010101010101010111011101110111100110011001100)
```
mac = "AAAA:BBBB:CCCC"
```

#### ၇။ အောက်ဖော်ပြပါ ip string အား ဒုတိယပုံစံကဲ့သို့ ဖြစ်အောင် ဖော်ပြပါ။
```
ip = "192.168.3.1"
```
Answer be Like..
```
10 1 1 1
00001010 00000001 00000001 00000001
```
-----
### Basic Scripts
Generally speaking, script is a regular file. This file stores the sequence of commands that you want
to execute.
```
access_template = ['switchport mode access',
'switchport access vlan {}',
'switchport nonegotiate',
'spanning-tree portfast',
'spanning-tree bpduguard enable']
print('\n'.join(access_template).format(5))
```
Items in list are combined into a string that is separated by \n and VLAN number is inserted
into string using string formatting.

#### Executable file
In order for a file to be executable and not have to write “python” every time before calling a file,
you need to:
- make file executable (for Linux)
- the first line of file should have **#!/usr/bin/env python** or **#!/usr/bin/env python3** depend-
ing on which version of Python is used by default
```
#!/usr/bin/env python3
access_template = ['switchport mode access',
'switchport access vlan {}',
'switchport nonegotiate',
'spanning-tree portfast',
'spanning-tree bpduguard enable']
print('\n'.join(access_template).format(5))
```
After that
```
chmod +x access_template_exec.py
```
Now you can call file like this:
```
$ ./access_template_exec.py
```

#### Passing arguments to the script (sys.argv)
Very often script solves some common problem. For example, script processes a configuration file.
Of course, in this case you don’t want to edit name of file every time with your hands in script. It
will be much better to pass file name as script argument and then use already specified file. The
sys module allows working with script arguments via argv.
```
from sys import argv
interface = argv[1]
vlan = argv[2]
access_template = ['switchport mode access',
'switchport access vlan {}',
'switchport nonegotiate',
'spanning-tree portfast',
'spanning-tree bpduguard enable']
print('interface {}'.format(interface))
print('\n'.join(access_template).format(vlan))
```
```
$ python access_argv.py Gi0/7 4
```
Arguments that have been passed to script are substituted as values in template.
- argv is a list
- all arguments are in list and represented as strings
- argv contains not only arguments that passed to script but also name of script itself. First comes the name of script itself, then arguments in the same order.

#### User input
Sometimes it is necessary to get information from user. For example, request a password. The input function is used to get information from the user:
```
print(input('What is your faivorite routing protocol? '))
#What is your faivorite routing protocol? OSPF

protocol = input('What is your faivorite routing protocol? ')
print(protocol)
```

```
interface = input('Enter interface type and number: ')
vlan = input('Enter VLAN number: ')
access_template = ['switchport mode access',
                  'switchport access vlan {}',
                  'switchport nonegotiate',
                  'spanning-tree portfast',
                  'spanning-tree bpduguard enable']
print('\n' + '-' * 30)
print('interface {}'.format(interface))
print('\n'.join(access_template).format(vlan))
```
### Tasks (Task များအားလုံးအား သင်ထားပြီးသော သင်ခန်းစာများကိုသာ အသုံးချ ဖြေဆိုရမည်)
အောက်တွင် r1, r2, sw1 တို့အားပေးထားပါသည်။ user ထံမှ input တစ်ခု တောင်းပါ။ ထို input သည် r1 ဖြစ်လျှင် သူနဲ့ သက်ဆိုင်ရာကို ထုတ်ပြပေးရမည်။ r2, sw1 လည်းလျှင်လည်း သူနဲ့ သက်ဆိုင်ရာကို ထုတ်ပြပေးရမည်။ 
```
နမူနာ အဖြေ
$ python task_5_1.py
Enter name of device: r1
{"location": "21 New Globe Walk", "vendor": "Cisco", "model": "4451", "ios": "15.4", "ip": "10.255.0.1"}
```
```
london_co = {
"r1": {
      "location": "21 New Globe Walk",
      "vendor": "Cisco",
      "model": "4451",
      "ios": "15.4",
      "ip": "10.255.0.1"
     },
"r2": {
      "location": "21 New Globe Walk",
      "vendor": "Cisco",
      "model": "4451",
      "ios": "15.4",
      "ip": "10.255.0.2"
     },
"sw1": {
      "location": "21 New Globe Walk",
      "vendor": "Cisco",
      "model": "3850",
      "ios": "3.6.XE",
      "ip": "10.255.0.101",
      "vlans": "10,20,30",
      "routing": True
     }
}
```
-----
