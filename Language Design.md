# Language Design



### Data Type

**Numerals**

default int = int32, real = double, complex = [double, double], byte = uint8

Variable declaration

```
int a;
a = 1;
```

Variable declaration with initialising

```
int a = 1;
real b = 2.5;
complex c = 1+3i;
byte d = 0x01;
```

**Bool**

```
bool a = true;
bool b = false;
```

**String**

```
string text = "Hello, World!";
```

**Array**

```
array<int> arr1 = (1, 2, 3, 4, 5);
array<int> arr2[5];
arr2[0] = 1;
```

**List**

Double linked list structure

```
list<int> list1 = (1, 2, 3, 4, 5);
list<int> list2;
list2.append(2); //list2 -> (2)
list2.prepend(1); //list2 -> (1, 2)
```

