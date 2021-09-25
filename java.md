
# Java

Benefits of Java: safety and portability. The safety features of the Java language ensure that a program is terminated if it tries to do something unsafe. The same Java program will run, without change, on Windows, UNIX, Linux, or Macintosh. In order to achieve portability, the Java compiler does not translate Java programs directly into CPU instructions. Instead, compiled Java programs contain instructions for the Java virtual machine, a program that simulates a real CPU. 

### basics
basic program
```java
public class HelloPrinter
{
   public static void main(String[] args)
   {  
      System.out.println("Hello, World!");
   }
}
```

To run the program, the Java compiler translates your source files (that is, the statements that you wrote) into class files. (A class file contains instructions for the Java virtual machine.) After the compiler has translated your source code into virtual machine instructions, the virtual machine executes them. During execution, the virtual machine accesses a library of pre-written code, including the implementations of the System and PrintStream classes that are necessary for displaying the program’s output.

Java source files end in ```.java```, while class files (compiled source) end in ```.class```

In Java, all programs consist of one or more classes. ```public``` denotes usable by the "public".

Files must be named according to the class contained therein. The code above would need to be saved in a file called "HelloPrinter.java".

All java programs must have a main() method.

For now consider the following code below to be necessary "plumbing" for writing code in java:

```java
public class HelloPrinter
{
   public static void main(String[] args)
   {
       System.out.println("Hello, World!");
   }
}
```

Note, each statement ends in a semicolon (;). Forgetting to type a semicolon is a common error. It confuses the compiler, because the compiler uses the semicolon to find where one statement ends and the next one starts. The compiler does not use line breaks or closing braces to recognize the end of statements.

A sequence of steps that is unambiguous, executable, and terminating is called an <ins>algorithm</ins>.

### Errors

<ins>Compile-time error</ins>: something is wrong according to the rules of the language. Detected by compiler.
<ins>Syntax error</ins>: oftenly used name for a compile-time error. Compiler refuses to translate the program into Java virtual machine instructions, and as a consequence you have no program that you can run. You must fix the error and compile again. 

<ins>Run-time error</ins>: program is syntactically correct but does something unintended (also called a <ins>logic error</ins>).

Sometimes, an <ins>exception</ins> is generated: an error message from the Java virtual machine (e.g. "Division by zero")

## Fundamental Data Types

### Variable Declarations

```java
int cansPerPack = 6;
double price = 2.50;
```

The statement above is a <ins>declaration</ins> (specification of a variable and its <ins>type</ins>). The variable ```cansPerPack``` is "<ins>initialized</ins>" with a value of 6. The ```double``` type is used for holding floating-point numbers.

### Variable Names

Variable names must begin with a letter or underscore (_). Remaining characters must be letters, numbers, or underscores. Use upper case letters to denote word boundaries.

Java uses camelCase for variable names. Variable names are case-sensitive, and reserved words cannot be used for variable names (e.g. ```double``` or ```class```). It is a java programmer convention that Class names begin with a capital letter, while variable names begin with a lower-case letter.

### Assignment

If a variable is already declared, a value can be assigned to it like so:

```java
int myNum;
myNum = 4;
```

An assignment statement stores a new value in a variable, replacing the previously stored value.

### Constants

If a variable is defined as ```final```, its value cannot be changed.

```java
final double BOTTLE_VOLUME = 2; // Liters in a 12-ounce can
```

It is customary to use all capital letters and underscores for variable names containing constants whose values should not change.

### Comments

single line comments are made with ```//```; multi-line comments made with ```/* ... */```. To create the equivalent of a "docstring" in java, i.e. a comment that explains the purpose of the program at the top of the file, use ```/**``` as the comment delimiter instead of ```/*```. Tools that analyze source files rely on this convention:

```java
/**
   This program computes the volume (in liters) of a six-pack of soda
   cans and the total volume of a six-pack and a two-liter bottle.
*/
public class Volume1
{
   public static void main(String[] args)
   {
     int cansPerPack = 6;
     final double CAN_VOLUME = 0.355; // Liters in a 12-ounce can
     double totalVolume = cansPerPack * CAN_VOLUME;

     System.out.print("A six-pack of 12-ounce cans contains ");
     System.out.print(totalVolume);
     System.out.println(" liters.");

     final double BOTTLE_VOLUME = 2; // Two-liter bottle

     totalVolume = totalVolume + BOTTLE_VOLUME;

     System.out.print("A six-pack and a two-liter bottle contain ");
     System.out.print(totalVolume);
     System.out.println(" liters.");
   }
}
```

