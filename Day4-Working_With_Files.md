## Working with files
In real life, in order to make full use of everything covered before this section you need to understand how to work with files.
When working with network equipment (and not only), files can be:
- configurations (simple, non-structured text files)
  - They are discussed in this section
    
- configuration templates
  - usually a special file format.

- files with connection options
  - usually they are structured files in some particular format: YAML, JSON, CSV

- other Python scripts
-----
This section covers simple text files. For example, Cisco configuration file.
There are several aspects to working with files:
- opening/closing
- reading
- writing
-----
### File opening
To start working with a file you have to open it.

Function **open** is most often used to open files:
```
file = open('file_name.txt', 'r')
```

Function **open** creates a file object to which different methods can then be applied to work with it.
File opening modes:
- **r** - open file in read-only mode (default)
- **r+** - open file for reading and writing
- **w** - open file for writing only
- if file exists, its content is removed
- if file does not exist, a new one is created
- **w+** - open file for reading and writing
- if file exists, its content is removed
- if file does not exist, a new one is created
- **a** - open file to add a data. Data is added to the end of file
- **a+** - open file for reading and writing. Data is added to the end of file

#### File reading
Python has several file reading methods:
- read - reads the contents of file to string
- readline - reads file line by line
- readlines - reads file lines and creates a list from the lines

**r1.txt**
```
!
service timestamps debug datetime msec localtime show-timezone year
service timestamps log datetime msec localtime show-timezone year
service password-encryption
service sequence-numbers
!
no ip domain lookup
!
ip ssh version 2
!
```

Method **read** reads the entire file to one string:
```
f = open('r1.txt')
print(f.read())
```

File can be read line by line using **readline** method:
```
f = open('r1.txt')
print(f.readline())
```
Another useful method is **readlines**. It reads file lines to the list:
```
f = open('r1.txt')
print(f.readline())
```
If you want to get lines of a file but without a new line character at the end, you can use split method and specify symbol \n as a separator.
```
f = open('r1.txt')
print(f.read().split('\n'))
print(f.read().rstrip().split('\n')) #if you use split before rstrip, list will be without empty string at the end
```
#### File writing
When writing information to a file, it is very important to specify the correct mode for opening the file, so as not to accidentally delete it:
- w - open file for writing. If file exists, its content is removed
- a - open file to add data. Data is appended to the end of the file
Both modes create a file if it does not exist

The following methods are used to write to a file:
- write - write one line to file
- writelines - allows to send as argument a list of strings

Method **write** expects string to write.
```
cfg_lines = ['!',
  'service timestamps debug datetime msec localtime show-timezone year',
  'service timestamps log datetime msec localtime show-timezone year',
  'service password-encryption',
  'service sequence-numbers',
  '!',
  'no ip domain lookup',
  '!',
  'ip ssh version 2',
  '!']
f = open('r2.txt', 'w')
cfg_lines_as_string = '\n'.join(cfg_lines)  ##Convert the list of commands to one large string using join
print(cfg_lines_as_string)
f.write(cfg_lines_as_string)
f.write('\nhostname r2') ##add a string manually
f.close()
```
#### writelines
Method writelines expects list of strings as an argument.
