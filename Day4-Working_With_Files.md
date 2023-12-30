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
f.writelines(cfg_lines)
f.close()
#cat r2.txt
```
As a result, all lines in the list were written into one line because there was no symbol \n at the end of lines. You can add newline character in different ways. For example, you can loop through a list:
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
f.writelines(cfg_lines)
f.close()
#cat r2.txt
cfg_lines2 = []

for line in cfg_lines:
    cfg_lines2.append(line + "\n")
print(cfg_lines2)

```
If the final list is written anew to the file, then it will already contain newlines
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
f.writelines(cfg_lines)
f.close()
#cat r2.txt
cfg_lines2 = []

for line in cfg_lines:
    cfg_lines2.append(line + "\n")
print(cfg_lines2)

f = open('r2.txt', 'w')
f.writelines(cfg_lines2)
f.close()
#cat r2.txt
```
#### File closing
Method close() met in File writing section. It was there to make sure that the content of file was
written on disk.

**Note:** In real life, the most common way to close files is use of **with** statement. It’s much more convenient way than to close file explicitly. But since you can also find **close** method in life, this section discusses how to use it. After you finish working with file you have to close it. In some cases Python can close file itself. But it’s best not to count on it and close file explicitly.
For this, Python has a separate flush method. But since in example with file writing there was no need to perform any more operations, file could be closed.
```
f = open('r1.txt', 'r')
print(f.read())
```
The file object has a special closed attribute that lets you check whether a file is closed or not. If
file is open, it returns False:
```
print(f.closed)
```
Now close file and check closed again:
```
f.close()
print(f.closed)
```
If you try to read file an exception will be raised:
```
print(f.read())
```
#### with statement
The **with** statement is called the **context manager**.Python has a more convenient way of working with files than the ones used so far - statement **with**. In addition, statement with guarantees file closure automatically.
```
with open('r1.txt', 'r') as f:
  for line in f:
    print(line)
```
In previous output there were extra empty lines between lines of the file because print adds another new line character.
To get rid of this you can use **rstrip** method.
```
with open('r1.txt', 'r') as f:
  for line in f:
    print(line.rstrip())
```
with statement can be used not only as a line-by-line reader, all methods that have been covered before also work:
```
with open('r1.txt', 'r') as f:
  print(f.read())
```
#### Open two files
Sometimes you have to work with two files simultaneously. For example, write some lines from one file to another.
In this case you can open two files in with block as follows-
```
with open('r1.txt') as src, open('result.txt', 'w') as dest:
  for line in src:
    if line.startswith('service'):
      dest.write(line)
#cat result.txt
```
This is equivalent to:
```
with open('r1.txt') as src:
with open('result.txt', 'w') as dest:
  for line in src:
    if line.startswith('service'):
      dest.write(line)
```
### Examples of working with files
This subsection covers working with files and brings together topics: files, loops, and conditions. When processing output of commands or configuration, often it will be necessary to write summary data to the dictionary. It is not always obvious how to handle the output of commands and how to deal with the output in general. 

#### Parsing column output
This example will deal with the output of sh ip int br command. From the output of command we need to get interface name and IP address. Interface name is dictionary key and IP address is value. At the same time, match must be made only for those interfaces with IP address assigned.
An example of sh ip int br output (sh_ip_int_br.txt file)
```
R1#show ip interface brief
Interface IP-Address OK? Method Status Protocol
FastEthernet0/0 15.0.15.1 YES manual up up
FastEthernet0/1 10.0.12.1 YES manual up up
FastEthernet0/2 10.0.13.1 YES manual up up
FastEthernet0/3 unassigned YES unset up down
Loopback0 10.1.1.1 YES manual up up
Loopback100 100.0.0.1 YES manual up up
```
Working_with_dict_example_1.py file:
```
result = {}
with open('sh_ip_int_br.txt') as f:
  for line in f:
    line = line.split()
    if line and line[1][0].isdigit():
      interface, address, *other = line
      result[interface] = address
