### Useful functions
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
