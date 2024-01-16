### Modules
Module in Python is a plain text file with Python code and .py extention. It allows logical ordering and grouping of the code. Division into modules can be done, for example, by this logic:
• division of data, formatting and code logic 
• grouping functions and other objects by functionality
The good thing about modules is that they allow you to reuse already written code and not copy it (for example, do not copy a previously written function).

#### Module import
Python has several ways to import a module:
• import module
• import module as
• from module import object
• from module import *

#### import module
```
print(dir())
```

```
import os
print(dir())
```
After importing the os module appeared in the output dir.This means that it is now in the current namespace.
To call some function or method from os module you should specify os. and then object name:
```
print(os.getlogin())
```
This import method is good because module objects do not enter the namespace of current program. That is, if you create a function named getlogin it will not conflict with the same function of os
module.

#### import module as
Construction import module as allows importing a module under a different name (usually shorter):
```
import subprocess as sp
sp.check_output('ping 8.8.8.8', shell=True)
```
#### from module import object
Option from module import object is convenient to use when only few functions are needed from whole module:
```
from os import getlogin, getcwd
```
These functions are now available in the current namespace:
```
dir()
```
They can be called without module name:
```
print(getlogin())
print(getcwd())
```
#### from module import *
Option from module import * imports all module names into the current namespace:
```
from os import *
print(dir())
```
There are many objects in os module, so the output is shortened. At the end, length of the list of names of current namespace is specified.
This import option is best not to use. With such code import it is not clear which function is taken, for example from os module. This makes it much harder to understand the code.

### Create your own modules
Module is a file with .py extension and Python code.
```
import ipaddress
def check_ip(ip):
  try:
    ipaddress.ip_address(ip)
    return True
  except ValueError as err:
    return False
ip1 = '10.1.1.1'
ip2 = '10.1.1'
print('Checking IP...')
print(ip1, check_ip(ip1))
print(ip2, check_ip(ip2))
```
File check_ip_function.py has created check_ip function which checks that argument is an IP address. This is done by using ipaddress module which will be discussed in the next section.
Function ipaddress.ip_address checks the correctness of IP address and generates ValueError exception if address is not validated. Function check_ip returns True if address is valid and False if
not. If you run check_ip_function.py script, the output is:
$ python check_ip_function.py
The second script imports check_ip function and uses it to select from address list only those that passed the check (get_correct_ip.py file):
```
from check_ip_function import check_ip
def return_correct_ip(ip_addresses):
  correct = []
  for ip in ip_addresses:
    if check_ip(ip):
      correct.append(ip)
  return correct
print('Cheking list of IP addresses')
ip_list = ['10.1.1.1', '8.8.8.8', '2.2.2']
correct = return_correct_ip(ip_list)
print(correct)
```
First line imports check_ip function from check_ip_function.py module.
$ python get_correct_ip.py

Note that not only information from get_correct_ip.py script is displayed, but also information from check_ip_function.py. This is because any type of import executes the entire script. That is, even
when import looks like from check_ip_function import check_ip, entire check_ip_function.py script is executed, not just check_ip function. As a result, all messages of imported script will be
displayed. Messages from imported script are not scary, they are just confusing. Worse when script performed some kind of connection to equipment and when importing a function from it, we will have to wait
for connection to take place. Python can specify that some strings should not be executed when importing. This is discussed in
the following subsection.
**Note**: Function return_correct_ip can be replaced by a filter or a list comprehension. Above is used the longer but most likely more understandable option:
```
list(filter(check_ip, ip_list))
[ip for ip in ip_list if check_ip(ip)]
def return_correct_ip(ip_addresses):
  return [ip for ip in ip_addresses if check_ip(ip)]
return_correct_ip(ip_list)
```
#### if __name__ == "__main__"
Often script can be executed independently and can be imported as a module by another script. Since importing a script runs this script, it is often necessary to specify that some strings should not
be executed when importing. In previous example there were two scripts: check_ip_function.py and get_correct_ip.py. And when starting get_correct_ip.py, print() from check_ip_function.py was displayed.
Python has a special technique that specifies that a code must not be executed at import: all lines that are in if __name__ == '__main__' block are not executed at import.
Variable __name__ is a special variable that will be equal to "__main__" only if file is run as the main program and is set equal to module name when importing the module. That is, if __name__ ==
'__main__' condition checks whether a file was run directly. As a rule, if __name__ == '__main__' block includes all function calls and information output on the standard output stream. That is, in check_ip_function.py script this block conytains everything
except import and return_correct_ip function:
```
import ipaddress
def check_ip(ip):
  try:
    ipaddress.ip_address(ip)
    return True
  except ValueError as err:
    return False
if __name__ == '__main__':
  ip1 = '10.1.1.1'
  ip2 = '10.1.1'
  print('Cheking IP...')
  print(ip1, check_ip(ip1))
  print(ip2, check_ip(ip2))
#python check_ip_function.py
```

When you start check_ip_function.py script directly, all lines are executed, because __name__ variable in this case is equal to '__main__'.
Script get_correct_ip.py remains unchanged
```
from check_ip_function import check_ip
def return_correct_ip(ip_addresses):
  correct = []
  for ip in ip_addresses:
    if check_ip(ip):
      correct.append(ip)
  return correct
print('Checking list of IP addresses')
ip_list = ['10.1.1.1', '8.8.8.8', '2.2.2']
correct = return_correct_ip(ip_list)
print(correct)
#python get_correct_ip.py
```
Now the output contains only information from script getcorrect__ip.py. In general, it is better to write all code that calls functions and outputs something to the standard
output stream inside if __name__ == '__main__' block.
**Warning**: Starting with Section 11, for tests to work correctly you have to always write a function call in task file within if __name__ == '__main__' block. The absence of this block
will not cause errors in all tasks, but it will still avoid problems.

-----
Tasks (Task များအားလုံးအား သင်ထားပြီးသော သင်ခန်းစာများကိုသာ အသုံးချ ဖြေဆိုရမည်)
-----
### Useful modules
