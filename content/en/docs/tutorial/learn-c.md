---
title: "🛤 Learn C"
description: ""
lead: ""
date: 2023-06-24T04:24:42+02:00
lastmod: 2023-06-24T04:24:42+02:00
draft: false
images: []
menu:
  docs:
    parent: ""
    identifier: "learn-c-1739e66f136fda5f8ed029777e9b0262"
weight: 999
toc: true
---

# learn-c

## My code while learning C and some data for you

Szymon Bronisław Błaszczyński © 2023 [museyoucoulduse@gmail.com](mailto:museyoucoulduse@gmail.com)

> For those seeking peace at time of war, and those at war in time of peace.

<font size="1">Powered by [https://cj.rs/riss](https://cj.rs/riss)</font>

___


## first-one

### Overview

This program greets my cat in many colors. The trick used here is simple, you take number 31, which stands for
red, and iterates until 37, meaning it will never hit 38, thus `i < 38`. All of this lays inside for loop
with `man 3 printf` statements that clears color encoding with `\033[0m` and interpolates `i` variable as a 
decimal - `%d`. At the end of each loop there is a `\n` character that mean to break a line and start over.

Overall program1 will print 7 times this sentence in different color:

```
Cześć Nutek, mówi Szymon!
```

[![asciicast](https://asciinema.org/a/563448.svg)](https://asciinema.org/a/563448?autoplay=1&speed=2&theme=solarized-dark)

### Why?

I'm reading __Learn C The Hard Way__ by _Zed Shaw_ probably availabla here - `help@learncodethehardway.org`.
The first task was to create a program that does something with 100 km away, so after hacking colors in _bash_
earlier the day, I thought it would be cool to start a new learning project to lay a ground for my future work.
Maybe you will get something from this too.

### What's next?

#### Reading and writing

Don't worry I have skills, so you can follow along. My language is somewhat all around the computer, but just in
case I have __ChatGPT__ to help me along the way. Set sail!

#### Makefile

There wouldn't be any of this if not __Copilot's__ long description of macros in my small _Makefile_. It made
me jelous about the technical writing skills of AI robot vs a human being, and I know that there is a room for
both.

```Makefile
CFLAGS=-Wall -g
```

This, first, line tells that every compiler command should warn us about anything wrong in the code. Something
like this:

```c
program1.c:5:11: error: array initializer must be an initializer list
    char *name[] = "Szymon";
          ^
program1.c:7:61: warning: format specifies type 'char *' but the argument has type 'char **' [-Wformat]
        printf("\033[0;\"%d\"mCześć Nutek, mówi %s.", i, name);
                                                ~~       ^~~~
1 warning and 1 error generated.
```

You can clearly see, that I tried to duplicate the `*argv[]` declaration inside main function, which produced
an error, and then I get someow related warning that my string interpolation is not the type it should be.

#### Compilation

You can compile your program with just invoking `clang input.c -o program`, but I have also made object file,
with `clang -c program1.c`, that will be neccesairly later in debuging in __lldb__ (you can use _gdb_). I had 
no idea how to do this, because all of my linking, object creating and compiling was with higher order 
programming languages, so I relied on _Copilot_ code generation. It also made me a clean task for easier 
management.

## printf();

In C programming language, the `printf()` function is used to output data to the console or terminal window. 
It is a powerful function that can be used to format and print various types of data, including text, numbers, 
and variables. Some of the things you can do with the `printf()` function include:

1. Print text: You can use the `printf()` function to output any text that you want to the console. For example,
`printf("Hello, world!");` will output the text "Hello, world!" to the console.

2. Print variables: You can use the `%d` format specifier to print integer variables, `%f` to print float variables,
`%c` to print character variables, and `%s` to print string variables. For example, `int x = 10; printf("The value of x is %d", x);` will output "The value of x is 10" to the console.

3. Format output: You can use a wide range of formatting options with the `printf()` function to control how 
your output is displayed. For example, you can specify the width and precision of numbers, add leading zeros, 
and control the alignment of your output.

### Precision of floating point number

To display a floating point number with a precision of two decimal places using the `printf()` function in C, 
you can use the `%0.2f` format specifier.

```c
#include <stdio.h>

int main() {
    float number = 3.14159;
    printf("The number is: %.2f\n", number);
    return 0;
}
```

This will display number `3.14`

### Leading zeros

To display a number with six leading zeros in C, you can use the `%06d` format specifier with the `printf()` 
function.

```c
#include <stdio.h>

int main() {
    int number = 42;
    printf("The number with six leading zeros is: %06d\n", number);
    return 0;
}
```

This will display number 000042

### Hexadecimal output

#### Integer

To display an integer in hexadecimal format using the `printf()` function in C, you can use the `%x` format 
specifier.

```c
#include <stdio.h>

int main() {
    int number = 255;
    printf("The number in hexadecimal format is: %x\n", number);
    return 0;
}
```

In this example, the number variable is an integer type with the value of 255. The `printf()` function is used 
to output the value of number in hexadecimal format using the format specifier `%x`. The output will be 
"The number in hexadecimal format is: ff".

### Float

Note that the `%x` format specifier only works with integers. If you want to display a floating point number 
in hexadecimal format, you can use the `%a` format specifier instead. For example:

```c
#include <stdio.h>

int main() {
    float number = 3.14159;
    printf("The number in hexadecimal format is: %a\n", number);
    return 0;
}
```

In this example, the number variable is a floating point type with the value of _3.14159_. The `printf()`
function is used to output the value of number in hexadecimal format using the `%a` format specifier. 
The output will be "The number in hexadecimal format is: 0x1.921fap+1".

### String

To display a string as a sequence of hexadecimal values using the `printf()` function in C, you can use the 
`%x` or `%X` format specifier in combination with a loop that iterates through each character in the string.

Here's an example code snippet that shows how to do this using the %x format specifier:

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[] = "Hello, world!";
    int len = strlen(str);
    for (int i = 0; i < len; i++) {
        printf("%x ", str[i]);
    }
    printf("\n");
    return 0;
}
```

In this example, the str variable is a string that contains the text "Hello, world!". The len variable is the 
length of the string, which is obtained using the `strlen()` function. The for loop iterates through each 
character in the string, and the `printf()` function is used to output the hexadecimal value of each character 
using the `%x` format specifier. The output will be a sequence of hexadecimal values, one for each character 
in the string.

Note that the `%x` format specifier displays the hexadecimal value of each character using lowercase letters 
(a-f) for values greater than 9. If you want to use uppercase letters (A-F) instead, you can use the `%X` format
specifier.

3. ...continur on what `printf()` can do...

4. Print special characters: You can use special escape sequences to print characters such as tabs, newlines, 
and quotes. For example, `printf("This is a tab:\tAnd this is a newline:\n");` will output "This is a tab: And
this is a newline:" to the console.

### Ring a bell

```c
#include <stdio.h>

int main() {
    printf("\a");
    return 0;
}
```

This program will ring a system bell if it can. Check it out! Here is some trivia: In this example, the `\a` 
escape sequence is used to generate the ASCII bell character, which will cause the system to ring the bell. 
The `printf()` function is used to output the bell character to the console. When you run this program, the 
system will ring the bell once.

Note that the behavior of the `\a` escape sequence may vary depending on the system and terminal emulator 
you are using. In some cases, it may not actually ring the system bell, but instead generate a visual or 
auditory signal in some other way.

5. Use conditionals: You can use conditional statements within the printf() function to output different text
based on the value of a variable. For example, `int x = 10; printf("x is %s", x > 5 ? "greater than 5" : "less than or equal to 5");` will output "x is greater than 5" to the console.

These are just a few examples of what you can do with the printf() function in C programming language. It is a versatile and powerful function that you can use to output all kinds of data to the console.

## C operators

In C programming language, there are different types of operators that can be used to perform various operations on values. Here are some of the most commonly used operators in C:

### Arithmetic Operators:

`+` : Addition
`-` : Subtraction
`*` : Multiplication
`/` : Division
`%` : Modulo (Remainder)

### Comparison Operators:

`==` : Equal to
`!=` : Not equal to
`<` : Less than
`>` : Greater than
`<=` : Less than or equal to
`>=` : Greater than or equal to

### Logical Operators:

`&&` : Logical AND
`||` : Logical OR
`!` : Logical NOT

### Assignment Operators:

`=` : Assign value
`+=` : Add and assign value
`-=` : Subtract and assign value
`*=` : Multiply and assign value
`/=` : Divide and assign value
`%=` : Modulo and assign value

### Increment and Decrement Operators:

`++` : Increment by 1
`--` : Decrement by 1

### Bitwise Operators:

`&` : Bitwise AND
`|` : Bitwise OR
`^` : Bitwise XOR
`~` : Bitwise NOT
`<<` : Bitwise left shift
`>>` : Bitwise right shift

### Ternary Operator:

`? :` : Conditional operator (also known as ternary operator)

These are some of the most commonly used operators in C. Understanding how to use these operators can help you 
perform various operations on data in your C programs.

### Pointers 

Pointers are used to store memory addresses of variables. To manipulate and access the data stored at those 
memory locations, pointer operators are used. Here are some of the most commonly used pointer operators in C:

`&` operator:

The `&` operator is used to get the address of a variable.
Example: `int x = 10; int* ptr = &x;` will assign the address of the variable x to the pointer ptr.

`*` operator:

The * operator is used to access the value stored at the memory address pointed to by a pointer.
Example: `int x = 10; int* ptr = &x; int y = *ptr;` will assign the value of x (which is 10) to the variable y.

`++` and `--` operators:

The `++` and `--` operators can be used to increment or decrement the memory address pointed to by a pointer.
Example: `int arr[] = {1, 2, 3}; int* ptr = arr; ptr++;` will increment the pointer ptr to point to the next 
element in the array.

`->` operator:

The `->` operator is used to access a member of a structure or union through a pointer.
Example: `struct Point { int x, y; }; struct Point p = {1, 2}; struct Point* ptr = &p; int x = ptr->x;` 
will assign the value of p.x (which is 1) to the variable x.

`[]` operator:

The `[]` operator can be used to access elements of an array through a pointer.
Example: `int arr[] = {1, 2, 3}; int* ptr = arr; int x = ptr[1];` will assign the value of arr[1] (which is 2) 
to the variable x.

These are some of the most commonly used pointer operators in C. Understanding how to use these operators can 
help you manipulate and access data stored in memory through pointers.

## C keywords

* `auto`: This keyword is used to define local variables that are automatically initialized to garbage values.

* `break`: This keyword is used to exit a loop or switch statement early.

* `case`: This keyword is used to define a case in a switch statement.

* `char`: This keyword is used to define a character variable.

* `const`: This keyword is used to define a variable as constant, i.e., its value cannot be changed.

* `continue`: This keyword is used to skip to the next iteration of a loop.

* `default`: This keyword is used to define the default case in a switch statement.

* `do`: This keyword is used to define a do-while loop.

* `double`: This keyword is used to define a double-precision floating-point variable.

* `else`: This keyword is used to define an alternative branch in an if statement.

* `enum`: This keyword is used to define an enumeration type.

* `extern`: This keyword is used to declare a variable or function that is defined in another file.

* `float`: This keyword is used to define a single-precision floating-point variable.

* `for`: This keyword is used to define a for loop.

* `goto`: This keyword is used to jump to a labeled statement.

* `if`: This keyword is used to define a conditional statement.

* `int`: This keyword is used to define an integer variable.

* `long`: This keyword is used to define a long integer variable.

* `register`: This keyword is used to define local variables that are stored in the CPU registers.

* `return`: This keyword is used to return a value from a function.

* `short`: This keyword is used to define a short integer variable.

* `signed`: This keyword is used to define a signed integer variable.

* `sizeof`: This keyword is used to determine the size of a variable or data type.

* `static`: This keyword is used to define local variables that are only initialized once and retain 
their values between function calls.

* `struct`: This keyword is used to define a structure type.

* `switch`: This keyword is used to define a switch statement.

* `typedef`: This keyword is used to define a new data type.

* `union`: This keyword is used to define a union type.

* `unsigned`: This keyword is used to define an unsigned integer variable.

* `void`: This keyword is used to define a function that does not return a value, or to define a pointer
to an unspecified data type.

* `volatile`: This keyword is used to tell the compiler that a variable's value may change at any time,
so it should not optimize out reads or writes to it.

```
auto     double   int      struct
break    else     long     switch
case     enum     register typedef
char     extern   return   union
const    float    short    unsigned
continue for      signed   void
default  goto     sizeof   volatile
do       if       static   while
```

## C language constructs

### if

* `if`: The `if` statement is used for conditional execution of code. Here's an example:

```
int x = 5;
if (x > 0) {
    printf("x is positive\n");
}
```

This code will print "x is positive" because the condition `x > 0` is true.

### switch

* `switch`: The `switch` statement is used for multi-way branching. Here's an example:

```
int day = 3;
switch (day) {
    case 1:
        printf("Monday\n");
        break;
    case 2:
        printf("Tuesday\n");
        break;
    case 3:
        printf("Wednesday\n");
        break;
    default:
        printf("Unknown day\n");
        break;
}
```

This code will print "Wednesday" because the variable `day` is set to 3.

### while

* `while`: The `while` statement is used for loop execution as long as a condition is true. Here's an example:

```
int i = 0;
while (i < 10) {
    printf("%d\n", i);
    i++;
}
```

This code will print the numbers 0 through 9 because the condition `i < 10` is true for those values of `i`.

### do while

* `do while`: The `do while` statement is used for loop execution at least once, and then repeatedly as
long as a condition is true. Here's an example:

```
int i = 0;
do {
    printf("%d\n", i);
    i++;
} while (i < 10);
```

This code will print the numbers 0 through 9 because the `do` block is executed at least once, and then 
repeatedly as long as the condition `i < 10` is true.

### for

* `for`: The `for` statement is used for loop execution with a fixed number of iterations. Here's an example:

```
for (int i = 0; i < 10; i++) {
    printf("%d\n", i);
}
```

This code will print the numbers 0 through 9 because the loop runs for 10 iterations with the variable `i`
starting at 0 and incrementing by 1 each time.

### goto

* `goto`: The `goto` statement is used for unconditional branching to a labeled statement. Here's an example:

```
int i = 0;
start:
printf("%d\n", i);
i++;
if (i < 10) {
    goto start;
}
```

This code will print the numbers 0 through 9 because the `goto` statement jumps back to the `start` label as 
long as the condition `i < 10` is true.

### function

* Function: A function is a named block of code that can be called from other parts of the program. 
Here's an example:

```
int add(int a, int b) {
    return a + b;
}

int result = add(3, 4);
printf("%d\n", result);
```

This code defines a function called `add` that takes two integer arguments and returns their sum. 
It then calls the `add` function with arguments 3 and 4 and prints the result, which is 7.

### typedef

* Typedef: The `typedef` keyword is used to define a new type based on an existing type. Here's an example:

```
typedef int myint;
myint x = 5;
```

This code defines a new type called `myint` that is an alias for the `int` type. It then declares a 
variable `x` of type myint and initializes it to 5.

### struct

* Struct: A `struct` is a user-defined data type that groups together related data items. Here's an example:

```
struct Person {
    char name[50];
    int age;
    float height;
};

struct Person john = {"John", 30, 1.75};
printf("%s is %d years old and %f meters tall\n", john.name, john.age, john.height);
```

This code defines a `struct` called `Person` that contains a character array for the name, an integer
for the age, and a floating-point number for the height. It then declares a variable `john` of type
`Person` and initializes its fields with values. Finally, it prints out some information about `john`.

### typedef struct

* Typedef struct: The `typedef struct` keyword combination is used to define a new type based on a `struct` 
type. Here's an example:

```
typedef struct {
    char title[50];
    int year;
} Book;

Book book = {"The Catcher in the Rye", 1951};
printf("%s was published in %d\n", book.title, book.year);
```

This code defines a new type `Book` based on an anonymous `struct` that contains a character array for the 
title and an integer for the year. It then declares a variable `book` of type `Book` and initializes its 
fields with values. Finally, it prints out some information about the book.

### union

* Union: A `union` is a user-defined data type that can hold data of different types in the same memory 
location. Here's an example:

```
union Data {
    int i;
    float f;
    char str[20];
};

union Data data;
data.i = 10;
printf("data.i = %d\n", data.i);
data.f = 3.14;
printf("data.f = %f\n", data.f);
strcpy(data.str, "Hello");
printf("data.str = %s\n", data.str);
```

This code defines a `union` called `Data` that can hold an integer, a floating-point number, or a character 
array. It then declares a variable `data` of type `Data` and initializes its integer field with a value. It 
then sets the floating-point field and the character array field to other values and prints out some 
information about `data`. Note that only one field of the `union` can be accessed at a time, and the other
fields may contain garbage data.

### difference between union and struct

In C, a `struct` is a user-defined data type that groups together related data items of different types. 
Each field within a `struct` has its own memory location, and all fields are allocated memory simultaneously.
Each field can be accessed independently and manipulated as needed.

On the other hand, a `union` is also a user-defined data type that can hold data of different types 
in the same memory location. Unlike a `struct`, a `union` can only hold one value at a time, and all fields 
share the same memory location. When a new value is assigned to a field of a `union`, the previous value 
is overwritten. Accessing any field of the union returns the currently stored value, regardless of what type
it is.

The main difference between a `struct` and a `union` is how they use memory. A `struct` allocates memory 
for all of its fields simultaneously, while a `union` allocates memory for only one of its fields at a time.
This makes `unions` more space-efficient than `structs` in certain situations, but also less flexible, 
since only one field can be accessed at a time.

Another important difference is that the size of a `struct` is the sum of the sizes of all its fields, 
while the size of a `union` is the size of its largest field. This means that the memory allocation 
of a `union` is based on its largest field, which may waste memory if the other fields are smaller.

In summary, a `struct` is used to group related data items of different types together, while a `union`
is used to represent different types of data in the same memory location. Both `structs` and `unions`
have their own unique uses and advantages depending on the situation.

## Why learn C?

Learning C language can be a great foundation for future development in other programming languages. 
Here are some steps you can take to learn C language quickly, reliably, and with the best results for 
future development:

1. Start with the basics: Begin by understanding the fundamentals of programming such as data types, 
variables, operators, loops, and functions. You can refer to a good C programming book or online tutorial 
to understand these concepts.

2. Practice coding: The best way to learn any programming language is by writing code. Try to solve small 
problems using C language, and gradually move to more complex problems. You can find many online platforms 
and coding challenges to practice your skills.

    - [Codewars.com](https://www.codewars.com/)

3. Learn from other people's code: Look at other people's code and try to understand how they are solving 
problems using C language. You can find open-source projects on GitHub or other platforms, read through 
the code and try to understand how it works.

    - [GitHub](https://github.com)

4. Get familiar with tools and IDEs: Use an Integrated Development Environment (IDE) that supports C 
programming. IDEs like CodeBlocks, Dev-C++, or Visual Studio Code can be helpful in writing and 
debugging code. Also, get familiar with tools like GCC and Makefile, which can be useful in compiling 
and building C code.

    - [Neovim](https://neovim.io/)

5. Keep learning and updating yourself: C language is a foundational language for many other programming 
languages, so it's important to keep learning and updating yourself with the latest developments in C 
language. Join online forums and communities, participate in discussions, and read blogs and articles 
to stay updated.

By following these steps, you can learn C language quickly, reliably, and with the best results for 
future development in other programming languages. Remember that learning a programming language takes time, 
so be patient and keep practicing.

## Rule the World, but first, complete this function

### Get git

No, seriously, get [git](https://git-scm.com/). Then head over to [Unity](https://github.com/ThrowTheSwitch/Unity) and 
click on the **green** button. Copy the _https_ link, don't worry it's completely free, like with me. Open
Termian on your computer, it might be called Console or Powershell, it does not matter, you will be talking
to the computer using commands, not being source of meta data - you just embark on your journey to become a
**dev**, so act like one and create yourself a folder where your source code will live and then, write in 
terminal `git clone https://github.com/ThrowTheSwitch/Unity`, press `<Enter>`, and that's it. You just 
cloned your first open source project. This one is unit testing framework that will help us get to know 
what's working in our programs and what's not. _Don't Reapeat Yourself_ and write down the exact flow of
the commands and maybe some additional notes what happened, because it's important.

### Unity, unit testing framework

Now we have to compile Unity. Actually we don't. We will just do this by the way... I mean we will eventally
compile the program, as it's not interpreted as for examply your macOS Ruby or Python, but it will be very easy.

```c
#include "path/to/folder/with/unity/src/unity.h" // see? It's just a mean of providing a correct path
// we don't have to link any external library or something, so it is relatively easy for this stage of your
// dev level (I hope you're eager to grow)

// now the first function
void setUp(void)
{
    // your code to setup the unit tests, like initializig connection to database
}

void tearDown(void)
{
    // close the connection to database, by the way - I'm non magically connecting/disconnecting here,
    // it's just my comments
}

// your first test function
void test_function_should_fail(void)
{
    // following red, green, refactor policy ♥️ -> 🐢 -> 🛤
    TEST_FAIL();
}

int main(void)
{
    UNITY_BEGIN();
    //Why should we fail, you ask?
    //First of all it helps to catch false positives,
    //and for the second argument, you will write a better test
    //next time, or prepare/plan you work befer you go...
    RUN_TEST(test_function_should_fail);
    return UNITY_END();
}
```

Now, I have to explain what we're actually doing. We want to know if a particular part of program is doing
what it's suppose to do, so we break the programs into smaller pieces, and then build up from them the
parts that will set to motion all the machinery inside your computer. I have to warn you. If you don't like
this it's fine, but if you want to find a job as a developer, you will be testing your programs all the day
long. If you write for fun, it's just good practice. Just good. What can I say to encourage you to do this?
You get the Unity for free, and are free to choose it.

Let's end the gibberysh talk and get to the point. Compilation. Ha, ha... Now we compile.

### Compile your first unit test

I have `clang` on my computer, you might have something else, so I will stick to the common ground and set on
`gcc` which should be available on most of the platforms.

```bash
gcc -Wall -g name_of_your_source_code_file.c path/to/unity.c -o test-if-fail
./test-if-fail
```

You should be presented with the output:

```text
-----------------------
1 Tests 1 Failures 0 Ignored
FAIL
```

I hope you're not feeling tremendously horrible with yourself right now. You should be proud! Your program
do exactly what you tell it to do, and nothing else.

### Let's spin the roulette around and see if we can... Yes, we can 🎨!

Instead of `TEST_FAIL()`, and yeah I know, I thought it's some kind of `Python` and that it will return false
and I could simply reverse it with `TEST_ASSERT_FALSE()`, but no, it's not like that. It's macro. We'll have
to embark on this journey together to know where it leads us. For now we will just refactor our RED/GREEN
case, assuming we wanted to fail and we had nothing before, to a bigger program. Now you judge me, or the
students. Let's assume there is a gradebook and we wan't to know who pass and what grade we will assign.

For the gradebook, you should be able to at least understand, if not write yourself, one of the first
`katas` from mentioned `Codewars` - Grasshopper - Grade book.

Find an averega of the 3 integer numbers (e.g. grades from the tests) and assign a final grade based on this
conditions:

```
if the average is less than 60, return 'F'
if the average is between 60 and 69, return 'D'
if the average is between 70 and 79, return 'C'
if the average is between 80 and 89, return 'B'
if the average is between 90 and 100, return 'A'
```

And I provide the test cases for you. If you haven't already, please open your text editor, IDE or
take a pen and piece of paper and follow along.

#### Test cases for grade book.

Modify the previous program, test function name to `test_function_should_assignGrades` and change it's
content to:

```c
TEST_ASSERT_EQUAL_INT_MESSAGE('A', get_grade(95, 90, 93), "95, 90, 93 should return 'A'");
TEST_ASSERT_EQUAL_INT_MESSAGE('A', get_grade(92, 93, 94), "92, 93, 94 should return 'A'");
TEST_ASSERT_EQUAL_INT_MESSAGE('A', get_grade(100, 85, 96), "100, 85, 96 should return 'A'");
TEST_ASSERT_EQUAL_INT_MESSAGE('B', get_grade(70, 70, 100), "70, 70, 100 should return 'B'");
TEST_ASSERT_EQUAL_INT_MESSAGE('B', get_grade(82, 85, 87), "82, 85, 87 should return 'B'");
TEST_ASSERT_EQUAL_INT_MESSAGE('B', get_grade(84, 79, 85), "84, 79, 85 should return 'B'");
TEST_ASSERT_EQUAL_INT_MESSAGE('C', get_grade(70, 70, 70), "70, 70, 70 should return 'C'");
TEST_ASSERT_EQUAL_INT_MESSAGE('C', get_grade(60, 82, 76), "60, 82, 76 should return 'C'");
TEST_ASSERT_EQUAL_INT_MESSAGE('C', get_grade(75, 70, 79), "75, 70, 79 should return 'C'");
TEST_ASSERT_EQUAL_INT_MESSAGE('D', get_grade(60, 60, 60), "60, 60, 60 should return 'D'");
TEST_ASSERT_EQUAL_INT_MESSAGE('F', get_grade(30, 30, 30), "30, 30, 30 should return 'F'");
TEST_ASSERT_EQUAL_INT_MESSAGE('F', get_grade(48, 55, 52), "48, 55, 52 should return 'F'");
```

Also, change in the main function, the line `RUN_TEST(test_function_should_assignGrades);`. Now you are ready
to write your first function on your own. You can do it in the same file, and to pass the tests, it's name
should be `get_grade`, or otherwise you will have to change all the invocations to name chosen by you.

### Grade book source code

My solution:

```c
int get_grade(int grade1, int grade2, int grade3)
{
    int average = (grade1 + grade2 + grade3) / 3;
    if (average < 60)
        return 'F';
    else if (average < 70)
        return 'D';
    else if (average < 80)
        return 'C';
    else if (average < 90)
        return 'B';
    else
        return 'A';
}
```

After running this code, or your code, along with the main test function you should get this result:

```text
-----------------------
1 Tests 0 Failures 0 Ignored
OK
```

Congratulation on your first passed test 🚀.

Here is the `Makefile` to cheer you up, with a little explanation:

```Makefile
CC = gcc
CFLAGS = -std=c11 -Wall -Wextra -Werror -I../unity

SRC = grasshoper-gradebook.c
UNITY_SRC = ../unity/unity.c

TARGET = grasshoper-gradebook

.PHONY: all clean

all: $(TARGET)

$(TARGET): $(SRC) $(UNITY_SRC)
	$(CC) $(CFLAGS) $^ -o $@

clean:
	rm -f $(TARGET)
	rm -f *.o
```

Here's an explanation of each part of the Makefile:

* `CC = gcc`: This sets the variable CC to gcc, which specifies the C compiler to use for building the program.

* `CFLAGS = -std=c99 -Wall -Wextra -Werror -I../unity`: This sets the variable CFLAGS to a list of compiler 
flags that will be used when compiling the program. `-std=c99` specifies that the C99 standard should be used, 

* `-Wall -Wextra -Werror` enable warnings and treat them as errors, and `-I../unity` specifies that the 
compiler should look in the `../unity` directory for header files.

* `SRC = grasshoper-gradebook.c`: This sets the variable `SRC` to the name of the C source file for the program.

* `UNITY_SRC = ../unity/unity.c`: This sets the variable `UNITY_SRC` to the name of the Unity source file that 
will be used for testing.

* `TARGET = grasshoper-gradebook`: This sets the variable `TARGET` to the name of the executable file that 
will be created.

* `.PHONY: all clean`: This declares the all and clean targets as phony, meaning that they don't correspond 
to actual files and should always be considered out of date.

* `all: $(TARGET)`: This declares the all target, which depends on the `$(TARGET)` file. When make `all` is run, 
it will build the `$(TARGET)` file.

* `$(TARGET): $(SRC) $(UNITY_SRC)`: This specifies that the `$(TARGET)` file depends on the `$(SRC)` and 

* `$(UNITY_SRC)` files. When make is run and `$(TARGET)` is out of date, it will rebuild the file by 
compiling `$(SRC)` and `$(UNITY_SRC)` together.

* `$(CC) $(CFLAGS) $^ -o $@`: This is the command that is run to build the `$(TARGET)` file. `$(CC)` and 

* `$(CFLAGS)` specify the compiler and its flags, `$^` expands to the list of dependencies (`$(SRC)` and 

* `$(UNITY_SRC)`), and `$@` expands to the target name (`$(TARGET)`).

* `clean: rm -f $(TARGET)`: This declares the clean target, which removes the `$(TARGET)` file when run.

## Dockerfile

Docker is a popular open-source platform for building, shipping, and running distributed applications. 
It allows developers to package applications and their dependencies into a portable container that can
run on any machine, regardless of the underlying operating system and hardware.

Here are a few common use cases for Docker:

1. Application deployment: Docker simplifies the deployment process by allowing developers to package their
applications and their dependencies into a single container. This container can then be easily deployed 
to any environment, whether it's a development machine, staging environment, or production server.

2. Microservices architecture: Docker's lightweight containers make it easier to break down monolithic
applications into smaller, independently deployable microservices. Each microservice can be packaged 
and deployed as a separate container, allowing for greater flexibility and scalability.

3. Continuous integration and deployment (CI/CD): Docker can be used in a CI/CD pipeline to automate 
the build, test, and deployment process. Developers can create a Docker image of their application, 
and then use that image to deploy the application to multiple environments automatically.

4. Development environments: Docker can be used to create consistent development environments across 
multiple machines. Developers can create a Docker image that includes all the tools and dependencies 
they need to develop their applications, and then use that image to spin up development environments 
on any machine.

5. Cloud computing: Docker is widely used in cloud computing environments such as AWS, Google Cloud Platform,
and Microsoft Azure. By using Docker containers, developers can create scalable, fault-tolerant applications
that can run on cloud infrastructure.

Overall, Docker provides a powerful tool for developers and system administrators to manage their
applications and infrastructure, and is widely used in modern software development and deployment practices.

From now on, I'm assuming you're using Linux, Unix or something like that. No, not really. As you've read
you should probably get the impression that I'm going to ask you to install another tool. But that's not
your oridinary LAMP server on your bare metal Windows box. You can have [Docker](https://www.docker.com/) 
([Podman](https://podman.io/) too) on your Windows too. All you need is that `git` for source version control
and OCI containers...

### What is OCI container

OCI (Open Container Initiative) container is a standard for container image format and runtime specification. 
It is a set of open standards and specifications for creating, packaging, and running containerized 
applications.

The OCI was formed by a group of companies and organizations in the container ecosystem to create open 
standards for container technology, and it is now a Linux Foundation project. The OCI container standard 
defines a common specification for the format and runtime of container images, ensuring that they are 
interoperable across different container runtimes.

The OCI image format defines the structure and layout of container images, while the OCI runtime 
specification defines how the container should be run and managed. The OCI standard provides an 
interoperable, vendor-neutral container format that can be used by any container runtime, enabling 
developers to build and distribute containerized applications without worrying about the underlying
infrastructure.

The OCI container standard is widely used by container platforms and orchestrators such as Docker,
Kubernetes, and containerd, which use the standard to ensure that container images and runtimes are
compatible and interoperable. By using the OCI standard, developers can ensure that their containerized
applications can run on any container runtime that supports the standard, providing greater flexibility
and portability.

### What is Fedora

Since my recent switch to dnf-based systems, I have tried CentOS Stream 9, Alma Linux, and Fedora, and this
one, Fedora, will be the one I will use since it's aimed at more day-to-day usage and broader package
coverage because it's base for the Red Hat Enterprise Linux package development management. The first
step is Fedora, then, CentOS Stream and RHEL at last (also Rocky and Alma Linux).

### What is DNF

DNF (Dandified Yum) is a package manager used on some Linux distributions that are based on the Fedora
operating system, such as Fedora itself, CentOS, and Red Hat Enterprise Linux (RHEL). It is the next
generation version of the Yum package manager, which was the default package manager on these distributions
prior to the introduction of DNF.

DNF is designed to provide improved performance and usability compared to Yum, while still maintaining
compatibility with existing Yum repositories and packages. Some of the key features of DNF include:

1. Faster performance: DNF is designed to be faster and more efficient than Yum, with better performance
for tasks such as package installation, updates, and dependency resolution.

2. Improved dependency handling: DNF includes improved dependency handling, with better tracking of
dependencies and conflicts between packages.

3. Modular architecture: DNF has a modular architecture, which makes it easier to extend and customize
for different use cases and environments.

4. Better error handling: DNF includes improved error handling, with more informative error messages
and better error reporting.

5. Support for other package formats: DNF can also work with other package formats besides the RPM
format used on Fedora-based systems, such as the Snappy format used on Ubuntu.

Overall, DNF provides a modern, powerful package management tool for Fedora-based systems, with
improved performance and usability compared to its predecessor, Yum.

### What is Linux

Linux is an open-source operating system kernel created by Linus Torvalds in 1991, and is the basis
for many popular Linux-based operating systems, commonly referred to as "Linux distributions". 
Linux is a Unix-like operating system, which means it shares many similarities with the original
Unix operating system, such as a hierarchical file system, a command-line interface, and a focus
on modular design and composability.

Linux is a popular choice for both personal and enterprise computing, as it is highly customizable,
secure, and can run on a wide range of hardware, from embedded devices and smartphones to servers and
supercomputers. Linux is widely used for web servers, cloud computing, scientific research, and
embedded systems, among other applications.

One of the key strengths of Linux is its open-source nature, which means that the source code is
freely available and can be modified and distributed by anyone. This has led to a vibrant ecosystem
of developers, companies, and communities working together to improve and maintain Linux, resulting
in a highly stable, reliable, and flexible operating system.

Linux is also known for its wide range of available software, including many free and open-source
applications, making it a popular choice for developers and users who value freedom, flexibility,
and community-driven innovation.

### What is GNU/Linux

GNU/Linux is a term used to refer to a complete operating system that is built on top of the Linux
kernel and includes a set of GNU tools and software. The GNU project was started by Richard Stallman
in 1983, with the goal of creating a free and open-source software ecosystem, and has since grown
into a large and influential community of developers, users, and advocates.

The Linux kernel, created by Linus Torvalds in 1991, provides the low-level services and interfaces
that allow the operating system to interact with the hardware of a computer or other device. The GNU
tools and software, which were developed independently of the Linux kernel, provide the higher-level
functionality that is typically associated with an operating system, such as user interfaces, file
systems, utilities, and programming tools.

The combination of the Linux kernel and the GNU software creates a powerful and flexible operating
system that is widely used in both personal and enterprise computing. The open-source nature of GNU/Linux
has led to a vibrant ecosystem of developers, companies, and communities that contribute to its
development, support, and distribution, resulting in a highly customizable, reliable, and secure
operating system.

GNU/Linux is used in a wide range of applications, from personal desktops and laptops to servers,
mobile devices, and embedded systems. It is known for its stability, security, and flexibility,
as well as for the wide range of available software and the passionate community of users and
developers who support it.

### Sum up the briefing

I hope that you now see, that what we'll be using is really useful and combinig all the skills
you will really distinguish yourself in the community so you might do your work faster, organize
better and deliver in full, not in parts. Now might be a good time to get you up and going with the
last tool I have introduced to you, `git`. It's ment to help collaborate and share source code, but it's
usege surpass that, and now even books are written using git, just like this one. What it do?
It keeps track of your changes to files, it is able to send data to git servers, such as [GitHub](https://github.com) or [GitLab](https://gitlab.com/kalilinux). Unfortunately, or not, it doesn't do this automatically.

[![asciicast](https://asciinema.org/a/562489.png)](https://asciinema.org/a/562489?autoplay=1&speed=2&theme=solarized-dark)

1. Initialize new .git repository (note that you do this only once, and some tools do this for you)

    - `git init`
    - you might have to set your username and email
        * git config --global user.name "FIRST_NAME LAST_NAME"
        * git config --global user.email "MY_NAME@example.com"

2. Stage your files for commit
    
    - `git add path/to/your/file another/file .gitignore` or
    - `git add *` - this will add all files except those in `.gitignore` but not always all, so check with:
    - `git status`

3. Commit your change

    - `git commit -m "Initial commit"`, where `-m` stands for message

4. Add remote

    4.1. create git repository on GitHub, it may be private (for free)
    4.2. follow the instructions on screen, or click the green button and copy the https link
    4.3. `git add remote origin https://your.link.git`, origin stands for name of the remote

5. Pull code from GitHub

    5.1. `git status`, and note the branch you're currently on, or:
    5.2. `git branch -l`, and check if the desired name is free
    5.3. `git pull origin main --rebase`, this is usually the main or master branch,
        but you might want to use another local branch, and `--rebase` option let's you
        choose which changes you wish to preserve from upstream or local branch
    
    - you might need to merge branches, so do `git checkout main` to change to main branch,
        and then, `git merge upstream`

6. Push code to GitHub

    - `git push origin main --set-upstream`, this will upload the code to GitHub and let you
        use just `git push` to send source code to GitHub.

### Repeat, what is git, elaborative description

Git is a distributed version control system that allows developers to manage and track changes to code
and other files over time. It was created by Linus Torvalds in 2005 to manage the development of the
Linux kernel, and has since become one of the most widely used version control systems in the software
development industry.

Git enables multiple developers to collaborate on the same project by allowing them to create their own
local copies (or "clones") of the code repository. Each developer can then make changes to their local 
copy and push those changes back to the central repository. Git uses a system of branching and merging 
to manage changes, allowing developers to work on different features or bug fixes in isolation and 
then merge their changes back into the main codebase when they are ready.

Some of the key features of Git include:

- Distributed architecture: Git stores a complete copy of the code repository on each developer's machine,
allowing them to work offline and reducing the risk of data loss or corruption.
- Branching and merging: Git allows developers to create multiple "branches" of the codebase to work
on separate features or bug fixes in isolation, and then merge those changes back into the main codebase
when they are ready.
- Version history: Git tracks every change made to the codebase, allowing developers to view a complete
history of all changes and revert to previous versions if necessary.
- Collaboration: Git enables multiple developers to work on the same project concurrently, sharing their
changes and resolving conflicts as needed.

Overall, Git is a powerful tool that enables developers to work more efficiently and collaboratively, 
while also providing a robust and reliable system for managing and tracking changes to code over time.

### When you're done

After the initial setup of `Podman & git` you can spin up this simple container. It consist of `Fedora`, 
GNU/Linux, `Development Tools` - our main focus here is `make` - for _Makefiles_ and `gcc` for __C__, 
and `Ruby` - dynamic programing language. Why another language? I want to show how to call C code from
other programming languages, and it's much more easier, and sane, to create a website using Ruby than using C.
We will also explore using JSON in C and in Ruby. We will create a KISS website containing data
download using `libcurl from ifconfig.me service and Apple Music API. Everything will be executed inside
a container with much less configuration needed to be performed and much safer way to publish your code.
We won't forget to make few unit tests, and to be honest, I'm learning this Test Driven Development with you.

1. Create file named Dockerfile in a folder that is available to share in Docker or Podman. There you
will store the rest of this new project.

```Dockerfile
FROM fedora:latest

WORKDIR /app

RUN dnf groupinstall -y 'Development Tools'
RUN dnf install -y ruby && gem install bundler
RUN bundle install

EXPOSE 9292 # not neccesairly needed, good practice

ENTRYPOINT [ "bundle exec rerun -- bundle exec rackup config.ru" ]
```

When you save this file in your system, then you can build it with `docker build --tag c-dev .` from the
same directory of the `Dockerfile`. This will build for you a Docker image with `Fedora` system and
development tools installed. To run this you use `docker run -it --name dev -v $(pwd):/app -p 9292:9292 c-dev`.
This command will create a dev container (change name how you like it), from the
build image. I have deliberatedly omitted --rm option, which would remove our container after stopping it.
If you want to remove this container, use this commad: `docker rm --force dev`.

Let's not jump quickly into conclusions, that this container will actually run. It wouldn't. 💄 RED -> 🐢 GREEN
-> 💫 REFACTOR. Remember? I have story to be laid out, and you have a lesson to learn. Bear with me, a little bit longer.

For the excuses I have another container that you can run, and it will be cURL image, the program that we will use,
thus we stay in the scope of this excercise. To run cURL container you will simply use this command (you have to
be connected to the Internet), so it before with `docker pull rancher/curl:latest`, this one will be very fast
because the image is of 5.33 MB. Now that you have the cURL program from image, you can run it:

```bash
docker run --rm -it rancher/curl ifconfig.me
```

[![asciicast](https://asciinema.org/a/562493.svg)](https://asciinema.org/a/562493?autoplay=1&theme=solarized-dark)

What you should expect? You will get the text response with your current IP number terminated by `%`.

## Shared and dynamic libraries

Dynamic and shared libraries are both types of libraries that contain code and data that can be shared among
different programs. However, there are some key differences between these two types of libraries:

1. Loading time: Dynamic libraries are loaded into memory at runtime when a program starts, whereas shared
libraries are loaded at link time when a program is built. This means that dynamic libraries can be loaded
and unloaded as needed, while shared libraries are loaded into memory for the entire lifetime of the program.

2. Memory usage: Because dynamic libraries are loaded into memory at runtime, they can be loaded and unloaded
as needed, which can help conserve memory usage. Shared libraries, on the other hand, are loaded into memory
for the entire lifetime of the program, which can lead to higher memory usage.

3. Linking: Dynamic libraries are linked dynamically at runtime, which means that the library can be updated
without recompiling the entire program. Shared libraries, on the other hand, are linked statically at link
time, which means that any changes to the library require recompiling the entire program.

4. Platform independence: Dynamic libraries are platform-independent, which means that a single dynamic
library can be used across multiple platforms without recompiling the library. Shared libraries, on the
other hand, are platform-specific, which means that a separate shared library needs to be compiled for each
platform.

In summary, dynamic libraries are loaded at runtime, can be loaded and unloaded as needed, and are
platform-independent, while shared libraries are loaded at link time, are loaded into memory for the
entire lifetime of the program, and are platform-specific.

### Compile shared library

To compile a shared library from a C file, you can use the "-shared" flag with the GCC 
(GNU Compiler Collection) command. Here's an example of how to do this:

1. Write your C code in a file named "my_library.c". For example:

```c
int add_numbers(int x, int y) {
    return x + y;
}
```

2. Compile the C code as a shared library using the GCC command with the "-shared" flag:

```bash
gcc -shared -o libmy_library.so my_library.c
```

This will create a shared library file named "libmy_library.so" in the current directory.

The "-shared" flag tells GCC to produce a shared library instead of an executable. The "-o" 
flag specifies the output file name.

Note that the file extension for shared libraries can vary depending on the platform. On Linux 
and other Unix-like systems, the file extension is typically ".so". On macOS, the file extension 
is typically ".dylib". On Windows, the file extension is typically ".dll".

Once you have compiled the shared library, you can link it with other programs that use the library.

### Compile dynamic library

Dynamic libraries, also known as shared object files (or shared libraries on Windows), are libraries
that are loaded into memory at runtime when a program starts or when the library is first used. Dynamic
libraries can contain code and data that can be shared among different programs, which can help reduce
the size of executables and reduce memory usage.

1. Write your C code in a file named "my_library.c". For example:

```c
int add_numbers(int x, int y) {
    return x + y;
}
```

2. Compile the C code as a dynamic library using the GCC command with the "-fPIC" (position-independent code)
and "-shared" flags:

```bash
gcc -fPIC -shared -o libmy_library.so my_library.c
```

This will create a dynamic library file named "libmy_library.so" in the current directory.

The "-fPIC" flag tells GCC to generate position-independent code, which is required for building shared
libraries. The "-shared" flag tells GCC to produce a dynamic library instead of an executable. The "-o"
flag specifies the output file name.

Note that the file extension for dynamic libraries can vary depending on the platform. On Linux and other
Unix-like systems, the file extension is typically ".so". On macOS, the file extension is typically ".dylib".
On Windows, the file extension is typically ".dll".

Once you have compiled the dynamic library, you can load it into a program using a dynamic linker, such as 
the "dlopen" function in C or the equivalent functions in other programming languages. The dynamic linker 
will load the library into memory at runtime and resolve any symbols that the program needs from the library. 
This allows programs to share code and data with dynamic libraries, which can help reduce memory usage and 
make it easier to update and maintain the shared code.

## Back to Dockerfile

This `Dockerfile` will eventually run our application so watch it closely as it changes.

### Minimal Dockerfile

Now please get back to the Dockerfile we created and change so it look like the file below and run `docker build --tag c-dev .`. 
This will create a c-dev image that you can run with `docker run --rm -it c-dev`. If it fails, you might need to run 
again `docker build --no-chache -t c-dev`

```Dockerfile
FROM fedora:latest

WORKDIR /app

RUN dnf groupinstall -y 'Development Tools'
RUN dnf install -y ruby libcurl-devel json-c-devel && gem install bundler

ENTRYPOINT [ "make", "test" ]
```
Be aware that I have added `libcurl` and `json-c` _*-devel_ libraries that we will use

This will inevitebly fail. But don't worry, we have just satisfied the red rule 💄. Now it's time to create a
Makefile for the tests we wil have.  You might start like this `touch Makefile` or more verbose `nvim Makefile`.
You can also have Visual Studio Code installed in your `PATH` variable (look into command pallete and type `code`).
I do not recommend a bigger IDE, like Visual Studio or Jet Brains for this because they are simply too big to fit
into 128 GB SSD drive. Beside that, it's just text. Maybe if I find courage, I might touch on graphic and UI design,
but for now we're just talking with machine (ChatGPT, remember?)

### Makefile, the task runner of the Empire

We use `Makefile` to make our job easier. We "automate", or divide building tasks of the app to smaller, easier to
manage pieces.

```Makefile
CC = cc
CFLAGS = -std=c11 -Wall -Wextra -Werror 
CURLCFLAGS = `curl-config --cflags`
CURLFLAGS = `curl-config --libs`
JSONCFLAGS = `pkg-config --cflags json-c`
JSONFLAGS = `pkg-config --libs json-c`

SRC = curl.c
CURL = curl
UNITY_SRC = ../unity/unity.c

TEST = test
DEBUG = debug
.PHONY: all clean test

# create curl library
all: $(SRC)
	$(CC) $(CFLAGS) $(CURLCFLAGS) $(JSONCFLAGS) -fPIC -shared $^ -o $(CURL) $(CURLFLAGS) $(JSONFLAGS)

# create test executable in debug mode
$(DEBUG): $(TEST).c $(UNITY_SRC)
	$(CC) $(CFLAGS) -I../unity $(CURLCFLAGS) $(JSONCFLAGS) -g $^ -o $@ $(CURLFLAGS) $(JSONFLAGS)

# run test executable
$(TEST): $(TEST).c $(UNITY_SRC)
	$(CC) $(CFLAGS) -I../unity $(CURLCFLAGS) $(JSONCFLAGS) $^ -o $@ $(CURLFLAGS) $(JSONFLAGS)
	./$(TEST)

# clean up
clean:
	rm -f *.o
	rm -f $(TEST)
	rm -rf *.dSYM
	rm -f $(DEBUG)
	rm -f $(CURL)
```

This is a lot of code, but it is intended to help you in managing all the compilation and linking process
that otherwise wouldn't be such simple task. Here we have, starting from top `CC` which sets the used compiler
to available alias of gcc, cc what was the standard command for `C compiler`. Then I have decided to add
compiler flags that defines the C standard to be c11, and to treat warnings as errors, so those who will go then
straight to `Rust` programming language might feel already at home with this, little, extra hand holding.
After that comes library specific code which I save to respective variables so they might be reused by tasks, after
all `Make` is a task runner like `Grunt` or `Gulp` (which you might encounter in `Java Script` world).

Next come variables holding main part of the C library we'll dissect, curl target, curl.c source code file and
path to Unity testing framework source code we have left from previous - grades - example. We also use `.PHONY`
target to specify that even if there is a file with the same name as the target itself, the task must be run again.

Now the time has come for tasks aka targets itself. The first three are ment to compile different parts of the library.
The `all` target compiles only the `curl` library. `DEBUG` target creates debugging ready version of `TEST` target,
so you might dive deep into troubleshooting. The main difference here is the usage of `-g` flag, that saves
debugging symbols into output file. The `TEST` target produces a test executable and runs it, and it's much faster than
testing in Ruby, what you will see and compare yourself.

The last target: `clean` is intended for maintenance purpose. Run it if you want to delete all the executables and libraries.

For the future reference, you might want to remember that using `pkg-config` with `--cflags` and `--libs` help in resolving
dependencies you have to use in order to correctly compile your programs and libraries.

### The test.c of our curl library

After creating `Makefile` and using it's task `make test` as an `ENTRYPOINT` for `Dockerfile` we have almost set the
thing in motion, but we lack C code right now. First we will implement unit tests. We're building cURL a-like
library that can connect to external resources and fetch data from them using simple `GET` request. So we need
to know the data and test against it. For example, we already tried cURL on `ifconfig.me` endpoint. It simply return
our IP address, but, the IP address changes from user to user of the library. We can't hardcode just our IP. In funct
we can't hardcode any IP, it would defeat the purpose of the unit test, and the library itself, to be reusable.
Think of it like a virus. It want's to spread, in open source world you might want to share your code with the others
and even if you're coding for yourself, your IP might change, what would happen then? Write tests for edge cases, like
if the format is proper, if it contains desired parts, but not the exact match. Don't test for 1, test for a number.

```c
#include "../unity/unity.h"
#include "curl.c"
#include <ctype.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

void setUp(void) {}

void tearDown(void) {}

void curl_should_returnUserIp(void) {
  // invoke curl() function; it should return a string
  // store result in a variable
  // check if the variable is not NULL
  // check if the variable is a valid ip address
  // check if the variable has 4 parts
  // check if the variable has 3 digits in each part
  // check if the variable has a dot in each part
  char *result = curl("ifconfig.me");
  TEST_ASSERT_NOT_NULL_MESSAGE(result, "ip should not be null\n");
  int i = 0;
  // check if there is a dot in each part
  char *token = strtok(result, ".");
  while (token != NULL) {
    // cast string to int
    int part = atoi(token);
    int digits[3];
    // trick to get digits of a number
    digits[0] = part / 100;
    digits[1] = (part / 10) % 10;
    digits[2] = part % 10;
    for (int i = 0; i < 3; i++) {
      // check if digit is a number, append '0' to get ascii value
      TEST_ASSERT_TRUE_MESSAGE(isdigit(digits[i] + '0'),
                               "ip should be a number\n");
    }
    // check if there is a dot in each part
    token = strtok(NULL, ".");
    // keep track of how many parts there are
    i++;
  }
  TEST_ASSERT_EQUAL_INT_MESSAGE(4, i, "ip should have 4 parts\n");
  // should have null at the end
  TEST_ASSERT_NOT_NULL_MESSAGE(strchr(result, '\0'),
                               "Ip is not null-terminated");
}

void curl_should_returnSetAndSettingsVol9(void) {
  char *result = curl("https://itunes.apple.com/lookup?id=1658237994");
  TEST_ASSERT_NOT_NULL_MESSAGE(result, "result should not be null\n");
  TEST_ASSERT_NOT_NULL_MESSAGE(strchr(result, '\0'),
                               "result is not null-terminated");
  // check if there is a string "Set and Settings, Vol. 9"
  // check if there is a string "Neosb"
  TEST_ASSERT_NOT_NULL_MESSAGE(
      strstr(result, "Set and Settings, Vol. 9"),
      "result should contain 'Set and Settings, Vol. 9'\n");
  TEST_ASSERT_NOT_NULL_MESSAGE(strstr(result, "Neosb"),
                               "result should contain 'Neosb'\n");
  // check if there is a string "1658237994"
  TEST_ASSERT_NOT_NULL_MESSAGE(strstr(result, "1658237994"),
                               "result should contain '1658237994'\n");
  // check if last character is a null terminator
  TEST_ASSERT_NOT_NULL_MESSAGE(strchr(result, '\0'),
                               "result is not null-terminated");
  TEST_ASSERT_EQUAL_CHAR_MESSAGE('\n', result[strlen(result) - 1],
                                 "result should end with a new line\n");
  // check if second last character is a new line

  TEST_ASSERT_EQUAL_CHAR_MESSAGE('\n', result[strlen(result) - 2],
                                 "result should end with a new line\n");
  // check if third last character is a new line
  TEST_ASSERT_EQUAL_CHAR_MESSAGE('\n', result[strlen(result) - 3],
                                 "result should end with a new line\n");
  // check if fourth last character is a curly bracket
  TEST_ASSERT_EQUAL_CHAR_MESSAGE('}', result[strlen(result) - 4],
                                 "result should end with a curly bracket\n");
}

int main(void) {
  UNITY_BEGIN();
  RUN_TEST(curl_should_returnUserIp);
  RUN_TEST(curl_should_returnSetAndSettingsVol9);
  return UNITY_END();
}
```

Here I have included two sources of information we test against: IP number obtained from (**thank you**) `ifconfig.me`,
and a second one, JSON object from Apple Music API. Both are free to use websites that provide machine readable
messages that after some tuning can turn into human readable data. And as for every rule, there are exceptions.
First of all. If you are sure that the message will never change, and you want to test the functionality of the
service. I have included in my `test.c` code three examples. I know that my song is named Set and Settings, Vol. 9,
but I also know that there are many similar song titles in my discography, so I want to check if the result of the
query is the exact match. Then I will know that my code works as intended. Probably I should also check if the result
of the search in Apple Music API is a proper JSON object, but that I leave to you for an excercise instead of another
round with kata from Codewars. They are good to train, but you probably won't write that kind of code never in your lifetime
as a proffesional Hacker, you would just copy and paste the result of a pleasent conversation with _ChatGPT_, or 
_Google_ search. To solve this puzzle, you can use `json-c` library that we have installed in Dockerfile. And yes,
you can develop in container. If you want to jump right now into development in containers, you might check this
article about [Visual Studio Code - devcontainers](https://code.visualstudio.com/docs/devcontainers/containers).

I hope you're ready for another round of dissecting source code, this time in `C`.

First we import every library and header file we will use in our test cases. Then we declare `setUp` and `tearDown`
functions, so the Unity framework is happy. This time there is nothing in them, but you will put there pieces
of code that must be run _before_ and _after_ every `RUN_TEST(test)` in main function. We can start from
putting names of our test functions, and yes there might be the other way to do this, mainly splitting code into
even smaller parts. That would greatly enhance the readability of a test runner output, but it has no difference
on running tests itself other than if your code depends on external resources, for example database, or API calls -
they will be repeated every time you invoke a test, so plan responsibly and accordingly to your Internet bandwith.

#### curl_should_returnUserIp

This function tests if the IP has proper format, if the message is not null, that it contains four crucial parts of
IPv4 IP address and that in response there are only digits and dots. As a side note, if you modify user agent of
curl invokation (you might do this in curl.c about which we will talk next), you can get HTML response which you
can then embed on website we will create in some time (this should be another kata for you).

How do we test? Thanks to Unity framework verbosity we know what types are used in test cases, and if one fails,
the function immedietly returns so you can investigate on your own. But remember that you should, but are not
constrained by anyone to fail 💄 the test first, and only then gradually improve. Since, we're in statically
typed world yet, we can't just run the tests, because of missing dependencies, so I think it's fair enough.

##### The tricks used.

- strtok(string, character) - split the string on first occurance of the desired character
- atoi(string) - tries to return int from string
- digits[0] = part / 100; digits[1] = (part / 10) % 10; digits[2] = part % 10; - get one digit at the time and save
to array
- isdigit(number) - return true if a digit is an actual number (one at the time)

#### curl_should_returnSetAndSettingsVol9

This function is in part exception to reusability rule, as it checks for hard coded values, but I know what this
values would be and I want to be sure that the returned response is exactly this nothing else.

Here I check for title of a song, it's id and and artist name. Also some basic string and null tests. Nothing
to worry about, just good to know. Like I mentioned, you should try to check if the output is valid JSON object,
and maybe add some test if the response contains particular fieldnames, becuase you might want to check for
other artist and accidently omit or add requested entities. Here is the link to [Apple Music API](https://performance-partners.apple.com/search-api).

##### Tricks used

- limit response to one song, and check for it's correctness

### curl library itself

Although there is already a tool named cURL, and it is very useful, here we use subset of it's inner engine libcurl
to create our own `GET` request to external resources. You can try this at home.

```c
#include <curl/curl.h>
#include <json-c/json.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

struct memory {
  char *response;
  size_t size;
};

static size_t write_data(void *data, size_t size, size_t nmemb, void *userp) {
  size_t realsize = size * nmemb;
  struct memory *mem = (struct memory *)userp;

  char *ptr = realloc(mem->response, mem->size + realsize + 1);
  if (ptr == NULL)
    return 0; // out of memory! 

  mem->response = ptr;
  memcpy(&(mem->response[mem->size]), data, realsize);
  mem->size += realsize;
  mem->response[mem->size] = 0;

  return realsize;
}

char *curl(char *url) {
    // initialize curl with ssl
  curl_global_init(CURL_GLOBAL_SSL);
  CURL *curl;
  CURLcode res;

  struct memory chunk;
  chunk.response = malloc(1); // will be grown as needed by the realloc above
  chunk.size = 0;             // no data at this point
  // init the curl session 
  curl = curl_easy_init();
  if (curl) {
    struct curl_slist *headers = NULL;
    // set the content type to json
    headers = curl_slist_append(headers, "Content-Type: application/json");
    curl_easy_setopt(curl, CURLOPT_HTTPHEADER, headers);
    // specify URL to get  
    curl_easy_setopt(curl, CURLOPT_URL, url);
    // set the ssl options
    curl_easy_setopt(curl, CURLOPT_SSL_VERIFYPEER, 1L);
    curl_easy_setopt(curl, CURLOPT_SSL_VERIFYHOST, 2L);
    // send all data to this function   
    curl_easy_setopt(curl, CURLOPT_WRITEFUNCTION, write_data);
    // we pass our 'chunk' struct to the callback function  
    curl_easy_setopt(curl, CURLOPT_WRITEDATA, (void *)&chunk);
    // get it!  
    res = curl_easy_perform(curl);
    // check for errors  
    if (res != CURLE_OK) {
      fprintf(stderr, "curl_easy_perform() failed: %s",
              curl_easy_strerror(res));
    }
    char *response = malloc(chunk.size);
    if (response == NULL) {
      fprintf(stderr, "malloc() failed: %s", curl_easy_strerror(res));
    }
    // if first char is not '{' or '[' then it is not a json
    // so we return the whole response
    if (chunk.response[0] != '{' && chunk.response[0] != '[') {
      // return not JSON object
      curl_easy_cleanup(curl);
      // we are done with libcurl, so clean it up  
      curl_global_cleanup();
      return chunk.response;
    } else {
      // encode the response to json
      // and return it
      // this is to avoid the problem of the json-c library
      // that can't parse the response if it is not a json
      // but it is a json
      // so we encode it to json and then decode it
      // and then return it
      // this is a workaround
      // and it is not a good solution
      // but it works
      // and it is the only solution that i found
      // so i will use it
      // and i will not change it
      // because it works
      // and i don't want to change it
      // because it works
      json_object *jobj = json_object_new_string(chunk.response);
      response = (char *)json_object_to_json_string(jobj);
      // cleanup curl stuff  
      curl_easy_cleanup(curl);
      // we are done with libcurl, so clean it up  
      curl_global_cleanup();
      return response;
    }
    // empty, should never run
    free(chunk.response);
    // cleanup curl stuff  
    curl_easy_cleanup(curl);
    // we are done with libcurl, so clean it up  
    curl_global_cleanup();
    return response;
  }
  // error initializing curl, return defaults
  // cleanup curl stuff  
  curl_easy_cleanup(curl);
  // we are done with libcurl, so clean it up  
  curl_global_cleanup();
  return chunk.response;
}
```

Here we go! We have here a complete source code for example usage of libcurl library in so called wrapper around it
, the function takes a single argument url, which is a pointer to a character array or C-style string. The function 
itself returns a pointer to a character array or C-style string. It is based of an example from cURL library webpage
with addition of SSL and JSON object check, cast and downcast. So now you should know how to solve the previous puzzle
on how to check if a string is a valid JSON object. We set headers, to accept json response, but if the response is not
JSON object, it's not the end of the world, our library wrapper will just return that response, so you might experiment
here with many other use cases for cURL. The only puzzle that isn't solved is [user agent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent) which you can set to something more real, than nothing to get other results from `ifconfig.me`,
and many other websites. In fact APIs are design to be user agent agnostic, so in most cases you will get the same result,
but you can request a website to get different HTML when you use iOS, or Android user agent, or some legacy browser like
Internet Explorer.

The only mysterious part of curl function for you as far as you read and learn on your own may be CURLOPT_WRITEFUNCTION and
CURLOPT_WRITEDATA where the write_data writes data as it comes to chunk so it can be returned as full response.

### make test

Right now you can run the Dockerfile. Still nothing? Don't worry... We have two options. We can share our "live" folder in
the container, or better, copy the source code to container so we don't loose data accidently. I will show you both ways.

```bash
docker run --name dev -v /absolute/path/to/source/code:/app -it c-dev
```

To copy source code into container, we have to change the Dockerfile

```Dockerfile
FROM fedora:latest

WORKDIR /app

RUN dnf groupinstall -y 'Development Tools'
RUN dnf install -y ruby libcurl-devel json-c-devel && gem install bundler

RUN git clone https://github.com/ThrowTheSwitch/Unity.git
COPY . /app
RUN sed -i 's/..\/unity\//Unity\/src\//' test.c && sed -i 's/-I..\/unity/-IUnity\/src/' Makefile && \
    sed -i 's/..\/unity\//Unity\/src\//' Makefile

ENTRYPOINT [ "make", "test" ]
```

Now that you have proper Dockerfile, place yourself in curl.c, and test.c source code directory and then you can rebuild it:

```bash
docker build --tag c-dev .
```

After this little treatment to Dockerfile and rebuild of image, you can run container:

```bash
docker run --rm -it c-dev`
```

Here you go 🍀! Now we're in green state.

## RuboCop and ClangFormat, the police of the source code

- [RuboCop](https://rubocop.org/) is a tool that beautifies your code written in Ruby. 
- [ClangFormat](https://clang.llvm.org/docs/ClangFormat.html) is a tool that prettifies your C, C++, Java,
Java Script, JSON, Objective-C, Protobuf and C# code.

Use this tools to make your code more align with the industry standards. Make it clean and shiny.

## Ruby and Sinatra

You have the data, now what? Let's display it on the website.

Create a `Gemfile` with this content:

```ruby
source 'https://rubygems.org'
gem 'sinatra', :github => 'sinatra/sinatra'
gem 'puma'
gem 'rack'
gem 'ffi'

# other dependencies
gem 'erb'
group :test do
  gem 'rack-test'
  gem 'rspec'
end

group :development, :test do
  gem "rerun"
end
```

We define here what will be installed when we run `bundle install` command. Let's change the Dockerfile too and
give it `/bin/bash` as the `ENTRYPOINT`, this will let us fiddle with the system while being able to run make and
in near future `bundle exec` commands. Do you know that you can connect to already running container? No? Well now you do.
It's just a matter of `docker exec` command. I think, that the best workflow from now until we have ready web app would be
to attach live folder into container. Comment out the `#RUN git clone`, `#COPY . /app`, subsequent `#RUN` and a line below 
`# ` and rebuild the container - `docker build -t c-dev .` After this you can attach current folder and run the container
with command like this (mind that we're publishing port 9292 from container to port 9292 on the host machine, what is
reflected in the command in the opposite order):

```bash
docker run --rm -it -v $(pwd):/app -p 9292:9292 c-dev
```

You might run into issues with permissions to read and write to folder, so dig into the settings of Docker Desktop app,
there is an option that enables sharing chosen directories.

On windows you might need to change `$(pwd)` to `${pwd}`.

After the initial run you might look around the system if you wish, but let's head now over to [RubyGems](https://rubygems.org)
where modules, called `gems` are shared between users. We will take a look at each of the entry in `Gemfile`.

Meanwhile, first thing we do is add `spec/examples.txt` to `.gitgnore`. I hope you're already using `git`, and .`gitignore`
simply tells `git` which files to ignore from source control.

Open [RubyGems](https://rubygems.org) in your web browser and take a look around. You already heard about `RuboCop`, try to
search for something that is in the interest for you. I will just itreate over `Gemfile` now.

### Gemfile

In the order of appearence:

- [Sinatra](https://sinatrarb.com/) - Sinatra is a DSL for quickly creating web applications in Ruby with minimal effort. If you
search for Sinatra on RubyGems you might notice, that there is plenty of gems that help Sinatra to be Sinatra. We will explore
this multitude of choices.
- [Puma](https://puma.io/) - Puma is a simple, fast, threaded, and highly parallel HTTP 1.1 server for Ruby/Rack applications. 
Puma is intended for use in both development and production environments. It's great for highly parallel Ruby implementations 
such as Rubinius and JRuby as well as as providing process worker support to support CRuby well.
- [Rack](https://github.com/rack/rack) - Rack provides a minimal, modular and adaptable interface for developing web applications
in Ruby. By wrapping HTTP requests and responses in the simplest way possible, it unifies and distills the API for web servers,
web frameworks, and software in between (the so-called middleware) into a single method call.
- [FFI](https://github.com/ffi/ffi/wiki) - Ruby FFI library. FFI stands for Foreign Function Interface.
- [erb](https://github.com/ruby/erb) - An easy to use but powerful templating system for Ruby.
- [rack-test](https://github.com/rack/rack-test) - Rack::Test is a small, simple testing API for Rack apps. It can be used
on its own or as a reusable starting point for Web frameworks and testing libraries to build on.
- [rspec](https://github.com/rspec) - BDD for Ruby
- [rerun](https://github.com/alexch/rerun/) - Restarts your app when a file changes. A no-frills, command-line alternative 
to Guard, Shotgun, Autotest, etc.

This are the dependencies for my web frontend to, let's be true, simple data. Maybe that's an overkill, but you will
learn a lot. Me too 🚀...

Now that we've talked about what is in there, run your image without `--rm` option and with `--name app` like so:

```bash
docker run -it --name app -v $(pwd):/app -p 9292 c-dev
```

This would tremendously make things simpler, you can now preserve state of container, because it's not removed after stopping,
and a name is a convenience label to access it.

### Bundle install

First of all, we need to add `ruby-devel` to list of installed packages on Fedora, so the Dockerfile should now look like this:

```Dockerfile
FROM fedora:latest

WORKDIR /app

RUN dnf groupinstall -y 'Development Tools'
RUN dnf install -y ruby ruby-devel libcurl-devel json-c-devel && gem install bundler

#RUN git clone https://github.com/ThrowTheSwitch/Unity.git
#COPY . /app
#RUN sed -i 's/..\/unity\//Unity\/src\//' test.c && sed -i 's/-I..\/unity/-IUnity\/src/' Makefile && \
#    sed -i 's/..\/unity\//Unity\/src\//' Makefile
ENTRYPOINT [ "/bin/bash" ]
```

Please start the container with `docker run -it --name app -v $(pwd):/app -p 9292 c-dev` command, and run `bundle install`
inside it. You will see how gems are consecutively installed, wait until command ends. After adding new gem to Gemfile 
you would have to run `bundle install` again, but for now we're done here.

### Configuration

Do you want to have a website? Maybe you want to see how I code a website? So we're going on with this example app that will
show us the results of our `curl()` function invocations in `Ruby` and `Sinatra`. Create two files, one `config.ru` and second
`config/environment.rb`.

#### config.ru

Place this inside:

```ruby
# frozen_string_literal: true

require './config/environment'
run Rack::URLMap.new('/' => Server)
```

and...

#### config/environment.rb

In this file:

```
# frozen_string_literal: true

require 'rubygems'
require 'bundler'
Bundler.require(:default)
Bundler.require(Sinatra::Application.environment)

require './app/server'
require './app/server'
```

In summary this files enables `rackup` support for `Sinatra` app, that will run in container. It's just setup files...
If you want to be more picky, dig up the documentation on Rack and it's support for Sinatra, but for now, I leave it
here as is. I hoope you will handle me and read this book as we go along, so we can create more sophisticated user interfaces
and more complicated libraries for, especially, my use case **api hacking**. I want to do this in future, but for now,
I have to refresh and broaden my basics knowledge, and writing this book helps me in the learning process and it should do
good job at giving you a primer on programming and development process.


### Rspec

If you want to, stick with me, come on and initialize your rspec testing environment with this command:

```bash
bundle exec rspec --init
```

Now make your `spec/spec_helper.rb` look like this (it's basically the same, with addition of top lines):

```ruby
# frozen_string_literal: true

ENV['RACK_ENV'] = 'test'
require './config/environment'
# This file was generated by the `rspec --init` command. Conventionally, all
# specs live under a `spec` directory, which RSpec adds to the `$LOAD_PATH`.
# The generated `.rspec` file contains `--require spec_helper` which will cause
# this file to always be loaded, without a need to explicitly require it in any
# files.
#
# Given that it is always loaded, you are encouraged to keep this file as
# light-weight as possible. Requiring heavyweight dependencies from this file
# will add to the boot time of your test suite on EVERY test run, even for an
# individual file that may not need all of that loaded. Instead, consider making
# a separate helper file that requires the additional dependencies and performs
# the additional setup, and require it from the spec files that actually need
# it.
#
# See https://rubydoc.info/gems/rspec-core/RSpec/Core/Configuration
RSpec.configure do |config|
  config.include Rack::Test::Methods
  # rspec-expectations config goes here. You can use an alternate
  # assertion/expectation library such as wrong or the stdlib/minitest
  # assertions if you prefer.
  config.expect_with :rspec do |expectations|
    # This option will default to `true` in RSpec 4. It makes the `description`
    # and `failure_message` of custom matchers include text for helper methods
    # defined using `chain`, e.g.:
    #     be_bigger_than(2).and_smaller_than(4).description
    #     # => "be bigger than 2 and smaller than 4"
    # ...rather than:
    #     # => "be bigger than 2"
    expectations.include_chain_clauses_in_custom_matcher_descriptions = true
  end

  # rspec-mocks config goes here. You can use an alternate test double
  # library (such as bogus or mocha) by changing the `mock_with` option here.
  config.mock_with :rspec do |mocks|
    # Prevents you from mocking or stubbing a method that does not exist on
    # a real object. This is generally recommended, and will default to
    # `true` in RSpec 4.
    mocks.verify_partial_doubles = true
  end

  # This option will default to `:apply_to_host_groups` in RSpec 4 (and will
  # have no way to turn it off -- the option exists only for backwards
  # compatibility in RSpec 3). It causes shared context metadata to be
  # inherited by the metadata hash of host groups and examples, rather than
  # triggering implicit auto-inclusion in groups with matching metadata.
  config.shared_context_metadata_behavior = :apply_to_host_groups

  # The settings below are suggested to provide a good initial experience
  # with RSpec, but feel free to customize to your heart's content.

  # This allows you to limit a spec run to individual examples or groups
  # you care about by tagging them with `:focus` metadata. When nothing
  # is tagged with `:focus`, all examples get run. RSpec also provides
  # aliases for `it`, `describe`, and `context` that include `:focus`
  # metadata: `fit`, `fdescribe` and `fcontext`, respectively.
  config.filter_run_when_matching :focus

  # Allows RSpec to persist some state between runs in order to support
  # the `--only-failures` and `--next-failure` CLI options. We recommend
  # you configure your source control system to ignore this file.
  config.example_status_persistence_file_path = 'spec/examples.txt'

  # Limits the available syntax to the non-monkey patched syntax that is
  # recommended. For more details, see:
  # https://relishapp.com/rspec/rspec-core/docs/configuration/zero-monkey-patching-mode
  config.disable_monkey_patching!

  # This setting enables warnings. It's recommended, but in some cases may
  # be too noisy due to issues in dependencies.
  config.warnings = true

  # Many RSpec users commonly either run the entire suite or an individual
  # file, and it's useful to allow more verbose output when running an
  # individual spec file.
  if config.files_to_run.one?
    # Use the documentation formatter for detailed output,
    # unless a formatter has already been configured
    # (e.g. via a command-line flag).
    config.default_formatter = 'doc'
  end

  # Print the 10 slowest examples and example groups at the
  # end of the spec run, to help surface which specs are running
  # particularly slow.
  config.profile_examples = 10

  # Run specs in random order to surface order dependencies. If you find an
  # order dependency and want to debug it, you can fix the order by providing
  # the seed, which is printed after each run.
  #     --seed 1234
  config.order = :random

  # Seed global randomization in this process using the `--seed` CLI option.
  # Setting this allows you to use `--seed` to deterministically reproduce
  # test failures related to randomization by passing the same `--seed` value
  # as the one that triggered the failure.
  Kernel.srand config.seed
end
```

Here, we set the environment for testing purposes with `ENV['RACK_ENV']` and then we import the config file so it's
available to the testing framework. Of course you can write your tests now. Make yourself an `spec/app` folder and inside
it create a ruby file with, for example, `server_spec.rb` name. Fill it with this content, or read throught the code, and
think how you could write your tests. But for now I recommend sticking to my trial and error effort.

```ruby
# frozen_string_literal: true

require 'spec_helper'

RSpec.describe Server do
  def app
    Server
  end
  describe 'GET /' do
    it 'works' do
      get '/'
      expect(last_response).to be_ok
    end
  end

  describe 'ifconfig.me' do
    it 'returns ip address' do
      get '/'
      body = last_response.body
      # search for patter in body
      # that looks like an IP address
      # e.g.
      expect(body).to match(/(\d{1,3}\.){3}\d{1,3}/)
    end
  end

  describe 'Apple Music API' do
    it 'contains artist name' do
      get '/'
      body = last_response.body
      expect(body).to match(/Neosb/)
    end

    it 'contains song name' do
      get '/'
      body = last_response.body
      expect(body).to match(/Set and Settings, Vol. 9/)
    end

    it 'contains song artwork' do
      get '/'
      body = last_response.body
      expect(body).to match(/artworkUrl100/)
    end

    it 'contains song preview' do
      get '/'
      body = last_response.body
      expect(body).to match(/previewUrl/)
    end

    it 'contains song id' do
      get '/'
      body = last_response.body
      expect(body).to match(/1658237994/)
    end
  end
end
```

This are just simple tests, and they shouldn't really be here because we already tested the `curl` library, thus we
shouldn't repeat ourselfs, but instead test our implementation that extend apps, not apps already written (library, or libraries
in fact). I put this here for learning purposes, and learning by doing and sometimes repeating and doing things twice, 
and the hard way. I wanted to show you that writing tests in `Ruby` can be really expressive and simple task. I think, that you
already see that coding does not have to be done the hard way, it's just learning that you have to do before (that's why we
learn C) is sometimes hard to grasp.

In Ruby we will be writing web application that will run in container on our machine, but you can simply install all the 
dependencies using bundler and with only `ruby` and maybe `ruby-devel` package you can run the whole app. For now we will stick
to Dockerfile, which is easier to manage - at least for me.

### Erb template

Hej! Let's create a folder named `app/views`. There will live templates (one), for this example. It will be reading from
server data, that will be passed into the view. The concept should be relatively simple. In the server part, you handle
all the data mangling, calling, adding, formatting and so one, and then you will send this data as a hash (something
similar to dictionary) to the template, that will display data to the end user (your best friend, maybe).

First I will show you a wrapper, a partial, a template that is served to the user and is used to yield the actual erb index
inside it. Save this as `layout.erb`.

```erb
<doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><%= title %></title>
    <%# Include the style.css %>
    <link rel="stylesheet" href="style.css">
</head>
<body class="main">
  <%= yield %>
</body>
```

Here we use simple `HTML`, Hypertext Markup Language that is the base language of the web. It is telling the browser what to
display and where. CSS that is loaded using `<link rel...` is the syling language of the web. It tells the browser how to display
content on the webpage. There is also Java Script that is the scripting language of the web, but we don't use it here - you might
try to write in your web browser console, `console.log("Something meaningful, like the essence of life.")`.

The `yield` and the `<%= %>` syntax is `Ruby` and `erb` respectively, and it's telling the template engine to include the result
of parsing view in between `<body>`.

Then we should create `style.css`. I include mine, but you might as well change some values and play around a bit with it (after
we finish the [Sinatra app](#sinatra-app)).

```css
.main {
    background-color: #f2f2f2;
    font-family: 'Roboto', sans-serif;
    font-size: 16px;
    color: #333;
    line-height: 1.5;
}
```

And now we finish this section with `index.erb`:

```erb
<h1>C library call from Ruby</h1>
<h2>Pre-requisites</h2>
<p>
  How to compile a C library and call it from Ruby using FFI.
  <pre>
    <code>
      // curl.c
      
      #include  &lt;curl/curl.h&gt;
      ...
      // compile with:
      gcc -o curl -shared curl.c -lcurl
      // or
      gcc -o curl -shared curl.c -lcurl -fPIC
      
      # then in Ruby:
      require 'ffi'
      # Define the FFI interface to the curl() function in the shared library
      module CurlLib
        extend FFI::Library
        ffi_lib './curl'
        attach_function :curl, [:string], :string # [] is for arguments, :string is for return type
      end
      # to call the curl() function, use CurlLib.curl()
      my_ip = CurlLib.curl('https://ifconfig.me')
      puts "My IP is #{my_ip}"
    </code>
  </pre>
  <h2>ifconfig.me</h2>
  <p>
    call - <strong>CurlLib.curl('https://ifconfig.me')</strong><br /><br />
    Result:<br />
    My IP is <%= curl %>
  </p>
  <h2>Apple Music API</h2>
  <p>
    call - <strong>CurlLib.curl('https://itunes.apple.com/lookup?id=1658237994')</strong><br /><br />
    Example of calling a C library from Ruby using FFI.
    Data returned by this website is in Java Script
    Object Notation, JSON in short.<br />
    <br />
    JSON stands for JavaScript Object Notation, and it is a 
    lightweight data interchange format. JSON is used to 
    transmit data between a server and a web application as an alternative to XML.
    <br />
    <br />
    JSON is easy for humans to read and write and is easy for 
    machines to parse and generate. It is based on a subset 
    of the JavaScript programming language, so it can be parsed 
    by any modern programming language.
    <br />
    <br />
    A JSON object is a collection of key/value pairs, where the 
    keys are strings and the values can be any valid JSON data type, 
    including strings, numbers, booleans, arrays, and other JSON objects.
    <br />
    <br />
    Here is an example of a JSON object:

    <pre>
      <code>
{
  "name": "John Smith",
  "age": 35,
  "email": "john.smith@example.com",
  "is_active": true,
  "friends": ["Jane Doe", "Bob Johnson"]
}
      </code>
    </pre>
    In this example, "name", "age", "email", and "is_active" are keys, 
    and "John Smith", 35, "john.smith@example.com", and true are their 
    corresponding values. The "friends" key has an array of two strings as its value.
    <br />
    <br />
    This is data extracted from Apple Music API:<br /><br />
    <ul>
      <li>Artist: <%= song_artist %></li>
      <li>Song name: <%= song_name %></li>
      <li>Song URL: <a href="<%= song_url %>" target="_blank">take me to the song</a></li>
      <li>Artwork: <img src=<%= song_artwork %> /></li>
      <li>
        Preview:
          <audio controls>
            <source src=<%= song_preview %>>
            Your browser does not support the audio element.
          </audio>
      </li>
    </ul>
    <br />
          <br />
    raw JSON:<br />
    <pre>
      <code>
<%= song_json %>  
      </code>
    </pre>
  </p>
```

### FFI

Now we have to talk a little bit about another gem. FFI. It's used in here to call C code we wrote earlier in curl.c.
We simply create a module and extend it with a library `curl`, and assign it a function, also named curl with one
string parameter and a string return type. This code essnetially enables us to use any C library we want (Rust too),
if we know how to call this function.

```ruby
require 'ffi'

# Define the FFI interface to the curl() function in the shared library
module CurlLib
  extend FFI::Library
  ffi_lib './curl'
  attach_function :curl, [:string], :string # [] is for arguments, :string is for return type
end
```

### Sinatra app

This is the final step after which you can run `rspec spec` to test the code, and `bundle exec rerurn -- bundle exec rackup config.ru`
to run the development server with rebuild after each change to the code you make (unfortunately not for only `curl`). Here
we do not follow the standard, and easiest way to make `Sinatra` app, we inherit a class from `Sinatra::Base` what gives us the
ability to test like we do. Then we only set the main handle, the `get '/'` and inside this block we call FFI module CurlLib
with curl method and string argument twice. Once for `ifconfig.me` and once for `Apple Music API`. We save them to local variables,
mangle them a bit (to get JSON and remove %), then save relevant parts to instance variables and return from `get '/'`  with 'erb'
call with `:index`, `locals: { ... }` and `layout:` parameters. Here is the source code:

```ruby
# frozen_string_literal: true

require 'sinatra/base'
require 'ffi'
require 'json'

# Define the FFI interface to the curl() function in the shared library
module CurlLib
  extend FFI::Library
  ffi_lib './curl'
  attach_function :curl, [:string], :string # [] is for arguments, :string is for return type
end

# invoke curl() function from curl.so
# send the result to the view
class Server < Sinatra::Base
  get '/' do
    # pass @curl to the view
    myip = CurlLib.curl 'ifconfig.me'
    @myip = myip.chop # remove trailing '%' from ifconfig.me response
    @title = 'Learn C'
    song = CurlLib.curl 'https://itunes.apple.com/lookup?id=1658237994'
    song = song.strip
    @song_pretty = JSON.pretty_generate(JSON.parse(song))
    song = JSON.parse(song)
    @song_preview = song['results'][0]['previewUrl']
    @song_name = song['results'][0]['trackName']
    @song_artist = song['results'][0]['artistName']
    @song_artwork = song['results'][0]['artworkUrl100']
    @song_url = song['results'][0]['trackViewUrl']
    # pass data to the view
    erb :index,
        locals: {
          curl: @myip,
          title: 'Learn C',
          song_json: @song_pretty,
          song_preview: @song_preview,
          song_name: @song_name,
          song_artist: @song_artist,
          song_artwork: @song_artwork,
          song_url: @song_url
        }, layout: :layout
  end
end
```

### Standalone container

```Dockerfile
FROM fedora:latest

WORKDIR /app

RUN dnf groupinstall -y 'Development Tools'
RUN dnf install -y ruby ruby-devel libcurl-devel json-c-devel && gem install bundler

RUN git clone https://github.com/ThrowTheSwitch/Unity.git
COPY . /app
RUN sed -i 's/..\/unity\//Unity\/src\//' test.c && sed -i 's/-I..\/unity/-IUnity\/src/' Makefile && \
    sed -i 's/..\/unity\//Unity\/src\//' Makefile

RUN make && make test && bundle install && bundle exec rspec spec

EXPOSE 9292

ENV RACK_ENV=production 

ENTRYPOINT ["bundle", "exec", "rackup", "--host", "0.0.0.0", "config.ru" ]
```

😺

### Push to hub.docker.com

To push your work to [hub.docker.com](https://hub.docker.com), use this commands:

```bash
docker login
docker tag c-dev you_docker_username/your_repository_name:tag # e.g. docker tag c-dev neosb/curl-app
docker push your_docker_usrname/you_repository_name:tag
```

First you login to Docker Hub, then you tag your image with additional tag name (usually `latest` or `0.1.0` - you can tag twice),
then you simply push to remote repository. There you can have many openly available images, and one private. It saves space on
your disk.

#### Use GitHub Actions to publish your Docker container to hub.docker.com

```yaml
name: ci

on:
  push:
    branches:
      - 'main'

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      -
        name: Set up QEMU
        uses: docker/setup-qemu-action@v2
      -
        name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2
      -
        name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          # save this in your GitHub settings
          username: ${{ secrets.DOCKER_USERNAME }}
          # get your token from hub.docker.com profile
          password: ${{ secrets.DOCKER_TOKEN }}
      -
        name: Build and push
        uses: docker/build-push-action@v4
        with:
          push: true
          tags: username/image-name:tag
```

### Git refresher

## Stack and heap

In computer programming, the terms "stack" and "heap" refer to two different areas of memory that are used to store data 
during the execution of a program.

The stack is a region of memory that is used to store function calls and local variables. Each time a function is called, 
a new frame is created on the stack, which contains the function's arguments, local variables, and return address. When the
function returns, its frame is removed from the stack, and the program resumes execution at the return address that was 
stored in the calling function's frame. The stack is a LIFO (last-in, first-out) data structure, meaning that the most 
recently added item is the first one to be removed.

The heap, on the other hand, is a region of memory that is used for dynamic memory allocation. When a program needs to 
allocate memory at runtime, it requests a block of memory from the heap using functions like malloc() or new(). The memory 
block that is allocated can be of any size and can be accessed randomly. Unlike the stack, the heap is not automatically 
managed by the program's execution flow, so it's up to the programmer to manage the memory allocations and deallocations 
properly to prevent memory leaks or other issues.

In summary, the stack is a fixed-size region of memory that is used for function calls and local variables, while the heap 
is a dynamic region of memory that is used for dynamic memory allocation.

Stack example:

```c
#include <stdio.h>

int factorial(int n) {
    if (n == 0) {
        return 1;
    }
    return n * factorial(n - 1);
}

int main() {
    int num = 5;  // local variable stored on the stack
    int result = factorial(num);  // function call creates a new frame on the stack
    printf("Factorial of %d is %d\n", num, result);
    return 0;
}
```

In this example, we define a function factorial that calculates the factorial of a given number recursively. When we call 
this function from main, a new frame is created on the stack to store the function arguments and local variables. When the 
function returns, its frame is removed from the stack, and the program resumes execution from where it left off.

Heap example:

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p;  // pointer variable to store the address of the memory block
    int n = 5;  // number of integers to allocate

    // allocate memory block on the heap using malloc()
    p = (int*) malloc(n * sizeof(int));
    if (p == NULL) {
        printf("Failed to allocate memory on the heap\n");
        return 1;
    }

    // initialize the memory block with some values
    for (int i = 0; i < n; i++) {
        *(p + i) = i * i;
    }

    // print the values stored in the memory block
    for (int i = 0; i < n; i++) {
        printf("%d ", *(p + i));
    }

    // free the memory block when we're done using it
    free(p);

    return 0;
}
```

In this example, we use the malloc function to allocate a block of memory on the heap that can hold n integers. 
We then initialize the memory block with some values and print them out. Finally, we use the free function to 
release the memory block back to the operating system. It's important to note that we must always free the memory 
block when we're done using it to prevent memory leaks.

### Stack overflow

Stack overflow occurs when the amount of memory allocated for the stack is exceeded. This can happen when a program 
has too many nested function calls or when a function allocates too much memory on the stack for local variables.

Here are some ways to prevent stack overflow in C language:

1. Reduce the number of nested function calls: One way to prevent stack overflow is to reduce the number of nested 
function calls in your program. This can be achieved by breaking down larger functions into smaller ones, or by using 
loops instead of recursion.

2.Limit the size of local variables: If you're allocating large arrays or structures on the stack, you may run out of 
space quickly. To prevent this, you can allocate these variables on the heap instead using functions like malloc or calloc.

3. Increase the stack size: Some compilers allow you to increase the amount of memory allocated for the stack. In GCC, 
for example, you can use the -Wl,--stack,SIZE linker option to set the stack size to SIZE bytes.

4. Use tail recursion: If you're using recursion, you can use tail recursion to reduce the amount of memory used on the 
stack. Tail recursion is a technique where the recursive call is the last statement in the function, so the compiler 
can optimize it into a loop.

5. Avoid infinite recursion: Infinite recursion occurs when a function calls itself recursively without a base case. 
This can quickly exhaust the stack space and cause a stack overflow. To prevent this, make sure your recursive functions 
have a base case that terminates the recursion.

By following these tips, you can prevent stack overflow and ensure that your program runs smoothly.

### C language caveats of stack and heap

In C language, the main difference between the stack and the heap is how memory is allocated and managed.

1. Memory allocation: The stack is a static memory allocation method where the memory is allocated at compile-time. 
On the other hand, the heap is a dynamic memory allocation method where the memory is allocated at run-time.

2. Memory management: The stack is managed automatically by the system, and memory is allocated and deallocated 
in a last-in, first-out (LIFO) manner. This means that memory is automatically deallocated when a function returns 
or a variable goes out of scope. In contrast, memory on the heap is allocated and deallocated manually by the programmer,
using functions like malloc, calloc, realloc, and free.

3. Memory size: The stack is typically smaller than the heap. The size of the stack is determined at compile-time and is 
limited by the amount of available memory. The size of the heap, on the other hand, can grow or shrink dynamically at 
run-time as needed.

4. Data access: Accessing data on the stack is faster than accessing data on the heap because the stack uses a LIFO 
memory allocation method, and data is stored in contiguous blocks. In contrast, accessing data on the heap requires 
the use of pointers, which can be slower.

In summary, the stack and the heap are two different memory allocation methods in C language. The stack is a static 
memory allocation method managed automatically by the system, while the heap is a dynamic memory allocation method 
managed manually by the programmer. The size of the stack is limited and determined at compile-time, while the size 
of the heap can grow or shrink dynamically at run-time. Accessing data on the stack is faster than accessing data on the heap.

### Segmentation fault

A segmentation fault (often referred to as a "segfault") is a type of error that occurs when a program tries to access
memory that it is not allowed to access. In C, this often happens when a program tries to access memory that has not been 
allocated or has already been freed. Here are a few examples of code that can cause a segmentation fault:

1. Accessing an array out of bounds:

```c
int arr[5];
arr[6] = 42; // Accessing the 7th element of the array (which doesn't exist)
```

In this example, the program tries to access the 7th element of the arr array, which is outside the bounds of the array 
(since the array only has 5 elements). This can cause a segmentation fault because the program is trying to access memory 
that has not been allocated for the array.

2. Dereferencing a null pointer:

```c
int* ptr = NULL;
*ptr = 42; // Dereferencing a null pointer
```

In this example, the program creates a null pointer ptr, and then tries to dereference it (i.e., access the memory it points to)
and store a value in it. This can cause a segmentation fault because the program is trying to access memory that has not been 
allocated for the pointer.

```c

3. Double-freeing memory:

```c
int* ptr = malloc(sizeof(int));
free(ptr);
free(ptr); // Freeing the same memory twice
```

In this example, the program allocates memory for an integer using malloc, and then frees it using free. However, 
the program then tries to free the same memory again, which can cause a segmentation fault because the memory has 
already been freed.

These are just a few examples of situations that can cause a segmentation fault in C. In general, segmentation faults 
occur when a program tries to access memory that it is not allowed to access, so it's important to be careful when 
working with pointers and memory allocation in C.

Here's an example of how returning from a function can cause a segmentation fault in C:

```c
int* create_array(int size) {
    int arr[size];
    for (int i = 0; i < size; i++) {
        arr[i] = i;
    }
    return arr;
}

int main() {
    int* ptr = create_array(5);
    return 0;
}
```

In this example, the create_array function creates an integer array arr of size size, initializes it with values, 
and then returns a pointer to the array. However, the array arr is allocated on the stack within the function, 
which means that it is deallocated when the function returns.

When the main function calls create_array and assigns the returned pointer to ptr, ptr points to memory that has 
already been deallocated, and accessing this memory can cause a segmentation fault.

To avoid this error, we could allocate the memory for the array on the heap using malloc, which would ensure that 
the memory remains valid after the function returns:

```c
int* create_array(int size) {
    int* arr = malloc(size * sizeof(int));
    for (int i = 0; i < size; i++) {
        arr[i] = i;
    }
    return arr;
}

int main() {
    int* ptr = create_array(5);
    free(ptr); // Don't forget to free the memory when you're done with it
    return 0;
}
```

In this version of the code, the create_array function allocates memory on the heap using malloc, initializes it 
with values, and returns a pointer to the allocated memory. The main function can safely access the memory pointed 
to by ptr because it was allocated on the heap using malloc and will remain valid even after the function returns.

## Pointers to functions

In C, it is possible to declare pointers to functions, which are similar to pointers to data. A pointer to a 
function stores the memory address of a function, allowing you to call the function indirectly through the pointer. 
This can be useful in many situations, such as when you want to pass a function as an argument to another function, 
or when you want to choose which function to call at runtime based on some condition.

Here's an example of how to declare and use a pointer to a function in C:

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int main() {
    int (*p)(int, int); // Declare a pointer to a function that takes two integers as arguments and returns an integer
    p = add; // Set the pointer to point to the 'add' function
    printf("%d\n", p(2, 3)); // Call the function indirectly through the pointer
    p = subtract; // Set the pointer to point to the 'subtract' function
    printf("%d\n", p(5, 3)); // Call the function indirectly through the pointer
    return 0;
}
```

In this example, we declare a pointer p to a function that takes two integers as arguments and returns an integer. 
We then set the pointer to point to the add function using the assignment p = add, and call the function indirectly 
through the pointer using p(2, 3). We then set the pointer to point to the subtract function using p = subtract, 
and call the function indirectly through the pointer using p(5, 3).

Note that the syntax for declaring a pointer to a function includes parentheses around the pointer name and the argument 
types, as well as an asterisk to indicate that it is a pointer. In the example above, we declare the pointer as 
int (*p)(int, int) to indicate that it is a pointer to a function that takes two int arguments and returns an int.

Use `typedef before pointer function declaration. Then you can pass it as a parameter to function (callback), use
it in one function definition and then when invoking function pass other functions respecting the type of callback.

## Bad practice in C

There are many bad practices in C code that can lead to bugs, security vulnerabilities, or poor performance. 
Here are some examples:

1. Not checking return values: C functions often return error codes or null pointers to indicate errors or failure.
Failing to check these return values can lead to undefined behavior or other problems in your program.

2. Using uninitialized variables: Using uninitialized variables can lead to unpredictable behavior, as the value of an
uninitialized variable is undefined.

3. Ignoring compiler warnings: Compiler warnings indicate potential problems in your code that you should fix. Ignoring 
these warnings can lead to bugs or other issues in your program.

4. Using magic numbers: Magic numbers are hard-coded constants that appear in your code without explanation. Using magic
numbers can make your code harder to understand and maintain.

5. Not freeing dynamically allocated memory: If you allocate memory dynamically using functions like malloc or calloc, you
should free it when you're done with it using the free function. Failing to do so can lead to memory leaks and poor performance.

6. Using unsafe functions: Some C functions are considered unsafe because they can cause buffer overflows or other security
vulnerabilities if used improperly. Examples include gets, strcpy, and scanf.

7. Not handling errors properly: When your program encounters an error, it's important to handle it properly to avoid
undefined behavior or other problems. This might involve logging an error message, returning an error code, or taking
some other appropriate action.

These are just a few examples of bad practices in C code. To write high-quality, robust C code, it's important to follow
best practices and avoid common pitfalls.

### Best practice in C

Here are some best practices for writing C code:

- Use descriptive variable names: Choosing descriptive names for your variables can make your code easier to 
understand and maintain.

- Use comments to explain your code: Adding comments to your code can help others understand what your code does 
and why.

- Always initialize your variables: Initializing your variables to a known value can help avoid bugs and undefined behavior.

- Check return values and handle errors: C functions often return error codes or null pointers to indicate errors or 
failure. Always check these return values and handle errors appropriately.

- Use const and static where appropriate: Using the const keyword can help prevent accidental modifications to your 
variables, while using the static keyword can limit the scope of your variables and functions.

- Use braces around conditional statements: Adding braces around your conditional statements can help prevent bugs and
improve readability.

- Avoid using global variables: Global variables can make your code harder to understand and maintain. Instead, consider
passing values as function arguments or using local variables.

- Use preprocessor macros sparingly: Preprocessor macros can be useful for defining constants or avoiding code duplication,
but they can also make your code harder to read and maintain.

- Follow a consistent coding style: Using a consistent coding style can make your code easier to read and understand. 
Consider using a popular coding style guide, such as the Google C++ Style Guide or the GNU Coding Standards.

- Test your code thoroughly: Testing your code can help catch bugs and ensure that your code works as expected. Consider
using automated testing tools, such as unit tests or integration tests, to help catch problems early.

## Continuosly update Ruby program with output from C program

To continuously receive updates from a C function in a Ruby code, you can use interprocess communication
(IPC) mechanisms such as pipes, sockets, or shared memory. Here's an example using pipes:

1. In the C program, create a pipe using the pipe function from the unistd.h library. This creates two file
descriptors, one for reading from the pipe (pipe_fd[0]) and one for writing to the pipe (pipe_fd[1]).

2. Write the updates to the pipe using the write function.

3. In the Ruby code, read from the pipe using the IO.read method.

4. Repeat steps 2-3 in a loop to continuously receive updates.

Here's an example implementation:

C program:

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    int pipe_fd[2];
    pipe(pipe_fd);

    int i = 0;
    while (1) {
        i++;
        char buffer[100];
        sprintf(buffer, "Update %d", i);
        write(pipe_fd[1], buffer, sizeof(buffer));
        sleep(1);
    }

    return 0;
}
```

Ruby code:

```ruby
pipe_rd, pipe_wr = IO.pipe

pid = spawn("path/to/c/program", out: pipe_wr)

while true
  update = pipe_rd.read(100)
  puts update
end
```

In this example, the C program continuously writes updates to the pipe every second, and the Ruby code
continuously reads from the pipe and prints the updates. The spawn method is used to execute the C program
as a separate process, and its out option redirects the program's standard output to the pipe's write end.

## Our own API - Futures/options market in EVE Online (Hello Rust!)

I'm sorry to disappoint you, but we no longer will be using C. I know it started to being fun, and that was, because
we introduced Ruby. And while we introduce Ruby, we should and another R to our team, `Rust`. I don't love this
language, but it's much easier to use, and since I want to teach you how to write modern code, and the purpose of this
book is to keep us happy not falling into the niche of hardcore Linux maniacs, I will guide you through the process of
downloading Rust from it's website and hopefully, make you make this API for brokers (I'm working on proprietary version
of `The Floor`, `evechange` part that is the code which will be run to implement trading "on the floor". Here, we will
develop open-source version of it's cousing , `The Broker`, client to the floor trading algorithm that can connect to
the market. All of this is intended to make use case for my in-game corporation which might grow during the development of
this package.

Why Rust? I'm not an expert, as far as you might see in the forseable future, the Rust programming language is going to at least
change the development process of C and C++. We didn't touched C++, and that's the only thing we might miss during our Sinatra
and Ruby challenges ahead, because they're both object oriented, but C++ i much, much more faster. Why we don't write websites
in C++? I don't know, but we write servers in C++...

This is just a teaser about what we will do in the far ahead sections of this book. We need to learn Rust first, and by that I mean
we need to know what macro is, traits and such constructs. I will make notes, and try to enjoy the process of reading and redacting
required material for our purposes. Bear with me, and I promise, that writing a code will be breeze for you and that with Rust and
Ruby you will feel at home, you will know when to use which one of them and by the time we finish The Broker library,
you will be able to make your own recipes.

### Install Rust

To install Rust visit `https://www.rust-lang.org/learn/get-started` and follow on-screen instructions. This will download
latest version of Rust.
