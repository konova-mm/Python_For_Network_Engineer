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
#### if \_\_name__ == "\_\_main__"
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
#### subprocess
Subprocess module allows you to create new processes. It can then connect to standard input/output/error streams and receive a return code.
Subprocess can for example execute any Linux commands from script. And depending on situation, get the output or just check that command has been performed correctly.
Function subprocess.run()
Function subprocess.run() is the main way of working with subprocess module.
The easiest way to use a function is to call it in this way:
```
import subprocess
result = subprocess.run('ls')
print(result)
```
The result variable now contains a special CompletedProcess object. From this object you can get information about execution of process, such as return code:
```
print(result.returncode)
```
Code 0 means that program was executed successfully. If it is necessary to call a command with arguments, it should be passed in this way (as a list):
```
result = subprocess.run(['ls', '-ls'])
print(result)
```
Another feature of run() If you try to run a ping command, for example, this aspect will be visible:
```
result = subprocess.run(['ping', '-c', '3', '-n', '8.8.8.8'])
print(result)
```
#### Getting the result of a command execution
By default, run() function returns the result of a command execution to a standard output stream. If you want to get the result of command execution, add stdout argument with value subprocess.PIPE:
```
result = subprocess.run(['ls', '-ls'], stdout=subprocess.PIPE)
print(result.stdout)
```
Now you can get the result of command executing in this way:
Note letter b before line. It means that module returned the output as a byte string. There are two options to translate it into unicode:
• decode received string
• specify encoding argument
Example with decode:
```
print(result.stdout.decode('utf-8'))
```
Example with encoding:
```
result = subprocess.run(['ls', '-ls'], stdout=subprocess.PIPE, encoding='utf-8')
print(result.stdout)
```
#### Output disabling
Sometimes it is enough to get only return code and need to disable output of execution result on standard output stream. This can be done by passing to run() function the stdout argument with value subprocess.DEVNULL:
```
result = subprocess.run(['ls', '-ls'], stdout=subprocess.DEVNULL)
print(result.stdout)
print(result.returncode)
```
#### Working with standard error stream
If command was executed with error or failed, the output of command will fall on standard error stream. This can be obtained in the same way as the standard output stream:
```
result = subprocess.run(['ping', '-c', '3', '-n', 'a'], stderr=subprocess.PIPE, encoding='utf-8')
```
Now result.stdout has empty string and result.stderr has standard output stream:
```
print(result.stdout)
print(result.stderr)
print(result.returncode)
```
### Examples of module use
Example of subprocess module use (subprocess_run_basic.py file):
```
import subprocess
reply = subprocess.run(['ping', '-c', '3', '-n', '8.8.8.8'])
if reply.returncode == 0:
  print('Alive')
else:
  print('Unreachable')
```
That is, the result of command execution is printed to standard output stream. Function ping_ip() checks the availability of IP address and returns True and stdout if address is available, or False and stderr if address is not available (subprocess_ping_function.py file):
```
import subprocess
def ping_ip(ip_address):
  """
  Ping IP address and return tuple:
  On success:
    * True
    * command output (stdout)
  On failure:
    * False
    * error output (stderr)
  """
  reply = subprocess.run(['ping', '-c', '3', '-n', ip_address],
  stdout=subprocess.PIPE,
  stderr=subprocess.PIPE,
  encoding='utf-8')
  if reply.returncode == 0:
    return True, reply.stdout
  else:
    return False, reply.stderr
print(ping_ip('8.8.8.8'))
print(ping_ip('a'))
```
Based on this function you can make a function that will check list of IP addresses and return as a result two lists: reachable and unreachable addresses.
If number of IP addresses to check is large, you can use threading or multiprocessing modules to speed up verification.

### os
