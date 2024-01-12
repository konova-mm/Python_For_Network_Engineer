### Useful functions
- print
- range
- sorted
- enumerate
- zip
- all_any
- lambda
- map
- filter

#### print
```
print(*items, sep=' ', end='\n', file=sys.stdout, flush=False)
```
Function print outputs all elements by separating them by their sep value and finishes output with end value.
All elements that are passed as arguments are converted into strings:
```
def f(a):
  return a
print(1, 2, f, range(10))
```
For functions f and range the result is equivalent to str:
```
print(str(f))
print(str(range(10)))
```
#### sep
Parameter **sep** controls which separator will be used between elements.
By default, space is used.You can change sep value to any other string:
```
print(1, 2, 3)
print(1, 2, 3, sep='|')
print(1, 2, 3, sep='\n')
print(1, 2, 3, sep=f"\n{'-' * 10}\n")
```
#### end
Parameter **end** controls which value will be displayed after all elements are printed. By default, new
line character is used. You can change end value to any other string:
```
print(1, 2, 3)
print(1, 2, 3, end='\n' + '-' * 10)
```

#### file
Parameter file controls where values of print function are displayed. The default output is sys.stdout.
Python allows to pass to file as an argument any object with write(string) method.



#### Anonymous function (lambda expression)
In Python, lambda expression allows creation of anonymous functions - functions that are not tied to a name.
Anonymous function:
• may contain only one expression
• can pass as many arguments as you want
Standard function:
```
def sum_arg(a, b): return a + b
print(sum_arg(1, 2))
```
Similar anonymous function or lambda function:
```
sum_arg = lambda a, b: a + b
print(sum_arg(1, 2))
```
Note that there is no return operator in lambda function definition because there can only be one expression in this function that always returns a value and closes the function. Function lambda is convenient to use in expressions where you need to write a small function for data processing. For example, in sorted function you can use lambda expression to specify sorting key:
```
list_of_tuples = [('IT_VLAN', 320),
                ('Mngmt_VLAN', 99),
                ('User_VLAN', 1010),
                ('DB_VLAN', 11)]
print(sorted(list_of_tuples, key=lambda x: x[1]))
```
