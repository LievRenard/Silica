# Language Design



### Data Type

**Numerals**

default int = int32, real = double (or float64), complex = [double, double], byte = uint8

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
list2.append(2); //[2]
list2.prepend(1); //[1, 2]
```

**Dictionary**

```
dict<string, real> dict1 = ["Physics": 4.5, "Chemistry": 4, "Biology": 2];
dict1.append(["Geology": 3]);
```

**Range**

Built as struct

```
range a = 1..10; //a is from 1, 2, 3, ..., 10
```



### Control Statement

Control statements are functions.

**if statement**

```
//if: (dict<atom, func>) -> void

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
//for: (atom, range, func) -> void

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
  
  func<real> norm = &{ return sqrt(self.x^2+self.y^2); };
}
```

**Access Modifier**

There are two access modifier: private and static. When there is not any access modifier, the default is public.

```
class MyClass: (
	int a; //a is public member.
	private int b; //b is private member.
	static int c; ) -> { //c is static member. c is only called when MyClass.c
	
	func<void> myFunction1 = &{...} //myFunction1 is public function
	private func<void> myFunction2 = &{...} //myFunction2 is private function
	static func<void> myFunction3 = &{...} //myFunction3 is static function. Only called when Myclass.myFunction3()
```



### Operators

Operators are also functions.

**Arithmetic operators**

&plus; : Addition of two numbers

```
//func opAddition: (int, int) -> int
//func opAddition: (real, real) -> real
//func opAddition: (complex, complex) -> complex

print(1 + 2); //output 3
```

 &minus; : Subtraction of two numbers

```
//func opSubtraction: (int, int) -> int
//func opSubtraction: (real, real) -> real
//func opSubtraction: (complex, complex) -> complex

print(5 - 2); //output 3
```

&ast; : Multiplication of two numbers

```
//func opMultiplication: (int, int) -> int
//func opMultiplication: (real, real) -> real
//func opMultiplication: (complex, complex) -> complex

print(5 * 2); //output 10
```

 / : Division of two numbers. But division by int returns quotient.

```
//func opDivision: (int, int) -> int
//func opDivision: (real, real) -> real
//func opDivision: (complex, complex) -> complex

print(5 / 2); //output 2
print(5 / 2.0); //output 2.5
```

% : Modulo of two numbers.

```
//func opModulo: (int, int) -> int
//func opModulo: (real, real) -> real
//func opModulo: (complex, complex) -> complex

print(5 % 2); //output 1
```

^ : Power operation.

```
//func opPower: (int, int) -> int
//func opPower: (real, real) -> real
//func opPower: (complex, complex) -> complex

print(3^3); //output 27
print(4^0.5); //output 2
```

+=, -=, *=, /=, %=, ^= : Operation and assign. "x op= y" is same with "x = x op y".

```
int a = 5;
a += 9;
print(a); //output 14

a -= 4;
print(a); //output 10

a *= 2;
print(a); //output 20

a /= 4;
print(a); //output 5

a %= 3;
print(a); //output 2

a ^= 2;
print(a); //output 4
```
