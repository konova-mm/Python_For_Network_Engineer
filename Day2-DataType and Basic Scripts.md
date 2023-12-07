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

`print("1+2)`

`print("10-7)`

`print("12*5)`

`print("2**3)`

`print("10%7)`

-----
#### Float

`print("10/3)`

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
print(string1[-1])
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


