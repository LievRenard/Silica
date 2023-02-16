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

A bool is also an atom. true = :true, false = :false

```
bool a = true;
bool b = false;
```

**String**

```
string text = "Hello, World!";
```

**Atom**

```
atom status = :ok;
```

**Array**

```
array<int> arr1 = [1, 2, 3, 4, 5];
array<int> arr2[5];
arr2[0] = 1;
```

**List**

Double linked list structure

```
list<int> list1 = [1, 2, 3, 4, 5];
list<int> list2;
list2.append(2); //list2 -> [2]
list2.prepend(1); //list2 -> [1, 2]
```

**Dictionary**

```
dict<string, real> dict1 = ["Physics": 4.5, "Chemistry": 4, "Biology": 2];
dict1.append(["Geology": 3]);
```

**Range**

Build by struct

```
range a = 1..10; //a is from 1, 2, 3, ..., 9 (excluding 10)
```



### Control Statement

**if statement**

```
//if: (map<atom, func>) -> void

if << {
	...: &{...},
	...: &{...},
	:else: &{...} //:otherwise is also available
}
```

**for statement**

```
//for: (atom, array, func) -> void
//for: (atom, list, func) -> void

for(:i,[...]) << &{
	...
}
```

**while statement**

```
//while: (bool, func) -> void

while([condition]) << &{
	...
}
```



### Functions

**Named function**

```
func [name]: ([type1] [parameter1], [type2] [parameter2], ...) -> (return type) {
	...
	//if return type is not void
	return ...
}

//example: addition of 2 integers

func add: (int a, int b) -> void {
	return a+b;
}
```

**Anonymous function**

```
func<type1, type2, ..., returntype> [variable] = (var1, var2, ...) -> {...}
func<type1, type2, ..., returntype> [variable] = &{...}
//parameter in func is written as &1, &2, ...

//example: addition of 2 integers
func<int, int, int> add = (a, b) -> {return a+b;};
//or
func<int, int, int> add = &{return &1+&2;};

//It can be available to use only &{...} in case of no return value and parameter function
func<void> sayhello = &{print("Hello");};
```



### Class and Struct

**Struct**

```
struct [Name]: (
	[type1] [member variable1],
	... ) -> {	
	[member function]
	...
}
```

**Class**

```
class [Name]: (
	[type1] [member variable1],
	... ) -> {	
	[member function]
	...
}

//example: 2D cartesian point class with distance from origin function
class Point: (
	real x,
	real y ) -> {
	
	func<real, real, void> Point = &{
		self.x = &1;
    self.y = &2;
  };
  
  func<Point, real> norm = &{ return sqrt(&1.x^2+&1.y^2); };
}
```