### Numeric Types in Java


|Type	|Description | Size|
| :---        |    :----   |     :----   | 
| int |integer type, range: -2,147,4863,648 to -2,147,4863,648 | 4 bytes |
|byte|describes single byte containing 8 bits, range: -128 to 127| 1 byte|
| short |short integer type, range: -32,768...32,767 | 2 bytes |
| long |long integer type, range: about 19 decimal digits | 8 bytes |
| double |double-precision floating-point type, range: +-10^308, ~15 decimal digits | 8 bytes |
| float	| single-precision floating-point type, range: +-10^38, ~7 decimal digits | 4 bytes |
| char	| character type, representing code units in the unicode encoding scheme| 2 bytes |

For extremely large numbers, see ```BigInteger``` or ```BigDecimal``` classes in ```java.math``` package.

### Quick Advice

Avoid using "Magic Numbers"; i.e. store numbers into variables, and use the variables in expressions, rather than arbitarily including numbers in expressions.
```java

// Don't do this
totalVolume = bottles * 2;

// Instead do this
final double BOTTLE_VOLUME = 2;
totalVolume = bottles * BOTTLE_VOLUME;
```

To deal with round off errors, it is recommended to do rounding. Or, display the number up to a certain number of digits.

### Increment, Decrement

```java
int items = 0;
items++;
```

### Division with floats, ints

performing arithemetic with floats and ints is as you would expect: adding floats and ints gives floats. However, one int divided by another int gives an int result, rather than a float. The remainder is disregarded.

```java
7.0 / 4.0; // 1.75
7   / 4.0; // 1.75
7.0 / 4;   // 1.75
7   / 4;   // 1
```

Use the modulus operator ```%``` if interested in the remainder.

### Powers and Roots

There are no symbols for powers and roots. To compute them, use the ```Math``` package. 


|Method	|Returns | 
| :---        |    :----   |  
|	Math.sqrt(x)	|	Square root of x (≥ 0)	|
|	Math.pow(x, y)	|	xy (x > 0, or x = 0 and y > 0, or x < 0 and y is an integer)	|
|	Math.sin(x)	|	Sine of x (x in radians)	|
|	Math.cos(x)	|	Cosine of x	|
|	Math.tan(x)	|	Tangent of x	|
|	Math.toRadians(x)	|	Convert x degrees to radians (i.e., returns x · π/180)	|
|	Math.toDegrees(x)	|	Convert x radians to degrees (i.e., returns x · 180/π)	|
|	Math.exp(x)	|	e^x	|
|	Math.log(x)	|	Natural log (ln(x), x > 0)	|
|	Math.log10(x)	|	Decimal log (log10 (x), x > 0)	|
|	Math.round(x)	|	Closest integer to x (as a long)	|
|	Math.abs(x)	|	Absolute value | x |	|
|	Math.max(x, y)	|	The larger of x and y	|
|	Math.min(x, y)	|	The smaller of x and y	|

### Type Casting (Converting Floating-Point Numbers to Integers)

to cast objects to a different type (e.g. double to int), use ```(type)``` 

```java
double total = 1.20;
double tax = total * 0.02;
int dollars = (int) (total + tax);

```

Pay extra attention to int / int division because this truncates the remainder. This can be remedied by casting either the numerator or denomenator to a float type (e.g. ```double```) and then performing the division.

Note: it is customary to include spaces around binary operators ( + - * / % = ) for readability. For unary operators (e.g. ```-b```, the negative value of b), do not include a space between the ```-``` and ```b```.

### Combine Arithmetic and Assignment

```java
total += cans;  // same as total = total + cans;
total *= 2;     // same as total = total * 2;
```

### Input and Output

To read keyboard input, use ```Scanner``` class. Note, when using the ```Scanner``` class, another step is needed: import the ```Scanner``` class from its package. A package is a collection of classes with a related purpose. All classes in the Java library are contained in packages. The ```System``` class belongs to the package ```java.lang```. The ```Scanner``` class belongs to the package ```java.util```.

```java
import java.util.Scanner;

Scanner in = new Scanner(System.in)
```

Use ```nextInt()``` to read an integer value, ```nextDouble()``` for a floating-point number,

```java
// ask for user input
System.out.print("Please enter the number of bottles: "); // don't use println() so that user input is typed next to text
int bottles = in.nextInt();
```

Use ```next()``` to read a String value:
```java
// ask for user input
System.out.print("Please enter your name: ");
String name = in.next();
```