print(result)
```
Command sh ip int br displays the output with columns. So desired fields are in the same line. Script processes the output line by line and divides each line using split() method. The resulting list contains output columns. Because we need only interfaces on which IP address is configured, first character of second column is checked: if first character is a number the address is
assigned to interface and string has to be processed. In interface, address, *other = line - variables are unpacked. Variable interface will have interface name, address will have IP address and other - all other fields. Since each line has a
key-value pair, they are assigned to dictionary: result[interface] = address.
The result of script execution will be a dictionary (here it is split into key-value pairs for convenience, in real script the dictionary output will be displayed in one line):
```
{'FastEthernet0/0': '15.0.15.1',
'FastEthernet0/1': '10.0.12.1',
'FastEthernet0/2': '10.0.13.1',
'Loopback0': '10.1.1.1',
'Loopback100': '100.0.0.1'}
```
#### Getting key and value from different output lines
Very often the output of commands looks like that key and value are in different lines. And you have to figure out how to process the output to get right match. For example, from the output of sh ip int br command you need to get match interface name – MTU (sh_ip_interface.txt file):
```
Ethernet0/0 is up, line protocol is up
Internet address is 192.168.100.1/24
Broadcast address is 255.255.255.255
Address determined by non-volatile memory
MTU is 1500 bytes
Helper address is not set
...
Ethernet0/1 is up, line protocol is up
Internet address is 192.168.200.1/24
Broadcast address is 255.255.255.255
Address determined by non-volatile memory
MTU is 1500 bytes
Helper address is not set
...
Ethernet0/2 is up, line protocol is up
Internet address is 19.1.1.1/24
Broadcast address is 255.255.255.255
Address determined by non-volatile memory
MTU is 1500 bytes
Helper address is not set
...
```
Interface name is in Ethernet0/0 is up, line protocol is up line and MTU in MTU is 1500 bytes line.
For example, try to remember interface each time and print its value when MTU parameter is detected, together with MTU value:
```
with open('sh_ip_interface.txt') as f:
  for line in f:
    if 'line protocol' in line:
      interface = line.split()[0]
    elif 'MTU is' in line:
      mtu = line.split()[-2]
      print('{:15}{}'.format(interface, mtu))
```
Command output is organized in such a way that there is always a line with interface first and then a line with MTU after several lines. If you remember the name of interface every time it appears and at the time when line matches MTU, the last memorized interface is the one which matches this MTU. Now, if you want to create a dictionary that matches interface – MTU, it’s enough to write values when MTU was found.
Working_with_dict_example_2.py file:
```
result = {}
with open('sh_ip_interface.txt') as f:
  for line in f:
    if 'line protocol' in line:
      interface = line.split()[0]
    elif 'MTU is' in line:
      mtu = line.split()[-2]
      result[interface] = mtu
print(result)
```
The result of script execution will be a dictionary (here it is split into key-value pairs for convenience, in real script the dictionary output will be displayed in one line):
```
{'Ethernet0/0': '1500',
'Ethernet0/1': '1500',
'Ethernet0/2': '1500',
'Ethernet0/3': '1500',
'Loopback0': '1514'}
```
This technique will be quite often useful because command output is generally organized in a very similar way.

#### Nested dictionary
If you want to get several parameters from the output, it is very convenient to use a dictionary with a nested dictionary. For example, from output sh ip interface you need to get two parameters:
IP address and MTU. First, output of information:
```
Ethernet0/0 is up, line protocol is up
Internet address is 192.168.100.1/24
Broadcast address is 255.255.255.255
Address determined by non-volatile memory
MTU is 1500 bytes
Helper address is not set
...
Ethernet0/1 is up, line protocol is up
Internet address is 192.168.200.1/24
Broadcast address is 255.255.255.255
Address determined by non-volatile memory
MTU is 1500 bytes
Helper address is not set
...
Ethernet0/2 is up, line protocol is up
Internet address is 19.1.1.1/24
Broadcast address is 255.255.255.255
Address determined by non-volatile memory
MTU is 1500 bytes
Helper address is not set
...
```
In the first step, each value is stored in a variable and then all three values are displayed. Values
are displayed when a string has MTU because it is the last string:
```
with open('sh_ip_interface.txt') as f:
  for line in f:
    if 'line protocol' in line:
      interface = line.split()[0]
    elif 'Internet address' in line:
      ip_address = line.split()[-1]
    elif 'MTU' in line:
      mtu = line.split()[-2]
      print('{:15}{:17}{}'.format(interface, ip_address, mtu))
