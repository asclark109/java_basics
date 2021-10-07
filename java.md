
# Java

Java Code is compiled to .class files (not binary files) which are interpretted as bytecode by the Java Virtual Machine (JVM). It is compiled down to bytecode, and the bytecode is interpretted by the JVM; so, it is both a compiled and interpretted language, technically.

No operator overloading in Java (can't redefine the * operator, for example, to mean something). Although, the + operator can be used to concatenate Strings (the single exception in Java of an operator having non-expected behavior).

Implementation Indendence: e.g. Java int is ALWAYS 32bits.

No pointers in Java. Instead, there are "Java references", which get used all the time. These behave like pointers but aren't pointers. These will be discussed later.

Version numbers in Java: "java 5.0" is actually "Jdk1.5"... Jdk1.8 was the biggest release in Java. Jdk1.8 includes the Streams API and Lambdas. With the introduction of Java 9.0, they started using modules instead of packages. The SDK was getting bloated. So, they decided to chop it up into modules. A lot of shops do not use Java 9.0 and above. Java 9.0 is not backwards compatible.

Benefits of Java: safety and portability. The safety features of the Java language ensure that a program is terminated if it tries to do something unsafe. The same Java program will run, without change, on Windows, UNIX, Linux, or Macintosh. In order to achieve portability, the Java compiler does not translate Java programs directly into CPU instructions. Instead, compiled Java programs contain instructions for the Java virtual machine, a program that simulates a real CPU. 

### Heap Memory

```static``` methods load when the program starts. Static memory holds all the necessarily imported tools (classes and their static methods).

There's also a section of memory called the ```Heap``` (an upside down tree). It is a data structure that is self-balancing and ordered. Heap memory is set aside and used to store variables in memory during runtime.

As a Java programmer, your job is to instantiate objects from classes (defined in the SDK or a 3rd party library or by you) on the heap and then manipulate and manage them. Though, still you need to begin in the static context. Static memory is more "expensive" than heap memory because it's always fully loaded when the program initializes. So, you don't want to put everything in static memory. Since we must begin in static memory, we must begin with a "driver". Thus, the driver can be seen as the class handle of the program being run.

The garbage collector of the JVM will deallocate memory off the heap as variables fall out of scope.

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

Note, by default ```java.lang.*``` is always imported. String is located in this package.

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

### Nomenclature standards

Class names are ```UpperCase```

Constants and enums are ```ALL_UPPER_CASE```

Everything else is ```lowerCamelCase```

One exception for lowerCamelCase is the constructor method for a class, which must be named the same as the Class 

```java
// upper case
public class Person {};

// all upper case
private final int MAX_OCCUPANCY;
public enum Day {SUNDAY,MONDAY,TUESDAY,WEDNESDAY,THURSDAY,FRIDAY,SATURDAY};

// lower case
private int nValue; //primitive
private double calcArea(double dWidth, double dHeight); //another primitive
private String strFirstName; //object
```

try to add an ```s``` to the end of a variable name for a local array or collection. This lets an IDE know this object is a collection
```java
boolean[] bAnswers;
String[] strCountries;
```

### Hungarian Notation (optional)

Some people add a short prefix to denote the type of an object/primitive:

|Type	|example variable name |
| :---        |    :----   |     
| boolean | bFlag|
| byte | yAge|
|char | cFirst|
|short | sRosterSize|
|int | nStudent; nC|
| long | lPopulation |
| float | fPrice|
| double | dDistanceToMoon|
| String | strFirstName |
| Date | datEncounter|

primitive variables always have one letter prefix (e.g. ```nCounter```).
Object-references have a three letter prefix (e.g. ```strName```).
Arrays and collections always have s postfix (e.g. ```strNames```).

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

The Java primatives (integers):
|Type	|Signed | Bits| Bytes| min | max |
| :---        |    :----   |     :----   |   :----   |   :----   | :----   | 
| byte | signed | 8 | 1 | -2^7 (-128)| 2^7-1 (+127) |
| short | signed | 16 | 2 | -2^15 (-32768)| 2^15-1 (+32767) |
| int | signed | 32 | 4 | -2^31 (21474833648)| 2^31-1 (+2147483647) |
| long | signed | 64 | 8 | -2^63 (-9.23E18)| 2^63-1 (+9.23E18) |

Java stores integers: -2^(bits-1) to 2^(bits-1)-1

Other Java primitives
|Type	|Signed | Bits| Bytes| min | max |
| :---        |    :----   |     :----   |   :----   |   :----   | :----   | 
| boolean | N/A | 1 | 1 | false | true |
| char | unsigned unicode | 32 | 4 | 0 (\u0000)| 2^16-1 (\uffff) |
| float | signed exponent (and mantissa) | 32 | 4 |  +-1.4E-45 |  +-3.4E38 (6-8 significant digits of accuracy)|
| double | signed exponent (and mantissa) | 64 | 8 | +-4.94E-324 | +-1.798E308 (14-15 significant digits of accuracy)|

### Wrapper Classes

Every primitive in java has a corresponding wrapper class (e.g. ```Double``` class for ```double``` primitive, ```Integer``` for ```int```, ```Boolean``` for ```boolean```, ```Character``` for ```char```). These can be used in place of primitives where you must use a primitive. Moreover, some data structures require use of objects; as an example, an Arraylist object must accept objects, and so you would need to provide Integer type objects to get a list of integers.

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

### Prefix and Postfix Unary Operators

When a prefix expression (e.g. ```++nX``` or ```--nX```) is used in an expression, the value returned is the value calculated after the prefix operator is applied.
When a postfix expression (e.g. ```++nX``` or ```--nX```) is used in an expression, the value returned is the value calculated before the postfix operator is applied.

```java
// prefix
int nX = 0;
int nY = 0;
nY = ++nX; //result: nY=1, nX=1

// postfix
int nX = 0;
int nY = 0;
nY = nX++; //result: nY=0, nX=1
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
```

### Object vs primitive

need to use ```new``` keyword to call the constructor and create an object in the heap memory.
```java
Card cardKS = new Card('K','S',10)
```

Creating an object on the heap creates a Java reference, a 64 bit memory address
```java
//e.g. Java Reference called cardKS holding a value: 7FFF_5FBF_8601_84AC 
```

### keywords

reserved keywords in Java (many similar to C/C++/C#)

```
abstract
continue
for
new
switch
assert***
default
goto*
package
synchronized
boolean
do
if
private
this
break
double
implements
protected
throw
byte
else
import
public
throws
case
enum****
instanceof
return
transient
catch
extends
int
short
try
char
final
interface
static
void
class
finally
long
strictfp**
volatile
const*
float
native
super
while

*	 	not used
**	 	added in 1.2
***	 	added in 1.4
****	 	added in 5.0
```

## Methods

Methods take the structure of (typically) ```public static``` (described later) with the ```returnType```, ```methodName(param1type param1, param2type param2, ...)```. If the function returns nothing, for example a function that mutates an object or prints out a message, the keyword ```void``` is used to designate nothing is returned by the method.

```java
public static returnType methodName(parameterType parameterName, ...)
{
    //method body
}
```
e.g.
```java
public static String getHelloStr(int duplications)
{
    String strFullHello = ""
    for (int i = 0; i < duplications; i++) {
        strFullHello += "Hello";
    }
    return strFullHello
}

public static void sayHello(int duplications)
{
    for (int i = 0; i < duplications; i++) {
        System.out.println("Hello");
    }
}
```

### javadoc conventions for methods

Copied from Big Java Late Objects Ed 2:

"Whenever you write a method, you should comment its behavior. Comments are for human readers, not compilers. The Java language provides a standard layout for method comments, called the javadoc convention"

```java
/**
   Computes the volume of a cube.
   @param sideLength the side length of the cube
   @return the volume
*/
public static double cubeVolume(double sideLength)
{
   double volume = sideLength * sideLength * sideLength;
   return volume;
} 
```

"Method comments explain the purpose of the method, the meaning of the parameter variables and return value, as well as any special requirements. 

Comments are enclosed in /** and */ delimiters. The first line of the comment describes the purpose of the method. Each @param clause describes a parameter variable and the @return clause describes the return value.

Note that the method comment does not document the implementation (how the method carries out its work) but rather the design (what the method does). The comment allows other programmers to use the method as a “black box”."

Note, In Java, a method can never change the contents of a variable that was passed as an argument.

### (Formal) Parameters vs Arguments

(Formal) Parameters are the variables created for receiving the method's arguments. Thus, parameters refer to the object within the function call, while the arguments refer to the specfic values are thare supplied to the method when it is "invoked" or "called".

### Return Values

The ```return``` statement terminates a method call and yields the method result.

Note, it is a compile-time error if some branches of a method return a value and others do not. For example:

```java
public static int sign(double number)
{
    if (number < 0) { return -1; }
    if (number > 0) { return 1; }
    // Error: missing return value if number equals 0
}
```

### methods tips

Keep them short; i.e., as a general rule of thumb, a single function should be able to fit on a single page. If it is longer, it should probably be abstracted more.

A <ins>stub</ins> method is a method that returns a simple value that is sufficient for testing another method.

### Variable Scope

The scope of a variable is the part of the program in which it is variable. For example, a method's parameter's scope would be the entirety of the method. A variable defined within a method would be called a <ins>local variable</ins>.

Two local or parameter variables can have the same name, provided that their scopes do not overlap.

```java
public static void main(String[] args)
{
    int sum = 0;
    for (int i = 1; i <= 10; i++>)
    {
        sum = sum + i;
    }
    for (int i = 1; i <= 10; i++>)
    {
        sum = sum + i;
    }
    System.out.println(sum);
}

```			

It is not legal to declare two variables with the same name in the same method in such a way that their scopes overlap. For example, the following is not legal: 

```java
public static int sumOfSquares(int n)
{
    int sum = 0;
    for (int i = 1; 1 <= n; i++)
    {
        int n = i * i;  //error
        sum = sum + n;
    }
    return sum;
}
```

## Arrays

To use arrays, import ```java.util.Arrays```.
```java
import java.util.Arrays;
```

An array collects a sequence of values of the same type. These types can be primitives or objects.

```java
// declaring array of ints that will hold 10 int values
new int[10];

// declaring array of String objects that will hold 20 String values
new String[20];

// declaring array of doubles that will hold 10 double values
new double[10];
```

Declaring new array objects
```java
// creating an array of doubles by only specifying size (empty)
double[] values = new double[5];

// creating an array of doubles by providing an array of doubles
double[] values = {1.2, 20.0, 153.0, 7.0, 7.15};
```

Accessing objects in an array with indexing
```java
// accessing the 3rd item
dThirdValue = values[2];

// updating 4th element
values[3] = dNewValue;
```

Access the array's size to make sure arrays are not indexed out of bounds. An error is thrown if the index falls outside of ```[0,values.length]```. Make us of the array variable ```array.length``` to determine the size of the array.

Typically an array will be partially filled in the sense that it will contain elements but not have reached its max size. With a partially filled array, keep a companion variable for the current size.

### Array References

An array reference specifies the location of an array. Copying the reference yields a second reference to the same array. Use the enhanced for loop if you do not need the index values in the loop body. 

```java
int[] scores = { 10, 9, 7, 4, 5 };
int[] values = scores; // Copying array reference 
// scores also points to the object {10,9,7,4,5}
```

### Enhanced for loop

You can use the enhanced for loop to visit all elements of an array.

```java
double total = 0; 
for (double element : values)
{
    total = total + element;
}
```

### Typical array tasks
filling
```java
for (int i = 0; i < values.length; i++)
{
    values[i] = i * i;
}
```

Removing an element from an array. If the order of the array does not matter, replace the item to be deleted with the last item in the list, and decrement the companion variable designating the size of the list. If the order of the list matters, it's more complicated. Then, when an item is removed, we have to move each adjacent item to the right over to the left one position.

When inserting an element, you need to do the opposite. Start at the last item in the list and move it one index to the right. Keep doing this for successive items until you get to the location where you're trying to insert a new item.

If swapping elements, use a temporary variable.

To make a true copy of an array, rather than just copying the reference to same array, use ```Arrays.copyOf(array_name,n)``` where ```array_name``` is the name of the array object and ```n``` is the allocated size of the new array (and to copy the first ```n``` values from the array to new array).

### input boilerplate

```java
double[] inputs = new double[INITIAL_SIZE];
int currentSize = 0;
while (in.hasNextDouble())
{
    // Grow the array (double its size) if it has been completely filled
    if (currentSize >= inputs.length)
	{
	    inputs = Arrays.copyOf(inputs, 2 * inputs.length); // Grow the inputs array
	}
inputs[currentSize] = in.nextDouble();
currentSize++;
}
//When you are done, you can discard any excess (unfilled) elements: 
inputs = Arrays.copyOf(inputs, currentSize);
```

### Array Sorting

Java has built in methods for sorting.
```java
Arrays.sort(values); // if array is full
Arrays.sort(values,0,currentSize); // if array is partially full
```

### Arrays with methods

Can take arrays as a parameter. Can also return arrays.

```java
public static void multiply(double[] values, double factor)
{
   for (int i = 0; i < values.length; i++)
   {
      values[i] = values[i] * factor;
   }
}

public static int[] squares(int n)
{
    int[] result = new int[n];
    for (int i = 0; i < n; i++)
    {
        result[i] = i * i;
    }
    return result;
}
```

Use the ```...``` keyword to specify variable number of input arguments
```java
public void sum(int... values)
{
   int total = 0;
   for (int i = 0; i < values.length; i++) // values is an int[]
   {
      total = total + values[i];
   }
   return total;
}
```

### Two-dim arrays (N-dim arrays)

Can create two dimensional arrays.
```java
final int COUNTRIES = 8;
final int MEDALS = 3;
int[][] counts = new int[COUNTRIES][MEDALS];
//Alternatively, you can declare and initialize the array by grouping each row: 
int[][] counts = 
{ 
    { 0, 3, 0 },
	{ 0, 0, 1 }, 
	{ 0, 0, 1 }, 
	{ 1, 0, 0 }, 
	{ 0, 0, 1 }, 
	{ 3, 1, 1 },
	{ 0, 1, 0 },
	{ 1, 0, 1 }
};
```

The number of rows can be accessed in ```array.length```, and the number of columns can be accessed with ```array[0].length```.

Similarly, higher dimensional arrays can be specified using more brackets ```[]```.
```java
int[][][] rubiksCube = new int[3][3][3];
```

### Array Lists

An array list stores a sequence of values whose size can change. The ArrayList class is a generic class: ArrayList<Type> collects elements of the specified type.

```java
import java.util.ArrayList;
ArrayList<String> names = new ArrayList<String>();

// add elements with ArrayList.add()
names.add("Jeremy);

```

Use the ```size()``` method to obtain the current size of an array list. Use the ```get()``` and ```set()``` methods to access and set items, providing an index.
Use the ```add()``` and ```remove()``` methods to add and remove array list elements.

```java
int i = names.size();
name_last = names.get(i-1);
name_last = names.set(0,"Austin");
name_last = names.add("Angela");
name_last = names.remove(0); //removes Austin
```

Looping with ArrayLists.
```java
ArrayList<String> names = . . . ;
for (String name : names)
{
    System.out.println(name);
}
//This loop is equivalent to the following basic for loop: 
for (int i = 0; i < names.size(); i++)
{
	String name = names.get(i);
	System.out.println(name);
}
```

Copying an ArrayList. pass the original ArrayList into the constructor
```java
ArrayList<String> newNames = new ArrayList<String>(names);
```

ArrayLists are objects and can be returned by a function.
```java
public static ArrayList<String> reverse(ArrayList<String> names)
{
    // Allocate a list to hold the method result
    ArrayList<String> result = new ArrayList<String>();
			  
    // Traverse the names list in reverse order, starting with the last element
    for (int i = names.size() - 1; i >= 0; i--)
    {
        // Add each name to the result
        result.add(names.get(i));
    }
    return result;
}
```

### Wrappers and Auto-boxing

In java, you can't directly insert primitive type values (numbers, charactors or boolean values) into array lists. So, you must use these primitive types' wrapper classes

| Primitive Type	| Wrapper Class |
| :---        |    :----   |     
| byte | Byte|
| boolean | Bollean|
| char | Character|
| double | Double|
| float | Float|
| int | Integer|
| long | Long | 
|short | Short|

Conversion between primitive types and the corresponding wrapper classes is automatic. This process is called auto-boxing (even though auto-wrapping would have been more consistent).

For example, if you assign a double value to a Double variable, the number is automatically “put into a box” (see Figure 19).

Storing Input Values in an Array List
```java
ArrayList<Double> inputs = new ArrayList<Double>();
while (in.hasNextDouble())
{
inputs.add(in.nextDouble());
}
```

### Array vs ArrayList

If the size of a collection never changes, use an array.
If you collect a long sequence of primitive type values and you are concerned about efficiency, use an array.
Otherwise, use an array list.'

### Note: Array/ArrayList

Java syntax can be a little inconsistent:
| Data Type	| Number of elements |
| :---        |    :----   |     
| Array | a.length |
| Array List | a.size() |
| String | a.length() |

### Diamond Syntax

There is a convenient syntax enhancement for declaring array lists and other generic classes. In a statement that declares and constructs an array list, you need not repeat the type parameter in the constructor. That is, you can write

```java
ArrayList<String> names = new ArrayList<>();

// instead of
ArrayList<String> names = new ArrayList<String>();
```

This is called diamond syntax because of the ```<>``` symbol that forms.

## Input / Output and Exception HAndling

### Reading / Writing files

Use the Scanner class for reading text files.
```java
// create a file object
File inputFile = new File("input.txt");

// create a scanner object to read the file
Scanner in = new Scanner(inputFile);

// process the file by iterating through lines
while (in.hasNextDouble())
{
    double value = in.nextDouble();
    //Process value.
}
```

With a Scanner, use ```next()``` to read the next String that is delimited by white space.
```java
while (in.hasNext())
{
    String input = in.next();
    System.out.println(input);
}
```

To read char's from a file, use the ```Scanner.useDelimiter()``` method to change the delimiter for reading
```java
Scanner in = new Scanner(. . .);
in.useDelimiter(""); 
// Now each call to next returns a string consisting of a single character. Here is how you can process the characters:
while (in.hasNext())
{
    char ch = in.next().charAt(0);
    // Process ch.
}
```

To classify character as they are read with a Scanner, use the ```Character.isDigit()``` or other Character class static methods.

To read an entire line, use ```Scanner.nextLine()```.
```java
String line = in.nextLine();
```

Note, you can use the Scanner object to read the characters from a String:
```java
Scanner lineScanner = new Scanner(line);
// Then you can use lineScanner like any other Scanner object, reading words and numbers:
String countryName = lineScanner.next(); // Read first word
```

When writing text files, use the PrintWriter class and the print/println/printf methods.
```java
// if file alread exists, it is emptied before new data is written into it.
// if the files doesn't exist, an empty file is created
PrintWriter out = new PrintWriter("output.txt"); 
```

The ```PrintWriter``` class is an enhancement of the ```PrintStream``` class that you already know—```System.out``` is a PrintStream object. You can use the familiar ```print```, ```println```, and ```printf``` methods with any PrintWriter object:
```java
out.println("Hello, World!");
out.printf("Total: %8.2f%n", total);
```

Close files when done with them.
```java
in.close();
out.close();
```

### Notes

Note, may need to use escape characters when specifying a path:
```java
File inputFile = new File("c:\\homework\\input.dat");
```

Note: ```Scanner``` uses a File object, not a String object representing the location of the file, whereas The PrintWriter does accept a String.
To specify just a file location for the Scanner class, create a File object in-line like so:
```java
Scanner in = new Scanner(new File("input.txt"))
```

If a string contains the digits of a number, you use the ```Integer.parseInt``` or ```Double.parseDouble``` method to obtain the number value.
```java
int populationValue = Integer.parseInt(population);
// populationValue is the integer 303824646

double price = Double.parseDouble(input); 
// price is the floating-point number 3.95 

// an error will be thrown if population has any non digit characters, such as spaces. So we can use trim()
int populationValue = Integer.parseInt(population.trim());
```

Avoid errors when reading numbers by wrapping reading the next input from Scanner with an if statement
```java
if (in.hasNextInt())
{
int value = in.nextInt();
// ...
}
// also use hasNextDouble method before calling nextDouble.
```

Reading an entire file into a list: use the Files class, which provides methods to work with files and directories. The Files class requires that you specify file paths as Path objects. The Paths.get method turns a string containing a file path into such an object. Use these commands:
```java
String filename = "my\\file\\path";
List<String> lines = Files.readAllLines(Paths.get(filename));
String content = new String(Files.readAllBytes(Paths.get(filename)));
```

### Formatting Output

Format Flags
| Flag	| Meaning | Example |
| :---        |    :----   |     :----   | 
| - | left alignment | 1.23 followed by spaces   |
| 0 | Show leading zeroes | 001.23  |
| + | Show a plus sign for positive numbers | +1.23  |
| ( | Enclose negative numbers in parentheses | (1.23)  |
| , | Show decimal separators | 12,300 |
| ^ | Convert letters to uppercase | 1.23E+1 |

Format Types
| Code	| Type | Example |
| :---        |    :----   |     :----   | 
| d | Decimal integer | 123  |
| f | fixed floating-point | 12.30  |
| e | exponential floating-point | 1.23e+1  |
| g | General floating-point (exponential notation is used for very large or very small values) | 12.3  |
| s | String | Tax: |

### Command Line Arguments

Programs that start from the command line receive the command line arguments in the main method:
```public static void main(String[] args)```

Consider the example
```bash
java ProgramClass -v input.dat
```

Then, the following elements exist in args
```java
args[0] //   "-v"
args[1] //   "input.dat"
```

### Throwing Exceptions

Exceptions in Java

![alt text](pics\exceptions_tree.png "Title")

To signal an exceptional condition, use the throw statement to throw an exception object. Do so when an error condition is encountered (and in such a situation you want the program to ultimately terminate after perhaps doing additional tasks). Moreover, when you throw an exception, processing continues in an exception handler.

```java
if (amount > balance)
{
    throw new IllegalArgumentException("Amount exceeds balance");
}   
```

Place the statements that can cause an exception inside a try block, and the handler inside a catch clause (try / catch / catch... paradigm).
```java
try 
{ 
String filename = . . .;
Scanner in = new Scanner(new File(filename));
String input = in.next();
int value = Integer.parseInt(input);
//. . .
} 
catch (IOException exception) 
{
    exception.printStackTrace();
} 
catch (NumberFormatException exception) 
{
    System.out.println(exception.getMessage());
} 
```

### Checked Exceptions

In java, exceptions that you can throw and catch fall into three categories:

<ins>Internal Errors</ins>: descendants of the type ```Error```. These are fatal errors that happen rarely, and these are seldom thought about.
<ins>Unchecked exceptions</ins>: descendents of the type ```RuntimeException``` (e.g. ```IndexOutOfBoundsException```,```IllegalArgumentException```) indicate errors in your code.
<ins>Checked exceptions</ins>: these exceptions indicate that something has gone wrong for some external reason beyond your control.

Checked exceptions are due to external circumstances that the programmer cannot prevent. The compiler checks that your program handles these exceptions.

Add a throws clause to a method that can throw a checked exception.
```java
public static String readData(String filename) throws FileNotFoundException 
{
    File inFile = new File(filename);
    Scanner in = new Scanner(inFile);
	//. . .
}
```

The throws clause signals the caller of your method that it may encounter a FileNotFoundException. Then the caller needs to make the same decision—handle the exception, or declare that the exception may be thrown. 

### Closing Resources

The ```try-with-resources``` statement ensures that a resource is closed when the statement ends normally or due to an exception.
```java
try (PrintWriter out = new PrintWriter(filename))
{
    writeData(out);
} // out.close() is always called
```

When the try block is completed, the close method is called on the variable. If no exception has occurred, this happens when the writeData method returns. However, if an exception occurs, the close method is invoked before the exception is passed to its handler.

You can declare multiple variables in a try-with-resources statement, like this:
```java
try (Scanner in = new Scanner(inFile); PrintWriter out = new PrintWriter(outFile))
{
    while (in.hasNextLine())
	{
        String input = in.nextLine();
		String result = process(input);
		out.println(result);
	}
} // Both in.close() and out.close() are called here
```

### Assertions

Throw an assertion when you want to assert that something should be true at all times in a particular program location.
```java
public double deposit(double amount)
{
    assert amount >= 0;
    balance = balance + amount;
}
```

When running a java file, assertion checking is disabled by default. To execute a program with assertion checking turned on use:
```bash
java -enableassertions MainClass
```

### Application: Handling Input Errors

When designing a program, ask yourself what kinds of exceptions can occur. For each exception, you need to decide which part of your program can competently handle it.

```java
import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.Scanner;
import java.util.NoSuchElementException;

/**
   This program processes a file containing a count followed by data values.
   If the file doesn't exist or the format is incorrect, you can specify 
   another file.

   Five files are provided:

   good.txt  bad1.txt   bad2.txt   bad3.txt   bad4.txt
   --------  --------   --------   --------   --------
   10        10         ten        10         10  
   1         1          1          one        1  
   2         2          2          2          2  
   3         3          3          3          3  
   4         4          4          4          4  
   5         5          5          5          5  
   6         6          6          6          6  
   7         7          7          7          7  
   8         8          8          8          8  
   9         9          9          9          9  
   10                   10         10         10 
                                              11
*/
public class DataAnalyzer
{
   public static void main(String[] args)
   {
      Scanner in = new Scanner(System.in);

      // Keep trying until there are no more exceptions

      boolean done = false;
      while (!done)
      {
         try
         {
            System.out.print("Please enter the file name: ");
            String filename = in.next();
            
            double[] data = readFile(filename);

            // As an example for processing the data, we compute the sum

            double sum = 0;
            for (double d : data) { sum = sum + d; }
            System.out.println("The sum is " + sum);

            done = true;
         }
         catch (FileNotFoundException exception)
         {
            System.out.println("File not found.");
         }
         catch (NoSuchElementException exception)
         {
            System.out.println("File contents invalid.");
         }
         catch (IOException exception)
         {
            exception.printStackTrace();
         }
      }
   }

   /**
      Opens a file and reads a data set.
      @param filename the name of the file holding the data
      @return the data in the file
   */
   public static double[] readFile(String filename) throws IOException
   {
      File inFile = new File(filename);
      try (Scanner in = new Scanner(inFile))
      {
         return readData(in);
      }
   }

   /**
      Reads a data set.
      @param in the scanner that scans the data
      @return the data set
   */
   public static double[] readData(Scanner in) throws IOException
   {
      int numberOfValues = in.nextInt(); // May throw NoSuchElementException
      double[] data = new double[numberOfValues];

      for (int i = 0; i < numberOfValues; i++)
      {
         data[i] = in.nextDouble(); // May throw NoSuchElementException
      }

      if (in.hasNext())
      {
         throw new IOException("End of file expected");
      }
      return data;
   }
}
```

## Classes, Constructors

### Constructors

Every class has a built-in constructor. The default constructor is overriden if you define a constructor for the class.

The constructor method has the same name as the class (Very important - otherwise it is not a constructor).

It is the only method that is allowed to be capitalized (it must match the class name, which is capitalized).

If you don't define a constructor, a default no-arg constructor is implied that will set fields to zero, or null.

If you define any constructor, then the default constructor is not available to you.

Creating an object is called <ins>instantiation</ins>.

```java

// by default, java.lang.* is always imported
// import java.lang.*;

public class Intern {

    private String name;

}
```

Every object in Java ```extends``` the Object class (the "cosmic superclass")

```java

// by default, java.lang.* is always imported
// import java.lang.* is hidden from you
import java.lang.*;

// "extends Object" is hidden from you
public class Intern extends Object {

    private String name;

    // default constructor is hidden from you
    public Intern() {

    }
}
```

As soon as we type out the constructor ourselves, we overwrite the hidden default constructor. You define multiple constructors; for example, one constructor that accepts no parameters, one constructor that accepts one parameter.
```java
// POJO: Plain old java object
public class Intern {

    private String name;

    public Intern(String name) {
        this.name = name;
    }

    public String getName(){
        return this.name;
    }

    public void setName(String name){
        this.name = name;
    }
}
```

Note, you are only instiating an object when the ```new``` keyword is used; the only exception is a String literal (equivalent to ```new String("Alice")```).

```java
// note: firstIntern is a 64 bit memory address to an object instantiated on the heap.
Intern firstIntern = new Intern("Alice");

// note: you do not necessarily need a reference for an object you are instantiating.
// this prints the memory address of the new object created on the heap.
System.out.println(new Intern("David")); 
```

### Passing (primitives vs objects)

(1) Everything is passed by value in Java; however, when you pass an object reference, you are making
a copy of the memory address. So, when you give the method the memory address, you are giving that method
the ability to mutate that object. When passing a primitive, you are not mutating anything; the original
primitive stays the same value.
(2) When you pass an object to a method, you are passing a copy of the memory address to that method.



```java

// ... in the main method
int nNumber = 5;
multByFive(nNumber);
System.out.println("nNumber: " + nNumber)
// ...

// NOTE: nMNumber EVALUATES TO 5. NOT 25
// this is copies of primitives are made when passed into methods

private static void multByFive(int nParam){
    nParam = nParam * 5;
}

```

```java

// ... in the main method
Rectangle recSquare = new Rectangle(1,1,10,10);
//0x67AB
doubleRec(recSquare);
System.out.println("recSquare: " + recSquare)
// ...

// NOTE: this mutates recSquare!!!
// this is because the memory address is copied into the method
// which points to the same object on the heap.
// like as if you would send someone a copy of your credit card number


private static void doubleRec(Rectangle rec){
    rec.setSize(rec.width *2, rec.height*2)
}

```



## Strings

Strings are object. Can initialize them without the ```new``` keyword, which makes them special.

Strings are immutable (discussed later).

Strings may be pooled. In other words, if you create two distinct String objects that hold the same value (e.g. "Austin", java will decide to have both object references be the same--point to the same object in memory; this is to save memory). 

\+ operator is overloaded for the String object.

```==``` compares memory addresses. For 99% of the time, when two distinct objects are compared this will evaluate to false. The exception is String objects that have been pooled, or primitives (e.g. ```51.20 == 51.20```)

```java
// consider this code

String strSum = "";


// this code creates 100 objects on the heap
// what is preferred is to use a StringBuilder, an object that allows you to mutate
// a String

StringBuilder stringBuilder = new StringBuilder();
for (int nC = 0; nC < 100; nC++) {
    stringBuilder.append(nC)
}

String strSum = stringBuilder.toString();
```

## Static Context

Uses for Static: Driver main, Driver helper-methods, Utility methods, Constants.

The Static context is loaded at the beginning of runtime: static methods, static variables will be loaded at the start of runtime, and one copy of them will get made.

In the static context, you need a class to act as the Driver. It needs a ```main()``` method. It is normal for the Driver class to have private static method: private meaning it can only be seen by Driver (because only the Driver class needs to see that method), and static because it is intended to be used from the Class, not from an instance of that class (an instantiated object that we created on the heap).

Note, if you wanted to create a class to house methods, and it would never make sense to instantiate an object of the class, you could define a private constructor for that class:
```java
public class Convert{
    
    private Convert() {
    }

    public static double tempToMetric(double dFar){
        // calc stuff
        return (dFar-32) * 5.0/9.0;
    }

    public static double tempToImperial(double dCel){
        // calc stuff
        return dCel * 9.0/5.0 + 32;
    }
}
```

Trying to instantiate the class would result in an error: ```Math math = new Math();```

Mentioned above, we might want to make constants static:
```java
public class Intern {

    // note all interns might belong to the same company. So this variable
    // would be found in every instance of a student.

    // public final String company = "Apple Computer";

    // In an effort to be more efficient we can and should declare it static,
    // a variable that belongs to the blueprint rather than to every instance
    // of the class. Now, it being static means there will only be one copy
    // of it.

    public final static String company = "Apple Computer";
}

```

### Implicit, Explicit Parameters

In the function call ```strName.indexOf(cSpace);```, cSpace is an explicit reference, and strName is an implicit reference. strName is implicitly passed into the method. So, instance methods will have an implicit parameter (the object instance).

If a method is called from the class (from the static context), as in a static method, there will be no implicit reference: ```Math.pow(2,3)```. So, static methods won't have implicit parameters.

## Packages

<ins>Packages</ins>: a collection of classes with a related purpose.

Remember ```java.lang.*``` is imported always automatically. The SDK contains many additional packages, however.

Import library classes by specifying the package and class name:
```java
import java.awt.Rectangle;
```

You can use the fully qualifed packages in-situ like so
```java
java.awt.Rectangle rect = new java.awt.Rectangle(1,3,56,34);
```

But this is uncommon. Instead it is more common to do
```java
import java.awt.Rectangle;

// . . .

Rectange\le rect = new Rectangle(1,3,56,34)
```

### Casting Primitives

```java

// can create floats by directly casting or appending an f:
float fValue = 89393.0008f;
float fValue = 89393.0008F;
float fValue = (float) 89393.0008;

// can create longs by directly casting or appending an L:
long lValue = 8984651684351381384l; // works, but VERY BAD PRACTICE because "l" hard to read!
long lValue = 8984651684351381384L; // recommended
long lValue = (long) 8984651684351381384; // recommended

// casting from integer to byte can be very weird and unexpected
// consider 393.
// consider the binary rep: 0000 0000 0000 0000 0000 0001 1000 1001
// casting to a byte lumps off (truncates) the leading however
// many bits until 8 bits are obtained:
//                                                     1000 1001
// result: -119
int nNumber = 393;
byte yNumber = (byte) nNumber;
```

### Techniques: reading input

Each Wrapper class has a parse function:
```java
Integer.parseInt(String str);
Double.parseDouble(String str);
Byte.parseByte(String str);
Boolean.parseBoolean(String str);
Character.parseCharacter(String str); // need to confirm
```

```System.in``` has minimal set of features -- can only read one byte at a time

```Scanner``` was added in java 5.0 to read keyboard input in a convenient manner. It has helpful methods like ```nextDouble(), nextLine(), next()```, which reads a double, a line (until user hits enter), and a word (until any white space), respectively.

There's a Random class that is helpful.
```java
import java.util.Random;
Random ran = new Random();
int n = ran.nextInt();
double d = ran.nextDouble();
int n = ran.nextInt(20); // 0-19
```