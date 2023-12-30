## Functions
Function:
- has a name to run this code block as many times as you want
- launch of function code is called a **function call**
- function **parameters** are usually defined when creating a function.
- function **parameters** determine which arguments a function can accept
- **arguments** can be passed to functions
- function code will be executed taking into account the specified arguments

#### What are functions for?
Typically, problems that code solves are very similar and often have something in common. For example, when working with configuration files each time it is necessary to perform such actions:
- file opening
- deletion (or skipping) of lines starting with exclamation mark (for Cisco)
- deleting (or skipping) empty lines
- deleting new line characters at the end of lines
- converting the result to a list
Beyond that, actions can vary depending on what needs to be done. Often there’s a piece of code that repeats itself. Of course, you can copy it from one script to another.
But this is very inconvenient because when you change code you have to update it in all files in which it is copied. It is much easier and more accurate to put this code into a function (it can also be several functions). And then you will call this function - in this file or another one. This section discusses when a function is in the same file. And in 11. Modules we will see how to reuse objects that are in other scripts.

#### Creation of functions
- functions are created with a reserved word **def**
- **def** followed by function name and parentheses
- **parameters** that function accepts inside parentheses
- after parentheses goes colon and from a new line with indent there is a block of code that function executes
- optionally, the first line can be **docstring**
- function can use **return** operator, it is used to terminate and exit a function,most often return operator returns some value
```
def configure_intf(intf_name, ip, mask):
  print('interface', intf_name)
  print('ip address', ip, mask)
```

Function **configure_intf** creates an interface configuration with specified name and IP address. Function has three parameters: intf_name, ip, mask. When function is called the real data will replace these parameters.

-----

**Note:** When function is created, it does nothing yet. Actions listed in it will be executed only when you call function. This is something like ACL in network equipment: when creating ACL in
configuration, it does nothing until it is applied.

-----

#### Function cal
When calling a function you must specify its name and pass arguments if necessary.
**Note:** Parameters are variables that are used to create a function. Arguments are the actual values (data) that are passed to functions when called.
Function configure_intf expects three values when called because it was created with three parameters:
```
def configure_intf(intf_name, ip, mask):
  print('interface', intf_name)
  print('ip address', ip, mask)
configure_intf('F0/0', '10.1.1.1', '255.255.255.0')
```
The current version of the configure_intf function prints commands to a standard output, commands can be seen but the result of function cannot be saved to a variable.
For example, sorted function does not simply print the sorting result to standard output stream but returns it, so it can be saved to variable in this way:
```
items = [40, 2, 0, 22]
print(sorted(items))

sorted_items = sorted(items)
print(sorted_items)
```
#### Operator return
Operator **return** is used to return a value, and at the same time it exits the function. Function can return any Python object. By default, function always returns **None**. In order for configure_intf function to return a value that can then be assigned to a variable, you must use **return** operator:
```
def configure_intf(intf_name, ip, mask):
    config = f'interface {intf_name}\nip address {ip} {mask}'
    return config
result = configure_intf('Fa0/0', '10.1.1.1', '255.255.255.0')
print(result)
```
Now the result variable contains a line with commands to configure interface. In real life, function will almost always return some value. Another important aspect of return operator is that after return the function closes, meaning that
the expressions that follow return are not executed. For example, in function below the line «Configuration is ready» will not be displayed because it stands after return:
```
def configure_intf(intf_name, ip, mask):
  config = f'interface {intf_name}\nip address {ip} {mask}'
  return config
  print('Configuration is ready')
configure_intf('Fa0/0', '10.1.1.1', '255.255.255.0')
```
Function can return multiple values. In this case, they are separated by a comma after return operator. In fact, function returns tuple:
```
def configure_intf(intf_name, ip, mask):
  config_intf = f'interface {intf_name}\n'
  config_ip = f'ip address {ip} {mask}'
  return config_intf, config_ip

result = configure_intf('Fa0/0', '10.1.1.1', '255.255.255.0')
result

type(result)

intf, ip_addr = configure_intf('Fa0/0', '10.1.1.1', '255.255.255.0')
intf
ip_addr
```

#### Namespace. Scope of variables
Variables in Python have a scope. Depending on location in code where variable has been defined, scope is also defined, it determines where variable will be available. When using variable names in a program, Python searches, creates or changes these names in the corresponding namespace each time. Namespace that is available at each moment depends on area in which code is located. Python has a LEGB rule that it uses for variables search. For example, when accessing a variable within a function, Python searches for a variable in this order in scopes (before the first match):
- L (local) - in local (within function)
- E (enclosing) - in local area of outer functions (these are functions within which our function is located)
- G (global) - in global (in script)
- B (built-in) - in built-in (reserved Python values)
Accordingly, there are local and global variables:
• local variables:
- variables that are defined within function
- these variables become unavailable after exit from function
• global variables:
- variables that are defined outside the function
- these variables are ‘global’ only within a module
- for example, to be available in another module they must be imported
```
def configure_intf(intf_name, ip, mask):
  intf_config = f'interface {intf_name}\nip address {ip} {mask}'
  return intf_config
print(intf_config)
```
Note that intf_config variable is not available outside of function. To get the result of a function you must call a function and assign result to a variable:
```
result = configure_intf('F0/0', '10.1.1.1', '255.255.255.0')
print(result)
```
#### Function parameters and arguments
The purpose of creating a function is typically to take a piece of code that performs a particular task to a separate object. This allows you to use this piece of code multiple times without having to re-create it in program.
Typically, a function must perform some actions with input values and produce an output. When working with functions it is important to distinguish:
- parameters - variables that are used when creating a function.
- arguments - actual values (data) that are passed to function when called.
For a function to receive incoming values, it must be created with parameters (func_check_passwd.py file)
```
def check_passwd(username, password):
  if len(password) < 8:
    print('Password is too short')
    return False
  elif username in password:
    print('Password contains username')
    return False
  else:
    print(f'Password for user {username} has passed all checks')
    return True
```
In this case, function has two parameters: username and password. Function checks password and returns False if checks fail and True if password passed checks:
```
print(check_passwd('nata', '12345'))
print(check_passwd('nata', '12345lsdkjflskfdjsnata'))
print(check_passwd('nata', '12345lsdkjflskfdjs'))
```
When defining a function in this way it is necessary to pass both arguments. If only one argument is passed, there is an error:
```
print(check_passwd('nata'))
```
#### Function parameter types
When creating a function you can specify which arguments must be passed and which must not. Accordingly, a function can be created with:
- required parameters
- optional parameters (with default values)