Call the ```hasNextInt()``` or ```hasNextDouble()``` method to ensure that the next input is a number.
```java
if (in.hasNextInt())
{
   int floor = in.nextInt();   
}
else
{
   System.out.println("Error: Not an integer.");
}
```

### Formatted Output

Use ```printf()``` method to specify how values should be formatted.

```java
System.out.printf("%10.2f", price);
// 10 is the field width (characters + decimal points)
// .2 denotes how many characters after decimal
// f denotes we are displaying a float
```

The construct ```%10.2f``` is a <ins>format specifier</ins>. ```%d``` indicates ```int```, ```%f``` indicates ```floating-point```, ```%s``` indicates ```string```. ```%n``` indicates a new line.

```java
System.out.printf("Quantity: %d Total: %10.2f", quantity, total);
```

Some example code:
```java
import java.util.Scanner;

/**
   This program prints the price per ounce for a six-pack of cans.
*/
public class Volume2
{
   public static void main(String[] args)
   {
      // Read price per pack

      Scanner in = new Scanner(System.in);

      System.out.print("Please enter the price for a six-pack: ");
      double packPrice = in.nextDouble();

      // Read can volume

      System.out.print("Please enter the volume for each can (in ounces): ");
      double canVolume = in.nextDouble();

      // Compute pack volume 
   
      final double CANS_PER_PACK = 6;
      double packVolume = canVolume * CANS_PER_PACK;

      // Compute and print price per ounce

      double pricePerOunce = packPrice / packVolume;

      System.out.printf("Price per ounce: %8.2f", pricePerOunce);
      System.out.println();
   }
}
```

More example code:
```java
import java.util.Scanner;

/**
   This program simulates a vending machine that gives change.
*/
public class VendingMachine
{
   public static void main(String[] args)
   {
      Scanner in = new Scanner(System.in);

      final int PENNIES_PER_DOLLAR = 100;
      final int PENNIES_PER_QUARTER = 25;

      System.out.print("Enter bill value (1 = $1 bill, 5 = $5 bill, etc.): ");
      int billValue = in.nextInt();
      System.out.print("Enter item price in pennies: ");
      int itemPrice = in.nextInt();

      // Compute change due

      int changeDue = PENNIES_PER_DOLLAR * billValue - itemPrice;
      int dollarCoins = changeDue / PENNIES_PER_DOLLAR;
      changeDue = changeDue % PENNIES_PER_DOLLAR;
      int quarters = changeDue / PENNIES_PER_QUARTER;

      // Print change due
      
      System.out.printf("Dollar coins: %6d", dollarCoins);
      System.out.println();
      System.out.printf("Quarters:     %6d", quarters);
      System.out.println();
   }
}
```

### String type

```String``` objects are created with quotation marks ```"myStr"```:
```java
String name = "Harry";
int n = name.length();
```

Use ```+``` operator with Strings to concatenate them.
```java
String fName = "Harry";
String lName = "Morgan";
String name = fName + " " + lName;
```

Interesting behavior when a String and int (or some object that is not String type) is added to a String: the other object is casted to a String object first. This happens whenever one of the involved objects is a String type object.
```java
String jobTitle = "Agent";
int employeeId = 7;
String bond = jobTitle + employeeId; // Agent7
```

### Escape Sequences

