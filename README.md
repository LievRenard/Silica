# Silica

A programming language ...(explanation need)...

> There is only design plan of this language. Maybe first it will be interpreter language and its interpreter will be made with Rust.


## Language Design

[Here](https://github.com/LievRenard/Silica/blob/main/Language%20Design.md)

Data type: int, real, complex, atom, bool, string, array, list and dictionary.
<br>
Control statements: if, for, while.
<br>
Function, class and struct will be supported.
<br>
Will be static type language.


Example: print summation of integers from 1 to 100.
```
int sum = 0;
for (:i, 1..101) << &{
  sum += i;
}
print(sum);
```

## First Milestone

Making interpreter
Making integer, real number type and its operation.