```
It uses the same technique as in previous example but adds another nested dictionary:
```
result = {}
with open('sh_ip_interface.txt') as f:
  for line in f:
    if 'line protocol' in line:
      interface = line.split()[0]
      result[interface] = {}
    elif 'Internet address' in line:
      ip_address = line.split()[-1]
      result[interface]['ip'] = ip_address
    elif 'MTU' in line:
      mtu = line.split()[-2]
      result[interface]['mtu'] = mtu
print(result)
```

Each time an interface is detected, result dictionary creates a key with the name of interface that corresponds to an empty dictionary. This blank is used so that at the time when IP address or MTU is detected, parameter can be written into nested dictionary of the corresponding interface. The result of script execution will be a dictionary (here it is split into key-value pairs for convenience, in real script the dictionary output will be displayed in one line):
```
{'Ethernet0/0': {'ip': '192.168.100.1/24', 'mtu': '1500'},
'Ethernet0/1': {'ip': '192.168.200.1/24', 'mtu': '1500'},
'Ethernet0/2': {'ip': '19.1.1.1/24', 'mtu': '1500'},
'Ethernet0/3': {'ip': '192.168.230.1/24', 'mtu': '1500'},
'Loopback0': {'ip': '4.4.4.4/32', 'mtu': '1514'}}
```
#### Output with empty values
Sometimes, sections with empty values will be found in the output. For example, in case of output `sh ip interface`, interfaces may look like:
```
Ethernet0/1 is up, line protocol is up
Internet protocol processing disabled
Ethernet0/2 is administratively down, line protocol is down
Internet protocol processing disabled
Ethernet0/3 is administratively down, line protocol is down
Internet protocol processing disabled
```
Consequently, there is no MTU or IP address. And if you execute previous script for a file with such interfaces, the result is this (output for file sh_ip_interface2.txt):
```
{'Ethernet0/0': {'ip': '192.168.100.2/24', 'mtu': '1500'},
'Ethernet0/1': {},
'Ethernet0/2': {},
'Ethernet0/3': {},
'Loopback0': {'ip': '2.2.2.2/32', 'mtu': '1514'}}
```
If you need to add interfaces to dictionary only when an IP address is assigned to interface, you need to move the creation of key with interface name to a moment when line with IP address is detected (working_with_dict_example_4.py file):
```
result = {}
with open('sh_ip_interface2.txt') as f:
  for line in f:
    if 'line protocol' in line:
      interface = line.split()[0]
  elif 'Internet address' in line:
    ip_address = line.split()[-1]
    result[interface] = {}
    result[interface]['ip'] = ip_address
  elif 'MTU' in line:
    mtu = line.split()[-2]
    result[interface]['mtu'] = mtu