Use ```\``` e.g. ```"He said \"Hello\""```

### Strings and Characters

In Java, a character is a value of the type ```char```. Characters have numeric values (e.g. 'H' is encoded as 72). Character literals are denoted by single quotation marks and are not to be confused with Strings, denoted by double quotation marks:
```java
'H'  //character, a value of type char
"H"  //string, a vlaue of type String
```

The String method ```charAt()``` returns the character at an index of the String. Strings are indexed beginning at 0.

```java
String name = "Harry";
char start = name.charAt(0); 
char last = name.charAt(4);
```

The String method ```contains(char)``` returns true if the String contains the char (need to confirm later if it accepts a String type as an argument)

### Substrings

the string method ```substring(start, pastEnd)``` returns a sub String within a String object:
```java
String greeting = "Hello, World!";
String sub = greeting.substring(0, 5); // sub is "Hello" 
```

### Instance Methods and Static Methods

The Java language distinguishes between values of <ins>primitive types</ins> and <ins>objects</ins>. Numbers and characters, as well as the values ```false``` and ```true``` (discussed later), are primitive. All other values are objects. Thus, the ```String``` type is actually an object type--not a primitive type (the capital "S" in ```String``` suggests a class as well). ```int```, ```char```, ```false```, ```true``` are examples of primitives.

In Java, each object belongs to a class (all strings are objects of ```String``` class, scanner object belongs to ```Scanner``` class, ```System.out``` is an objecty of the ```PrintStream``` class). A class declares the methods you can use with its objects. A method is invoked using <ins>dot notation</ins>: the object is followed by the name of the method, and teh method is followed by parameters enclosed in parentheses.

In Java, classes can declare methods that are not invoked on objects (i.e. methods intended to be invoked using the class). These methods are called <ins>static methods</ins> ("static" comes from C/C++). An example of a static method is ```Math.sqrt(2)```. 

In contrast, a method that is invoked on an object is called an <ins>instance method</ins>. An example of an instance method is ```System.out.println("Hello")```. ```System.out``` can be seen as the object, ```println``` as the name of the method, and ```"Hello"``` as a parameter.

## Decisions

### The ```if``` statement

The if statement allows a program to carry out different actions depending on the nature of the data to be processed.

Note about brace layout. Placement of the braces does not matter ```{ }```. Using a dedicated line for brackets makes them more readable, but putting the ```{``` on a single line can save space:

```java
int actualFloor;
			  
if (floor > 13)
{
   actualFloor = floor - 1;
}
else
{
   actualFloor = floor;
}

// alternatively.
int actualFloor;
			  
if (floor > 13) {
   actualFloor = floor - 1;
}
else {
   actualFloor = floor;
}
```

Brackets are not necessary for single-line statement, but it is not recommended:
```java
if (floor > 13)
    floor--;
```

can use the ```if```, ```else if```, and ```else``` construct for flow of logic:
```java
if (richter >= 8.0)
{
   System.out.println("Most structures fall");
}
else if (richter >= 7.0)
{
   System.out.println("Many buildings destroyed");
}
else if (richter >= 6.0)
{
   System.out.println("Many buildings considerably damaged, some collapse");
}
else if (richter >= 4.5)
{
   System.out.println("Damage to poorly constructed buildings");
}
else 
{
   System.out.println("No destruction of buildings");
}
```

As a short-cut, can use the ```switch``` statement to test for many conditions:
```java
int digit = . . .;
switch (digit)
{
   case 1: digitName = "one"; break;
   case 2: digitName = "two"; break;
   case 3: digitName = "three"; break;
   case 4: digitName = "four"; break;
   case 5: digitName = "five"; break;
   case 6: digitName = "six"; break;
   case 7: digitName = "seven"; break;
   case 8: digitName = "eight"; break;
   case 9: digitName = "nine"; break;
   default: digitName = ""; break;
}

// is an alternative representation of:
int digit = . . .;
if (digit == 1) { digitName = "one"; }
else if (digit == 2) { digitName = "two"; }
else if (digit == 3) { digitName = "three"; }
else if (digit == 4) { digitName = "four"; }
else if (digit == 5) { digitName = "five"; }
else if (digit == 6) { digitName = "six"; }
else if (digit == 7) { digitName = "seven"; }
else if (digit == 8) { digitName = "eight"; }
else if (digit == 9) { digitName = "nine"; }
else { digitName = ""; }
```

Can have nested if's...


### The conditional operator

Java has a <ins>conditional operator</ins> of the form: "condition ? value1 : value2". The value of the expression is either value1 if the test passes, or it is value2 if it fails:

```java
actualFloor = floor > 13 ? floor - 1 : floor;

// equivalent to
if (floor > 13) { actualFloor = floor - 1; } else { actualFloor = floor; }
```

the conditional operator can be used anywhere a value is expected (in an expression).

### Relational Operators

|Java operator	| description | 
| :---        |    :----   |  
| > | greater than|
| >= | greater than or equal|
| < | less than|
| <= | less than or equal|
| == | equal|
| != | not equal|

Note, for comparing Strings, do not use ```str1 == str2```. This tests whether both String objects are stored at the same location in memory. Instead, compare two String objects with ```equals()``` (e.g. ```str1.equals(str2)```).

Note: to do exact comparison of floating-point numbers, calculate whether their difference is within some acceptable tolerance:
```java
final double EPSILON = 1E-14;
double r = Math.sqrt(2.0);
if (Math.abs(r * r - 2.0) < EPSILON) 
{
   System.out.println("Math.sqrt(2.0) squared is approximately 2.0"); 
}
```

The ```compareTo()``` method for String objects compares two Strings by their lexicographic order: ```str1.compareTo(str2) > 0``` (evaluates to boolean).

Some example code using operators
```java
import java.util.Scanner;

/**
   This program demonstrates comparisons of numbers and strings.
*/
public class Compare
{
   public static void main(String[] args)
   {
      // Integers

      int m = 2;
      int n = 4;

      if (m * m == n)
      {
         System.out.println("2 times 2 is four.");
      }

      // Floating-point numbers

      double x = Math.sqrt(2);
      double y = 2.0;

      if (x * x == y)
      {
         System.out.println("sqrt(2) times sqrt(2) is 2");
      }
      else
      {
         System.out.printf("sqrt(2) times sqrt(2) is not 2 but %.18f%n", x * x);
      }

      final double EPSILON = 1E-14;
      if (Math.abs(x * x - y) < EPSILON)
      {
         System.out.println("sqrt(2) times sqrt(2) is approximately 2");
      }

      // Strings

      String s = "120";
      String t = "20";

      int result = s.compareTo(t);

      String comparison;
      if (result < 0)
      {
         comparison = "comes before";
      }
      else if (result > 0)
      {
         comparison = "comes after";
      }
      else
      {
         comparison = "is the same as";
      }

      System.out.printf("The string \"%s\" %s the string \"%s\"%n", 
         s, comparison, t);

      String u = "1" + t;

      System.out.printf("The strings \"%s\" and \"%s\" are ", s, u);
      if (s != u) { System.out.print("not "); }
      System.out.print("identical. They are ");
      if (!s.equals(u)) { System.out.print("not "); }
      System.out.println("equal.");
   }
}
```

### Enumeration Types

If you want a variable to only be able to take on certain values, you can declare it as an <ins>enumeration type</ins>. It works like so:

```java

public enum FilingStatus { SINGLE, MARRIED, MARRIED_FILING_SEPARATELY }

// You can have any number of values, but you must include them all in the enum declaration. 
// You can declare variables of the enumeration type:

FilingStatus status = FilingStatus.SINGLE;
	
// If you try to assign a value that isn’t a FilingStatus, such as 2 or "S", then the compiler reports an error. 
// Use the == operator to compare enumeration values, for example: 
if (status == FilingStatus.SINGLE) . . .

// Place the enum declaration inside the class that implements your program, such as
public class TaxReturn
{
   public enum FilingStatus { SINGLE, MARRIED, MARRIED_FILING_SEPARATELY }
		  
   public static void main(String[] args)
   {
      . . .
   }
}
```

### Logging

You could debug programs by inserting print statements throughout the program. However, once the program is complete, you might want to delete the print statements. If you find another error, you would need to put the print statements back in. To overcome this issue, you can use logging.

In Java, use the ```Logger``` class, which allows you to turn off trace messages without removing them from the program.

```java
Logger.getglobal().setLevel(Level.OFF); // include this at the beginning of the main method to suppress all log messages

if (status == SINGLE)
{
   System.out.println("status is SINGLE");
   Logger.getGlobal().info("status is SINGLE");
}
```

Thus, ```Logger.getGlobal().info``` behaves similarly to ```System.out.println```.

### Boolean Variables and Operators

Use the ```&&``` operator for joining booleans with ```and```, and use the ```||``` operator for connecting booleans with ```or```.

Invert a boolean with ```!``` (e.g. ```!true``` returns ```false```). 

```&&``` and ```||``` are computed with short-circuit evaluation: as soon as a truth value is determined, no further conditions are evaluated.

```java

import java.util.Scanner;

/**
   This program demonstrates comparisons of numbers, using Boolean expressions.
*/
public class Compare2
{
   public static void main(String[] args)
   {  
      Scanner in = new Scanner(System.in);

      System.out.println("Enter two numbers (such as 3.5 4.5): ");
      double x = in.nextDouble();
      double y = in.nextDouble();
      if (x == y) 
      {
         System.out.println("They are the same.");
      }
      else 
      {
         System.out.print("The first number is ");
         if (x > y)
         {
            System.out.println("larger");
         }
         else
         {
            System.out.println("smaller");
         }

         if (-0.01 < x - y && x - y < 0.01)
         {
            System.out.println("The numbers are close together");
         }

         if (x == y + 1 || x == y - 1)
         {
            System.out.println("The numbers are one apart");
         }

         if (x > 0 && y > 0 || x < 0 && y < 0)
         {
            System.out.println("The numbers have the same sign");
         }
         else
         {
            System.out.println("The numbers have different signs");
         }
      }
   }
}
```


## Loops

### ```while``` loop

while loop: a loop that executes repeatedly while a condition is true.
```java
while (balance < TARGET)
{
   year++;
   double interest = balance * RATE / 100;
   balance = balance + interest;
}
```

A certain form of while loops that are common involve initializing and using a counter.
```java
int counter = 1; // Initialize the counter
while (counter <= 10) // Check the counter
{
   System.out.println(counter);
   counter++; // Update the counter 
}
```
Since this form is so common, the ```for``` loop was created.

### ```for``` loop

for loop: used when a variable runs from a starting point to an ending point with a constant increment or decrement. 
```java
for (int counter = 1; counter <= 10; counter++)
{
   System.out.println(counter);
}
```

It is important to note the order of execution of these statements. First, when the loop is encountered, the counter variable ```counter``` is initialized (before entering loop). Then, for each iteration in the loop, the condition is first checked before the iteration (before entering the loop). If the condition evaluates to true, the code enters the body of the loop and executes everything. Lastly, the counter variable is incremented/decremented depending on the statement in the header of the for loop (here, the counter is incremented: ```counter++```). Note, the counter could increase by 2 (```counter = counter + 2```) or even decrement (```counter--```).

### ```do``` loop

do loop: appropriate when the loop body must be executed at least once. This might be useful when you specifically want to execute some code once, and then check for a conditional statement before repeating code executed once already:

```java
int value;
do
{
   System.out.print("Enter an integer < 100: ");
   value = in.nextInt();
}
while (value >= 100);
```

### Sentinel Values

When reading a sequence of numbers, it is sometimes useful to include a non-physical number to a list of numbers to denote termination of the sequence. A sentinel serves as a signal for termination, usually. For example, in a sequence of numbers representing the number of apples picked each day, we might include "-1" at the end of the sequence to denote the end of the sequence.

Example use of a sentinel to continually read input from the user until a -1 is encountered:
```java
import java.util.Scanner;

/**
   This program prints the average of salary values that are terminated with a 
   sentinel.
*/
public class SentinelDemo
{
   public static void main(String[] args)
   {  
      double sum = 0;
      int count = 0;
      double salary = 0;
      System.out.print("Enter salaries, -1 to finish: ");
      Scanner in = new Scanner(System.in);

      // Process data until the sentinel is entered 

      while (salary != -1)
      {  
         salary = in.nextDouble();
         if (salary != -1) 
         {  
            sum = sum + salary;
            count++;
         }
      }

      // Compute and print the average

      if (count > 0)
      {
         double average = sum / count;
         System.out.println("Average salary: " + average);
      }
      else
      {
         System.out.println("No data");
      }
   }
}
```

### ```break``` statement

Loops can be terminated early using a ```break``` statement:

```java
while (true)
{
   double value = in.nextDouble();
   if (value == -1)
   {
       break;
   }
}
```

### Redirection of input and output

```Input redirection``` allows you to use text stored in a file to be used as the input in a java program. This is done with the ```<``` symbol at the command line. Likewise, output from a java program can be redirected a file using the ```>``` symbol at the command line (```output redirection```):

```bash
java SentinelDemo < numbers.txt > output.txt
```

In summary, use input redirection to read input from a file. Use output redirection to capture program output in a file.


### basic loop problems in java

Average
```java
double total = 0;
int count = 0;
while (in.hasNextDouble())
{
   double input = in.nextDouble();
   total = total + input; 
   count++;
}
double average = 0; 
if (count > 0) 
{ 
   average = total / count; 
}
```

counting matches (counting number of spaces)
```java
int spaces = 0;
for (int i = 0; i < str.length(); i++)
{
   char ch = str.charAt(i);
   if (ch == ' ')
   {
      spaces++;
   }
}
```

finding the first match
```java
boolean found = false;
char ch = '?';
int position = 0;
while (!found && position < str.length())
{
   ch = str.charAt(position);
   if (ch == 'A' || ch == 'a') { found = true; }
   else { position++; }
}
```

Prompt user until match is found
```java
boolean valid = false;
double input = 0;
while (!valid)
{
   System.out.print("Please enter a positive value < 100: ");
   input = in.nextDouble();
   if (0 < input && input < 100) { valid = true; }
   else { System.out.println("Invalid input."); }
}
```

Find largest value
```java
double largest = in.nextDouble();
while (in.hasNextDouble())
{
   double input = in.nextDouble();
   if (input > largest)
   {
      largest = input;
   }
}

