## Functions
Function:
• has a name to run this code block as many times as you want
- launch of function code is called a function call
• function parameters are usually defined when creating a function.
- function parameters determine which arguments a function can accept
- arguments can be passed to functions
- function code will be executed taking into account the specified arguments

#### What are functions for?
Typically, problems that code solves are very similar and often have something in common. For example, when working with configuration files each time it is necessary to perform such actions:
- file opening
- deletion (or skipping) of lines starting with exclamation mark (for Cisco)
- deleting (or skipping) empty lines
- deleting new line characters at the end of lines
- converting the result to a list
Beyond that, actions can vary depending on what needs to be done. Often there’s a piece of code that repeats itself. Of course, you can copy it from one script to another.
But this is very inconvenient because when you change code you have to update it in all files in which it is copied. It is much easier and more accurate to put this code into a function (it can also be several functions).
And then you will call this function - in this file or another one. This section discusses when a function is in the same file. And in 11. Modules we will see how to reuse objects that are in other scripts.

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