print(result)
```
In this case, the result will be a dictionary:
```
{'Ethernet0/0': {'ip': '192.168.100.2/24', 'mtu': '1500'},
'Loopback0': {'ip': '2.2.2.2/32', 'mtu': '1514'}}
```

### Tasks (Task များအားလုံးအား သင်ထားပြီးသော သင်ခန်းစာများကိုသာ အသုံးချ ဖြေဆိုရမည်)
၁။ အောက်ပါ ospf.txt ဖိုင်မှ စာကြောင်းများကို ဖော်ပြပါ output format အဖြစ် Stdout ပုံစံဖြင့် print ထုတ်ပြပါ။ ( Stdout - Standard Output )
ospf.txt
```
O        10.0.24.0/24 [110/41] via 10.0.13.3, 3d18h, FastEthernet0/0
O        10.0.28.0/24 [110/31] via 10.0.13.3, 3d20h, FastEthernet0/0
O        10.0.37.0/24 [110/11] via 10.0.13.3, 3d20h, FastEthernet0/0
O        10.0.41.0/24 [110/51] via 10.0.13.3, 3d20h, FastEthernet0/0
O        10.0.78.0/24 [110/21] via 10.0.13.3, 3d20h, FastEthernet0/0
O        10.0.79.0/24 [110/20] via 10.0.19.9, 4d02h, FastEthernet0/2
```
Output Format
```
Prefix 10.0.24.0/24
AD/Metric 110/41
Next-Hop 10.0.13.3
Last update 3d18h
Outbound Interface FastEthernet0/0
```

၂။ အောက်ဖော်ပြပါ config_sw1.txt ကို အသုံးပြုပြီး stdout အဖြစ် ပြန်လည်ဖော်ပြပါ။ ဖော်ပြသည့်အခါ **!** များကို ဖြုတ်ရမည်၊ Blank Line များ မပါဝင်စေရ၊ config_sw1.txt အား argument အနေဖြင့် အသုံးပြုရမည်။
config_sw1.txt
```
Current configuration : 2033 bytes
!
! Last configuration change at 13:11:59 UTC Thu Feb 25 2016
!
version 15.0
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname sw1
!
!
!
!
!
!
interface Ethernet0/0
 duplex auto
!
interface Ethernet0/1
 switchport trunk encapsulation dot1q
 switchport trunk allowed vlan 100
 switchport mode trunk
 duplex auto
 spanning-tree portfast edge trunk
!
interface Ethernet0/2
 duplex auto
!         
interface Ethernet0/3
 switchport trunk encapsulation dot1q
 switchport trunk allowed vlan 100
 duplex auto
 switchport mode trunk
 spanning-tree portfast edge trunk
!         
interface Ethernet1/0
 duplex auto
!
interface Ethernet1/1
 duplex auto
!
interface Ethernet1/2
 duplex auto
!
interface Ethernet1/3
 duplex auto
!
interface Vlan100
 ip address 10.0.100.1 255.255.255.0
!
!
alias configure sh do sh 
alias exec ospf sh run | s ^router ospf
alias exec bri show ip int bri | exc unass
alias exec id show int desc
alias exec top sh proc cpu sorted | excl 0.00%__0.00%__0.00%
alias exec c conf t
alias exec diff sh archive config differences nvram:startup-config system:running-config
alias exec shcr sh run | s ^crypto
alias exec desc sh int desc | ex down
alias exec bgp sh run | s ^router bgp
alias exec xc sh xconnect all
alias exec vc sh mpls l2tr vc
!
line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line aux 0
line vty 0 4
 login
 transport input all
!
end
```
Sample Result Output Format
```
$ python task_7_2.py config_sw1.txt
Current configuration : 2033 bytes
version 15.0
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
hostname sw1
interface Ethernet0/0
...
```
၃။ မေးခွန်း (၂) တွင် ရရှိသော script အား အောက်ပါ ignore ရှိ စာလုံးများပါသော စာကြောင်းများမထွက်သည့် လုပ်ဆောင်ချက် ထပ်ပေါင်းထည့်ပါ။
```
ignore = ["duplex", "alias", "Current configuration"]
```
၄။ မေးခွန်း (၃) တွင် ရရှိသော output အား Stdout မဖြစ်မထုတ်ပဲ output_config.txt file အဖြစ် သိမ်းဆည်းပါ။
