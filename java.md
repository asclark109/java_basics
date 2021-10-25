
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


## OOP

A class describes a set of objects with the same behavior.

The set of all methods provided by a class, together with a description of their behavior, is called the <ins>public interface</ins> of the class. 

Every class has a public interface: a collection of methods through which the objects of the class can be manipulated.
			
The process of providing a public interface, while hiding the implementation details, is called <ins>encapsulation</ins>. Encapsulation is the act of providing a public interface and hiding the implementation details.

Encapsulation enables changes in the implementation without affecting users of a class.

### Implementing a Simple Class

The methods of a class define the behavior of its objects.

The methods of a class define the behavior of its objects.

An object stores its state in instance variables. An instance of a class is an object of the class. Thus, an instance variable is a storage location that is present in each object of the class. You specify instance variables in the class declaration:

```java
public class Counter {  
       private int value;
       // ...
}
```

An instance variable declaration consists of the following parts: 
•A modifier (private) 
•The type of the instance variable (such as int) 
•The name of the instance variable (such as value) 

Each object of a class has its own set of instance variables.

The methods that you invoke on an object are called <ins>instance</ins> methods. An instance method can access the instance variables of the object on which it acts.

```java
public int getValue()
{
    return value;
}
```

A private instance variable can only be accessed by the methods of its own class.

### Class Public Interface

When designing a class, you start by specifying its public interface. The public interface of a class consists of all methods that a user of the class may want to apply to its objects. You can use method headers and method comments to specify the public interface of a class.

```java

/**
    A simulated cash register that tracks the item
    count and the total amount due.
*/
public class CashRegister
{
    //private data—see Section 8.4

    /**
        Adds an item to this cash register.
        @param price the price of this item
    */
    public void addItem(double price)
    { 
        //implementation
    }
    
    /**
        Gets the price of all items in the current sale.
        @return the total price
    */
    public double getTotal()
    { 
        //implementation
    }
    
    /**
        Gets the number of items in the current sale.
        @return the item count
    */
    public int getCount()
    { 
        //implementation
    } 
    
    /**
        Clears the item count and the total.
    */
    public void clear()
    { 
        //implementation
    }
}
```

The method declarations and comments make up the <ins>public interface</ins> of the class. The data and the method bodies make up the <ins>private implementation</ins> of the class. Note that the methods of the CashRegister class are instance methods. They are not declared as static. You invoke them on objects (or instances) of the CashRegister class.

It is useful to classify its methods as <ins>mutators</ins> and <ins>accessors</ins>. A <ins>mutator</ins> method modifies the object on which it operates. The CashRegister class has two mutators: addItem and clear. An <ins>accessor</ins> method queries the object for some information without changing it. The CashRegister class has two accessors: getTotal and getCount. The CashRegister class has two accessors: getTotal and getCount.

### Javadoc Utility

The javadoc utility formats documentation comments into a neat set of documents that you can view in a web browser. It makes good use of the seemingly repetitive phrases. The first sentence of each method comment is used for a summary table of all methods of your class. The ```@param``` and ```@return``` comments are neatly formatted in the detail description of each method. If you omit any of the comments, then javadoc generates documents that look strangely empty. 

You can invoke the javadoc utility from a shell window, by issuing the command ```javadoc MyClass.java```

The javadoc tool is wonderful because it does one thing right: It allows you to put the documentation together with your code. That way, when you update your programs, you can see right away which documentation needs to be updated. Hopefully, you will update it right then and there. Afterward, run javadoc again and get updated information that is timely and nicely formatted.

### Data Representation (private variables)

Each accessor method must either retrieve a stored value or compute the result.

Commonly, there is more than one way of representing the data of an object, and you must make a choice.

Be sure that your data representation supports method calls in any order.

### Instance Methods

boiler plate:

```java
modifiers returnType methodName(paramType parameterName, ... )
{
    method body
}


// EX
public void addItem(double price){
    itemCount ++;
    totalPrice = totalPrice + price;
}
```

The object on which an instance method is applied is the implicit parameter. for instance when executing the method ```register1.addItem(1.95)```, register1 is passed in the method as an implicit parameter. That is how JVM would know which Register object's private variables we want to manipulate. In Java, you do not actually write the implicit parameter in the method declaration. For that reason, the parameter is called “implicit”. 

Explicit parameters of a method are listed in the method declaration.

### Tip: All Instance Variables Should Be Private; Most Methods Should Be Public

It is possible to declare instance variables as public, but you should not do that in your own code. Always use encapsulation, with private instance variables that are manipulated with methods.

Typically, methods are public. However, sometimes you have a method that is used only as a helper method by other methods. In that case, you can make the helper method private. Simply use the private reserved word when declaring the method.


### Constructors

A <ins>constructor</ins> initializes the instance variables of an object. The constructor is automatically called whenever an object is created with the new operator. A constructor initializes the instance variables of an object. A constructor is invoked when an object is created with the new operator.

```java
Scanner in = new Scanner(System.in);
```

The name of a constructor is the same as the class name.

```java
public class CashRegister
{
    . . .
    
    /**
        Constructs a cash register with cleared item count and total.
    */
    public CashRegister() // A constructor
    { 
        itemCount = 0;
        totalPrice = 0;
    }
}
```

A class can have multiple constructors.
```java
public class BankAccount
{ 
    . . .
    
    /**
        Constructs a bank account with a zero balance.
    */
    public BankAccount() { . . . }
    
    /**
        Constructs a bank account with a given balance.
        @param initialBalance the initial balance
    */
    public BankAccount(double initialBalance) { . . . }
}     
```

The compiler picks the constructor that matches the construction arguments.

```java
BankAccount joesAccount = new BankAccount(); 
// Uses BankAccount() constructor
BankAccount lisasAccount = new BankAccount(499.95); 
// Uses BankAccount(double) constructor
```

If you do not initialize an instance variable in a constructor, it is automatically set to a default value: by default, numbers are initialized as 0, Booleans as false, and object references as null that indicates that no object is associated with the variable. This is usually not desirable, and you should initialize object references in your constructors.

In this regard, instance variables differ from local variables declared inside methods. The computer reports an error if you use a local variable that has not been explicitly initialized. 

If you do not supply any constructor for a class, the compiler automatically generates a constructor. That constructor has no arguments, and it initializes all instance variables with their default values. Therefore, every class has at least one constructor. If you do not supply any constructor for a class, the compiler automatically generates a constructor. That constructor has no arguments, and it initializes all instance variables with their default values. Therefore, every class has at least one constructor.

```java
public class Intern{
    // default constructor is hidden from you
    public Intern() {

    }
}
```

#### common errors / topics

TRYING TO CALL A CONSTRUCTOR

A constructor is not a method. You must use it in combination with the new reserved word:

```CashRegister register1 = new CashRegister();```

After an object has been constructed, you cannot invoke the constructor on that object again. For example, you cannot call the constructor to clear an object:

```register1.CashRegister(); // Error```
			
It is true that the constructor can set a new CashRegister object to the cleared state, but you cannot invoke a constructor on an existing object. However, you can replace the object with a new one:

```register1 = new CashRegister(); // OK```

DECLARING A CONSTRUCTOR AS VOID

Do not use the void reserved word when you declare a constructor:

```public void BankAccount()  // Error—don’t use void!```

This would declare a method with return type void and not a constructor. Unfortunately, the Java compiler does not consider this a syntax error.

OVERLOADING

When the same method name is used for more than one method, then the name is overloaded. In Java you can overload method names provided that the parameter types are different. For example, you can declare two methods, both called print:

```java
public void print(CashRegister register)
public void print(BankAccount account)
//When the print method is called,
print(x);
```

rhe compiler looks at the type of x. If x is a CashRegister object, the first method is called. If x is an BankAccount object, the second method is called. If x is neither, the compiler generates an error.
	
We have not discussed the overloading feature. Instead, we give each method a unique name, such as printRegister or printAccount. However, we have no choice with constructors. Java demands that the name of a constructor equal the name of the class. If a class has more than one constructor, then that name must be overloaded.

### Testing a Class

In the long run, your class may become a part of a larger program that interacts with users, stores data in files, and so on. However, before integrating a class into a program, it is always a good idea to test it in isolation. Testing in isolation, outside a complete program, is called unit testing.

To test your class, you have two choices. Some interactive development environments, such as BlueJ (http://bluej.org) and Dr. Java (http://drjava.org), have commands for constructing objects and invoking methods. Then you can test a class simply by constructing an object, calling methods, and verifying that you get the expected return values. Figure 7 shows the result of calling the getTotal method on a CashRegister object in BlueJ.

Alternatively, you can write a tester class. A tester class is a class with a main method that contains statements to run methods of another class. A tester class typically carries out the following steps:

1.Construct one or more objects of the class that is being tested.
2.Invoke one or more methods.
3.Print out one or more results.
4.Print the expected results. 

A <ins>unit test</ins> verifies that a class works correctly in isolation, outside a complete program. To test a class, use an environment for interactive testing, or write a tester class to execute test instructions.

Determining the expected result in advance is an important part of testing. 

```java
/**
   This program tests the CashRegister class.
*/
public class CashRegisterTester
{
   public static void main(String[] args)
   {
      CashRegister register1 = new CashRegister();
      register1.addItem(1.95);
      register1.addItem(0.95);
      register1.addItem(2.50);
      System.out.println(register1.getCount());
      System.out.println("Expected: 3");
      System.out.printf("%.2f%n", register1.getTotal());
      System.out.println("Expected: 5.40");
   }
}
```

```java
/**
   A simulated cash register that tracks the item count and
   the total amount due.
 */
public class CashRegister
{
   private int itemCount;
   private double totalPrice;

   /**
      Constructs a cash register with cleared item count and total.
   */
   public CashRegister()
   {
      itemCount = 0;
      totalPrice = 0;
   }

   /**
      Adds an item to this cash register.
      @param price the price of this item
   */
   public void addItem(double price)
   {
      itemCount++;
      totalPrice = totalPrice + price;
   }

   /**
      Gets the price of all items in the current sale.
      @return the total amount
   */
   public double getTotal()
   {
      return totalPrice; 
   }
   
   /**
      Gets the number of items in the current sale.
      @return the item count
   */
   public int getCount()
   {
      return itemCount; 
   }

   /**
      Clears the item count and the total.
   */
   public void clear()
   {
      itemCount = 0;
      totalPrice = 0;
   }
}
```

To produce a program, you need to combine the CashRegister and CashRegisterTester classes. The details for building the program depend on your compiler and development environment. In most environments, you need to carry out these steps:

1.Make a new subfolder for your program. 
2.Make two files, one for each class. 
3.Compile both files. 
4.Run the test program. 

### Object References

In Java, a variable whose type is a class does not actually hold an object. It merely holds the memory location of an object. The object itself is stored elsewhere.

We use the technical term object reference to denote the memory location of an object. When a variable contains the memory location of an object, we say that it refers to an object. For example, after the statement

```java
CashRegister reg1 = new CashRegister();   
```

the variable reg1 refers to the CashRegister object that the new operator constructed. Technically speaking, the new operator returned a reference to the new object, and that reference is stored in the reg1 variable.


### Shared References

You can have two (or more) object variables that store references to the same object, for example by assigning one to the other.

```java
CashRegister reg2 = reg1;
```

Now you can access the same CashRegister object both as reg1 and as reg2.

In this regard, object variables differ from variables for primitive types (numbers, characters, and boolean values). When you declare

```java
int num1 = 0;
```

Then the num1 variable holds the number 0, not a reference to the number.

NOTE: Multiple object variables can contain references to the same object.
NOTE: Primitive type variables store values. Object variables store references.

When copying an object reference, you have two references to the same object.

There is a reason for the difference between primitives and objects. In the computer, each primitive requires a small amount of memory. But objects can be very large. It is far more efficient to manipulate only the memory location. 

### The null reference

An object reference can have the special value null if it refers to no object at all. It is common to use the null value to indicate that a value has never been set. For example,

```java
String middleInitial = null; // No middle initial 
```

The null reference refers to no object. You use the == operator (and not equals) to test whether an object reference is a null reference.

### ```this``` reference

Every instance method receives the implicit parameter in a variable called this. For example, consider the method call

```java
reg1.addItem(2.95);
```

When the method is called, the parameter variable ```this``` refers to the same object as reg1.

You don’t usually need to use the this reference, but you can. For example, you can write the addItem method like this:

```java
void addItem(double price)
{
    this.itemCount++;
    this.totalPrice = this.totalPrice + price;
}
```

Some programmers like to use the this reference to make it clear that itemCount and totalPrice are instance variables and not local variables. You may want to try it out and see if you like that style. 

There is another situation where the this reference can make your programs easier to read. Consider a constructor or instance method that calls another instance method on the same object. For example, the CashRegister constructor can call the clear method instead of duplicating its code:
```java
public CashRegister()
{
    clear();
}
// This call is easier to understand when you use the this reference:
public CashRegister()
{
    this.clear();
}
```

It is now more obvious that the method is invoked on the object that is being constructed.

Finally, some people like to use the this reference in constructors. Here is a typical example:
```java
public class Student
{
    private int id;
    private String name;
    
    public Student(int id, String name)
    {
        this.id = id;
        this.name = name;
    }
}
```

The expression id refers to the parameter variable, and this.id to the instance variable. In general, if both a local variable and an instance variable have the same name, you can access the local variable by its name, and the instance variable with the this reference.

You can implement the constructor without using the this reference. Simply choose other names for the parameter variables:

```java
public Student(int anId, String aName)
{
    id = anId;
    name = aName;
}
```

#### Common mistake

Just as it is a common error to forget to initialize a local variable, it is easy to forget about instance variables. Every constructor needs to ensure that all instance variables are set to appropriate values. 

If you do not initialize an instance variable, the Java compiler will initialize it for you. Numbers are initialized with 0, but object references—such as string variables—are set to the null reference.

Of course, 0 is often a convenient default for numbers. However, null is hardly ever a convenient default for objects. Consider this “lazy” constructor for a modified version of the BankAccount class: 

```java
public class BankAccount
{ 
    private double balance; 
    private String owner;  // set to null reference!
    . . . 
    public BankAccount(double initialBalance) 
    { 
        balance = initialBalance; 
        //String owner set to null reference!
    } 
}
```

In this case, balance is initialized, but the owner variable is set to a null reference. This can be a problem—it is illegal to call methods on the null reference. 

To avoid this problem, it is a good idea to initialize every instance variable:

```java
public BankAccount(double initialBalance) 
{ 
    balance = initialBalance; 
    owner = "None";
}
```

#### Calling one constructor from another

Consider the BankAccount class outlined before. It has two constructors: a constructor without arguments to initialize the balance with zero, and another constructor to supply an initial balance. Rather than explicitly setting the balance to zero, one constructor can call another constructor of the same class instead. There is a shorthand notation to achieve this result: 

```java
public class BankAccount
{  
    public BankAccount(double initialBalance) 
    {  
        balance = initialBalance;
    } 
    
    public BankAccount() 
    {  
        this(0);
    } 
    . . . 
}
```

The command this(0); means “Call another constructor of this class and supply the value 0”. Such a call to another constructor can occur only as the first line in a constructor. 

This syntax is a minor convenience. Not used much. Actually, the use of the reserved word ```this``` is a little confusing. Normally, this denotes a reference to the implicit parameter, but if this is followed by parentheses, it denotes a call to another constructor of this class. 


### Static Variables and Methods

Sometimes, a value properly belongs to a class, not to any object of the class. You use a static variable for this purpose. A static variable belongs to the class, not to any object of the class.

```java
public class BankAccount
{ 
    private double balance;
    private int accountNumber;
    private static int lastAssignedNumber = 1000;
    
    public BankAccount()
    {
        lastAssignedNumber++;
        accountNumber = lastAssignedNumber;
    }
    . . .
}  
```

Like instance variables, static variables should always be declared as private to ensure that methods of other classes do not change their values. However, static constants may be either private or public. For example, the BankAccount class can define a public constant value, such as

```java
public class BankAccount
{
    public static final double OVERDRAFT_FEE = 29.95;
    . . .
}
```

Methods from any class can refer to such a constant as ```BankAccount.OVERDRAFT_FEE```. 

Sometimes a class defines methods that are not invoked on an object. Such a method is called a static method. A typical example of a static method is the sqrt method in the Math class. Because numbers aren’t objects, you can’t invoke methods on them. A static method is not invoked on an object.

Making your own static methods for use in other classes:
```java
public class Financial
{
    /**
        Computes a percentage of an amount. 
        @param percentage the percentage to apply
        @param amount the amount to which the percentage is applied
        @return the requested percentage of the amount 
    */
    public static double percentOf(double percentage, double amount)
    { 
        return (percentage / 100) * amount;
    }
}
```

When calling this method, supply the name of the class containing it: 

```java
double tax = Financial.percentOf(taxRate, total);
```

### Patterns for Object Data

Keeping a <ins>total</ins>: an instance variable for the total is updated in methods that increase or decrease the total amount.
Keeping a <ins>counter</ins>: that counts events is incremented in methods that correspond to the events.
			
Keep a counter, such as
```java
private int itemCount;
```
Increment the counter in those methods that correspond to the events that you want to count. 

```java
public void addItem(double price)
{
    totalPrice = totalPrice + price;
    itemCount++;
}
```

You may need to clear the counter, for example at the end of a sale or a statement period. 

```java
public void clear()
{
    total = 0;
    itemCount = 0;
}
```

<ins>Collecting Values</ins>: Some objects collect numbers, strings, or other objects. For example, each multiple-choice question has a number of choices. A cash register may need to store all prices of the current sale. 

Use an array list or an array to store the values. (An array list is usually simpler because you won’t need to track the number of values.) For example,

public class Question

```java
{
    private ArrayList<String> choices;
    . . .

    //In the constructor, initialize the instance variable to an empty collection:
    public Question()
    {
        choices = new ArrayList<String>();
    }

    //You need to supply some mechanism for adding values. It is common to provide a method for appending a value to the collection:
    public void add(String choice)
    {
        choices.add(choice);
    }

    //The user of a Question object can call this method multiple times to add the various choices.
}
```

<ins>Managing Properties of an Object</ins>: A property is a value of an object that an object user can set and retrieve. For example, a Student object may have a name and an ID. Provide an instance variable to store the property’s value and methods to get and set it. An object property can be accessed with a getter method and changed with a setter method.

```java
public class Student
{
    private String name;
    . . .
    public String getName() { return name; }
    public void setName(String newName) { name = newName; }
    . . .

    //It is common to add error checking to the setter method. For example, we may want to reject a blank name:
    public void setName(String newName)
    {
        if (newName.length() > 0) { name = newName; }
    }
} 
```

```java
//Some properties should not change after they have been set in the constructor. 
//For example, a student’s ID may be fixed (unlike the student’s name, which may change).
//In that case, don’t supply a setter method.
public class Student
{
    private int id;
    . . .
    public Student(int anId) { id = anId; }
    public String getId() { return id; }
    // No setId method
    . . .
}
```

<ins>Modeling Objects with Distinct States</ins>: A property is a value of an object that an object user can set and retrieve. For example, a Student object may have a name and an ID. Provide an instance variable to store the property’s value and methods to get and set it. An object property can be accessed with a getter method and changed with a setter method.

Some objects have behavior that varies depending on what has happened in the past. For example, a Fish object may look for food when it is hungry and ignore food after it has eaten. Such an object would need to remember whether it has recently eaten.

Supply an instance variable that models the state, together with some constants for the state values:

```java
public class Fish
{
    private int hungry; 
    
    public static final int NOT_HUNGRY = 0; 
    public static final int SOMEWHAT_HUNGRY = 1; 
    public static final int VERY_HUNGRY = 2;  
    . . .
}
```

Alternatively, can use enumeration. Determine which methods change the state. In this example, a fish that has just eaten food, won’t be hungry. But as the fish moves, it will get hungrier.

```java
public void eat()
{
    hungry = NOT_HUNGRY;
    . . .
}
    
public void move()
{
    . . .
    if (hungry < VERY_HUNGRY) { hungry++; }
}
```

Finally, determine where the state affects behavior. A fish that is very hungry will want to look for food first.
```java
public void move()
{
    if (hungry == VERY_HUNGRY)
    {
        //Look for food.
    }
    . . .
}
```

<ins>Describing the Position of an Object</ins>: To model a moving object, you need to store and update its position.


### Packages

A Java program consists of a collection of classes. So far, most of your programs have consisted of a small number of classes. As programs get larger, however, simply distributing the classes over multiple files isn’t enough. An additional structuring mechanism is needed.

In Java, packages provide this structuring mechanism. A Java <ins>package</ins> is a set of related classes. For example, the Java library consists of several hundred packages, some of which are listed in Table 1. A package is a set of related classes.

![alt text](pics\packages_impt.JPG "Title")

### Organizing Related Classes into Packages

To put one of your classes in a package, you must place a line 

```java
package packageName;
```

as the first instruction in the source file containing the class. A package name consists of one or more identifiers separated by periods. (See Section 8.12.3 of Big Java Late Objects for tips on constructing package names.)

For example, let’s put the Financial class introduced in this chapter into a package named com.horstmann.bigjava. 

The Financial.java file must start as follows: 

```java
package com.horstmann.bigjava;
public class Financial
{
    . . .
}
```

In addition to the named packages (such as java.util or com.horstmann.bigjava), there is a special package, called the default package, which has no name. If you did not include any package statement at the top of your source file, its classes are placed in the default package. 

### Importing Packages

If you want to use a class from a package, you can refer to it by its full name (package name plus class name). For example, java.util.Scanner refers to the Scanner class in the java.util package: 

```java
java.util.Scanner in = new java.util.Scanner(System.in);
```

Naturally, that is somewhat inconvenient. For that reason, you usually import a name with an import statement: 

```java
import java.util.Scanner;
```

Then you can refer to the class as Scanner without the package prefix.

You can import all classes of a package with an import statement that ends in .*. For example, you can use the statement 

```java
import java.util.*;
```

to import all classes from the java.util package. That statement lets you refer to classes like Scanner or Random without a java.util prefix. The import directive lets you refer to a class of a package by its class name, without the package prefix.

However, you never need to import the classes in the java.lang package explicitly. That is the package containing the most basic Java classes, such as Math and Object. These classes are always available to you. In effect, an automatic import java.lang.*; statement has been placed into every source file. 

Finally, you don’t need to import other classes in the same package. For example, when you implement the class homework1.Tester, you don’t need to import the class homework1.Bank. The compiler will find the Bank class without an import statement because it is located in the same package, homework1.

### Packages Names

Placing related classes into a package is clearly a convenient mechanism to organize classes. However, there is a more important reason for packages: to avoid name clashes.

In a large project, it is inevitable that two people will come up with the same name for the same concept. This even happens in the standard Java class library (which has now grown to thousands of classes). There is a class Timer in the java.util package and another class called Timer in the javax.swing package. You can still tell the Java compiler exactly which Timer class you need, simply by referring to them as java.util.Timer and javax.swing.Timer. 

Of course, for the package-naming convention to work, there must be some way to ensure that package names are unique. It wouldn’t be good if the car maker BMW placed all its Java code into the package bmw, and some other programmer (perhaps Britney M. Walters) had the same bright idea. To avoid this problem, the inventors of Java recommend that you use a package-naming scheme that takes advantage of the uniqueness of Internet domain names. 
			
Use a domain name in reverse to construct an unambiguous package name.
			
For example, if I have a domain name horstmann.com, and there is nobody else on the planet with the same domain name. (I was lucky that the domain name horstmann.com had not been taken by anyone else when I applied. If your name is Walters, you will sadly find that someone else beat you to walters.com.) To get a package name, turn the domain name around to produce a package name prefix, such as com.horstmann.

If you don’t have your own domain name, you can still create a package name that has a high probability of being unique by writing your e-mail address backwards. For example, if Britney Walters has an e-mail address walters@cs.sjsu.edu, then she can use a package name edu.sjsu.cs.walters for her own classes. 

### Packages and Source Files

A source file must be located in a subdirectory that matches the package name. The parts of the name between periods represent successively nested directories. For example, the source files for classes in the package com.horstmann.bigjava would be placed in a subdirectory com/horstmann/bigjava. You place the subdirectory inside the base directory holding your program’s files. For example, if you do your homework assignment in a directory /home/britney/hw8/problem1, then you can place the class files for the com.horstmann.bigjava package into the directory /home/britney/hw8/problem1/com/horstmann/bigjava, as shown in Figure 15. (Here, we are using UNIX-style file names. Under Windows, you might use c:\Users\Britney\hw8\problem1\com\horstmann\bigjava.)

The path of a class file must match its package name.

![alt text](pics\pckg_dir.JPG "Title")

#### Common Error / Package Access

CONFUSING DOTS

In Java, the dot symbol ( . ) is used as a separator in the following situations: 
•Between package names (java.util) 
•Between package and class names (homework1.Bank) 
•Between class and inner class names (Ellipse2D.Double) 
•Between class and instance variable names (Math.PI) 
•Between objects and methods (account.getBalance()) 

When you see a long chain of dot-separated names, it can be a challenge to find out which part is the package name, which part is the class name, which part is an instance variable name, and which part is a method name. Consider 

```java
java.lang.System.out.println(x);
```

Because ```println``` is followed by an opening parenthesis, it must be a method name. Therefore, ```out``` must be either an object or a class with a static ```println``` method. (Of course, we know that ```out``` is an object reference of type ```PrintStream```.) Again, it is not at all clear, without context, whether ```System``` is another object, with a public variable ```out```, or a class with a static variable. Judging from the number of pages that the Java language specification devotes to this issue, even the compiler has trouble interpreting these dot-separated sequences of strings.

To avoid problems, it is helpful to adopt a strict coding style. If class names always start with an uppercase letter, and variable, method, and package names always start with a lowercase letter, then confusion can be avoided. 

PACKAGE ACCESS

If a class, instance variable, or method has no public or private modifier, then all methods of classes in the same package can access the feature. For example, if a class is declared as public, then all other classes in all packages can use it. But if a class is declared without an access modifier, then only the other classes in the same package can use it. Package access is a reasonable default for classes, but it is extremely unfortunate for instance variables.

It is a common error to forget the reserved word private, thereby opening up a potential security hole. For example, at the time of this writing, the Window class in the java.awt package contained the following declaration: 

```java
public class Window extends Container
{  
    String warningString;
    . . .
}
```
		
There actually was no good reason to grant package access to the warningString instance variable—no other class accesses it. 
Package access for instance variables is rarely useful and always a potential security risk. Most instance variables are given package access by accident because the programmer simply forgot the private reserved word. It is a good idea to get into the habit of scanning your instance variable declarations for missing private modifiers.

An instance variable or method that is not declared as public or private can be accessed by all classes in the same package, which is usually not desirable.

### Summary
Understand the concepts of classes, objects, and encapsulation.  

•A class describes a set of objects with the same behavior.
•Every class has a public interface: a collection of methods through which the objects of the class can be manipulated. 
•Encapsulation is the act of providing a public interface and hiding the implementation details.
•Encapsulation enables changes in the implementation without affecting users of a class.

Understand instance variables and method implementations of a simple class.

•The methods of a class define the behavior of its objects. 
•An object’s instance variables represent the state of the object.
•Each object of a class has its own set of instance variables.
•An instance method can access the instance variables of the object on which it acts.
•A private instance variable can only be accessed by the methods of its own class.

Write method headers that describe the public interface of a class.

•You can use method headers and method comments to specify the public interface of a class.
•A mutator method changes the object on which it operates.
•An accessor method does not change the object on which it operates.

Choose an appropriate data representation for a class.

•Each accessor method must either retrieve a stored value or compute the result.
•Commonly, there is more than one way of representing the data of an object, and you must make a choice.
•Be sure that your data representation supports method calls in any order.

Provide the implementation of instance methods for a class.

•The object on which an instance method is applied is the implicit parameter.
•Explicit parameters of a method are listed in the method declaration.

Design and implement constructors.

•A constructor initializes the instance variables of an object. 
•A constructor is invoked when an object is created with the new operator.
•The name of a constructor is the same as the class name.
•A class can have multiple constructors.
•The compiler picks the constructor that matches the construction arguments.
•By default, numbers are initialized as 0, Booleans as false, and object references as null.
•If you do not provide a constructor, a constructor with no arguments is generated.

Write tests that verify that a class works correctly.

•A unit test verifies that a class works correctly in isolation, outside a complete program.
•To test a class, use an environment for interactive testing, or write a tester class to execute test instructions.
•Determining the expected result in advance is an important part of testing.

Use the technique of object tracing for visualizing object behavior.

•Write the methods on the front of a card, and the instance variables on the back.
•Update the values of the instance variables when a mutator method is called.

Describe the behavior of object references.

•An object reference specifies the location of an object.
•Multiple object variables can contain references to the same object.
•Primitive type variables store values. Object variables store references.
•When copying an object reference, you have two references to the same object.
•The null reference refers to no object.
•In a method, the this reference refers to the implicit parameter.

Understand the behavior of static variables and methods.

•A static variable belongs to the class, not to any object of the class.
•A static method is not invoked on an object.

Use patterns to design the data representation of a class.  

•An instance variable for the total is updated in methods that increase or decrease the total amount.
•A counter that counts events is incremented in methods that correspond to the events.
•An object can collect other objects in an array or array list.
•An object property can be accessed with a getter method and changed with a setter method.
•If your object can have one of several states that affect the behavior, supply an instance variable for the current state.
•To model a moving object, you need to store and update its position.

Use packages to organize sets of related classes.

•A package is a set of related classes.
•The import directive lets you refer to a class of a package by its class name, without the package prefix.
•Use a domain name in reverse to construct an unambiguous package name.
•The path of a class file must match its package name.
•An instance variable or method that is not declared as public or private can be accessed by all classes in the same package, which is usually not desirable.

## Inheritence

Intellij
crtl-H: shows heirarchy of object
shift-alt-U: on package, shows relationship among packages

### Abstract class

can't be instantiated. meant to be inherented by concerete sub-classes.

A class must be defined as abstract as soon as an abstract method is added. Abstract method is a method that subclasses must define.

### final class

This disallows other developers from extending this class

```java
public final class Executive extends Manager {
    // stuff
}
```

### super keyowrd

Abstract class have constructors, which is strange at first.

Calling ```super()``` in a constructor calls the super class

```java
public Person(String name) {
    super();
    mName = name;
}

public Student(String name, String major) {
    super(name);
    mMajor = major;
}
```

```java
Student student = new Student("Adam","CS")
student.getName()   // note Student does not have a getName() method! It's super class does.
```

Note, calling ```super()``` in Student does not instantiate a Person object.

### Every reference is an aperture

```java
Object obj = new Double(5.87);
```

Instiating an object called obj. Points to the Double object. Now, obj has available to it all the Object methods. This works because Double extends Object in its heirarchy tree. So, a Double object can behave like an Object if so desired. Thus, references are apertures of objects.

We can instantiate other Object types in the heirarchy tree for Double:

```java
Object obj = new Double(5.87);      // a few available methods
Number num = (Number) obj;          // more available methods
Double dub = (Double) num;          // most available methods
// all 3 references point to different "views" of the same object

// if you were to print out the following you will all get Double
obj.getClass().getCanonicalName() // double
num.getClass().getCanonicalName() // double
dub.getClass().getCanonicalName() // double
```

You cannot instantiate a Double (subclass) reference that points to a super class object
because the Double (sublcass) contains way more information than the super class object
contains

```java
// what happens here?
Double dub = new Object();  // VIOLATES. ERROR 
```

Instiating an object with no reference:
```java
new Double(5.87);      
System.out.println(new Double (5.87))
```

### Upcasting / Downcasting

```java
Double dub = new Double(43.43)

// narrow aperture
Object obj = dub; // points to same object

// don't even need to epxlicitly cast
// Object obj = (Object) dub;

// widen the aperture. more risky.
// downcast. requires an explicit cast
Number num = (Number) obj;
```

Why is a downcast potentially dangerous? Well, you because 
```java
obj = new Rectangle(1,2,5,6); // extends object. Number does too
number num = (Number) obj;    // error! Class cast exception
```

### Overriding

Overriding methods are those with the same signature of a method in the class' hierarchy.
If you extend an abstract class, you must override methods (same with implementing
interfaces). Important for polymorphism.

```@Overide``` is optional notation. It tells the compiler to check the signature and verify
the overloading.

Useful to look at object references and classes in a freemason pyramid drawing.
looking for a method proceeds like so:

(1) start at the lowest-level of the substructure, if it's implemented there, then
call it.

(2) If not, crawl up the hierarchy until it's implemented.

![alt text](pics\aperture.JPG "Title")

### Overloading methods

We talked about overloading of constructors.
Overloading is helpful for constructors, but also certain methods

Keep in mind when overloading the method: the return type is not sufficient to differentiate overloaded methods. Instead, it is the explicit parameters (formal parameters) of the methods that are used to differentiate the method. In other words, all methods with the same method name need to have different formal parameters.

Tip, can check instance of an object like so

```java

public String greetOther(Employee employee, boolean shout) {

    if (shout) {
        if (employee instanceof Executive) {
            return (greetOther((Executive) employee)).toUpperCase();
        } else {
            String strType = employee.getClass().getSimpleName();
            return ("You are just a " + strType + ", leave me alone").toUpperCase();
        } 
    } else {
        return greetOther(employee)
    }
}

public String greetOther(Employee employee) {

    if (employee instanceof Executive) {
        return greetOther((Executive) employee);
    } else {
        String strType = employee.getClass().getSimpleName();
        return "You are just a " + strType + ", leave me alone";
    }

}

// Note! we can make this method below private!
private String greetOther(Executive other) {
    // do stuff
}
```

### Interfaces

A class implements an interface rather than extends it. They are essentially contracts. Any class that implements the interface must override all the interface methods with its own methods.

Interface names often end with "able" to imply that they add to the capability of the class. An interface is a contract; it defines the methods.

```java
public interface Singable {
    String sing();  //optional to precede declaration with public abstract 
    String dance(); //optional to precede declaration with public abstract 
}
```

Interfaces only define functionality, they do not implement it. Abstract classes allow you to create functionality that subclasses can implement or override.

A class can extend only one abstract class, but it can take advantage of multiple interfaces.

## Implementation Inheritance 

### Inheritance Hierarchies

n object-oriented design, inheritance is a relationship between a more general class (called the superclass) and a more specialized class (called the subclass). The subclass inherits data and behavior from the superclass. For example, BMW might be subclass of Car. A subclass inherits data and behavior from a superclass.

For example, consider a method that takes an argument of type Vehicle:
```java
void processVehicle(Vehicle v)
```

Because Car is a subclass of Vehicle, you can call that method with a Car object:

```java
Car myCar = new Car(. . .);
processVehicle(myCar);
```

Why provide a method that processes Vehicle objects instead of Car objects? That method is more useful because it can handle any kind of vehicle (including Truck and Motorcycle objects). In general, when we group classes into an inheritance hierarchy, we can share common code among the classes. 

TIP: Use a Single Class for Variation in Values, Inheritance for Variation in Behavior

The purpose of inheritance is to model objects with different behavior. When people first learn about inheritance, they have a tendency to overuse it, by creating multiple classes even though the variation could be expressed with a simple instance variable. 

Consider a program that tracks the fuel efficiency of a fleet of cars by logging the distance traveled and the refueling amounts. Some cars in the fleet are hybrids. Should you create a subclass HybridCar? Not in this application. Hybrids don’t behave any differently than other cars when it comes to driving and refueling. They just have a better fuel efficiency. A single Car class with an instance variable 
```java
double milesPerGallon;
```
is entirely sufficient. 

However, if you write a program that shows how to repair different kinds of vehicles, then it makes sense to have a separate class HybridCar. When it comes to repairs, hybrid cars behave differently from other cars

### Implementing Subclasses

In Java, you form a subclass by specifying what makes the subclass different from its superclass. Subclass objects automatically have the instance variables that are declared in the superclass. You only declare instance variables that are not part of the superclass objects. 

```A subclass inherits all methods that it does not override.```

The subclass inherits all public methods from the superclass. You declare any methods that are new to the subclass, and change the implementation of inherited methods if the inherited behavior is not appropriate. When you supply a new implementation for an inherited method, you **override** the method. 

```A subclass can override a superclass method by providing a new implementation.```

```The extends reserved word indicates that a class inherits from a superclass.```

e.g.
```java
public class ChoiceQuestion extends Question
{
    // This instance variable is added to the subclass
    private ArrayList<String> choices;
    
    // This method is added to the subclass
    public void addChoice(String choice, boolean correct) { . . . }
    
    // This method overrides a method from the superclass
    public void display() { . . . }
}
```

**COMMON ERROR**: A subclass has no access to the private instance variables of the superclass. 

```java
public ChoiceQuestion(String questionText)
{
    text = questionText; // Error—tries to access private superclass variable
}
```

When faced with a compiler error, beginners commonly “solve” this issue by adding another instance variable with the same name to the subclass:

```java
public class ChoiceQuestion extends Question
{

    private ArrayList<String> choices;
    private String text; // Don’t!
    . . .
}
```

Sure, now the constructor compiles, but it doesn’t set the correct text! Such a ChoiceQuestion object has two instance variables, both named text. The constructor sets one of them, and the display method displays the other. 


### Overriding Methods

The subclass inherits the methods from the superclass. If you are not satisfied with the behavior of an inherited method, you override it by specifying a new implementation in the subclass. 

```An overriding method can extend or replace the functionality of the superclass method.```

```Use the reserved word super to call a superclass method.```

```java
public void display() 
{
    // Display the question text
    super.display(); // OK
    // Display the answer choices
    . . .
}
```


e.g.
```java

/**
   A question with a text and an answer.
*/
public class Question
{
   private String text;
   private String answer;

   /**
      Constructs a question with empty question and answer.
   */
   public Question() 
   {
      text = "";
      answer = "";
   }

   /**
      Sets the question text.
      @param questionText the text of this question
   */
   public void setText(String questionText)   
   {
      text = questionText;
   }

   /**
      Sets the answer for this question.
      @param correctResponse the answer
   */
   public void setAnswer(String correctResponse)
   {
      answer = correctResponse;
   }

   /**
      Checks a given response for correctness.
      @param response the response to check
      @return true if the response was correct, false otherwise
   */
   public boolean checkAnswer(String response)
   {
      return response.equals(answer);
   }

   /**
      Displays this question.
   */
   public void display()
   {
      System.out.println(text);
   }
}
```


**COMMON ERROR** ACCIDENTAL OVERLOADING

In Java, two methods can have the same name, provided they differ in their parameter types. For example, the PrintStream class has methods called println with headers

```java
void println(int x)
```
and
```java
void println(String x)
```

These are different methods, each with its own implementation. The Java compiler considers them to be completely unrelated. We say that the println name is **overloaded**. This is different from overriding, where a subclass method provides an implementation of a method whose parameter variables have the same types.

If you mean to override a method but use a parameter variable with a different type, then you accidentally introduce an overloaded method. For example,
```java
public class ChoiceQuestion extends Question
{
    . . .
    public void display(PrintStream out) 
    // Does not override void display()
    {
        . . . 
    }
}
```

The compiler will not complain. It thinks that you want to provide a method just for PrintStream arguments, while inheriting another method void display(). When overriding a method, be sure to check that the types of the parameter variables match exactly.

#### Calling the Superclass Constructor

Consider the process of constructing a subclass object. A subclass constructor can only initialize the instance variables of the subclass. But the superclass instance variables also need to be initialized. 
			
Unless specified otherwise, the subclass constructor calls the superclass constructor with no arguments.

Unless you specify otherwise, the superclass instance variables are initialized with the constructor of the superclass that has no arguments.

To call a superclass constructor, use the ```super``` reserved word in the first statement of the subclass constructor.

In order to specify another constructor, you use the super reserved word, together with the arguments of the superclass constructor, as the first statement of the subclass constructor.

For example, suppose the Question superclass had a constructor for setting the question text. Here is how a subclass constructor could call that superclass constructor:

```java
public ChoiceQuestion(String questionText)
{
    super(questionText);
    choices = new ArrayList<String>();
} 
```

The constructor of a subclass can pass arguments to a superclass constructor, using the reserved word super. 

However, if all superclass constructors have arguments, you must use the super syntax and provide the arguments for a superclass constructor.

When the reserved word super is followed by a parenthesis, it indicates a call to the superclass constructor. When used in this way, the constructor call must be the first statement of the subclass constructor. If super is followed by a period and a method name, on the other hand, it indicates a call to a superclass method, as you saw in the preceding section. Such a call can be made anywhere in any subclass method. 

### Polymorphism

In Java, method calls are always determined by the type of the actual object, not the type of the variable containing the object reference. This is called **dynamic method lookup**. 
			
Dynamic method lookup allows us to treat objects of different classes in a uniform way. This feature is called **polymorphism**. We ask multiple objects to carry out a task, and each object does so in its own way.

Polymorphism makes programs easily extensible. Suppose we want to have a new kind of question for calculations, where we are willing to accept an approximate answer. All we need to do is to declare a new class NumericQuestion that extends Question, with its own checkAnswer method. Then we can call the presentQuestion method with a mixture of plain questions, choice questions, and numeric questions. The presentQuestion method need not be changed at all! Thanks to dynamic method lookup, method calls to the display and checkAnswer methods automatically select the correct method of the newly declared classes.

```Polymorphism (“having multiple shapes”) allows us to manipulate objects that share a set of tasks, even though the tasks are executed in different ways. ```

### Abstract Classes

When you extend an existing class, you have the choice whether or not to override the methods of the superclass. Sometimes, it is desirable to force programmers to override a method. That happens when there is no good default for the superclass, and only the subclass programmer can know how to implement the method properly. An **abstract method** is the solution.

```java
public abstract void deductFees();
```

```An abstract method is a method whose implementation is not specified.```

An **abstract method** has no implementation. This forces the implementors of subclasses to specify concrete implementations of this method. (Of course, some subclasses might decide to implement a do-nothing method, but then that is their choice—not a silently inherited default.)

You cannot construct objects of classes with abstract methods. For example, once the Account class has an abstract method, the compiler will flag an attempt to create a new Account() as an error. 
			
A class for which you cannot create objects is called an **abstract class**. A class for which you can create objects is sometimes called a **concrete class**. 

```An abstract class is a class that cannot be instantiated.```

In Java, you must declare all abstract classes with the reserved word abstract: 
```java
public abstract class Account
{ 
    public abstract void deductFees();
    . . .
}
    
public class SavingsAccount extends Account // Not abstract
{
    . . .
    public void deductFees() // Provides an implementation
    {
        . . .
    }
}
```


#### Final Methods and Classes

Above, we showed how to force other programmers to create subclasses of abstract classes and override abstract methods. Occasionally, you may want to do the opposite and prevent other programmers from creating subclasses or from overriding certain methods. In these situations, you use the ```final``` reserved word. For example, the String class in the standard Java library has been declared as 

```java
public final class String { . . . }
```

That means that nobody can extend the String class. When you have a reference of type String, it must contain a String object, never an object of a subclass. You can also declare individual methods as final: 

```java
public class SecureAccount extends BankAccount
{ 
    . . .
    public final boolean checkPassword(String password)
    { 
        . . .
    }
}
```

This way, nobody can override the checkPassword method with another method that simply returns true. 

#### Protected Access

We ran into a hurdle when trying to implement the display method of the ChoiceQuestion class. That method wanted to access the instance variable text of the superclass. Our remedy was to use the appropriate method of the superclass to display the text. 

Java offers another solution to this problem. The superclass can declare an instance variable as protected: 

```java
public class Question
{ 
    protected String text;
    . . .
}
```

Protected data in an object can be accessed by the methods of the object’s class and all its subclasses. 

Protected means that a subclass from another package cannot access protected members of arbitrary instances of their superclasses. They can only access them on instances of their own type (where type is a compile-time type of expression, since it's a compile-time check).

For example, ChoiceQuestion inherits from Question, so its methods can access the protected instance variables of the Question superclass. 

Some programmers like the protected access feature because it seems to strike a balance between absolute protection (making instance variables private) and no protection at all (making instance variables public). However, experience has shown that protected instance variables are subject to the same kinds of problems as public instance variables. The designer of the superclass has no control over the authors of subclasses. Any of the subclass methods can corrupt the superclass data. Furthermore, classes with protected variables are hard to modify. Even if the author of the superclass would like to change the data implementation, the protected variables cannot be changed, because someone somewhere out there might have written a subclass whose code depends on them. 

In Java, protected variables have another drawback—they are accessible not just by subclasses, but also by other classes in the same package.

It is best to leave all data private. If you want to grant access to the data to subclass methods only, consider making the accessor method protected. 



It's probably best to avoid use of the protected keyword, erring on the side of using the private keyword instead.

### Object: the cosmic superclass

In Java, every class that is declared without an explicit ```extends``` clause automatically extends the class ```Object```. That is, the class ```Object``` is the direct or indirect superclass of every class in Java. The ```Object``` class defines several very general methods, including

```toString```, which yields a string describing the object\
```equals```, which compares objects with each other\
```hashCode```, which yields a numerical code for storing the object in a set

#### Overriding the ```toString``` Method

The ```toString``` method returns a string representation for each object. It is often used for debugging. The ```toString``` method is called automatically whenever you concatenate a string with an object. On one side of the + concatenation operator is a string, but on the other side is an object reference. The Java compiler automatically invokes the toString method to turn the object into a string. Then both strings are concatenated.

interesting example
```java
BankAccount momsSavings = new BankAccount(5000);
String s = momsSavings.toString(); // Sets s to something like "BankAccount@d24606bf"
```

That’s disappointing—all that’s printed is the name of the class, followed by the hash code, a seemingly random code. The **hash code** can be used to tell objects apart—different objects are likely to have different hash codes.

We don’t care about the hash code. We want to know what is inside the object. But, of course, the toString method of the Object class does not know what is inside the BankAccount class. Therefore, we have to override the method and supply our own version in the BankAccount class. We’ll follow the same format that the toString method of the Rectangle class uses: first print the name of the class, and then the values of the instance variables inside brackets. 

```java
public class BankAccount
{ 
    . . .
    public String toString()
    { 
        return "BankAccount[balance=" + balance + "]";
    }
}
```

This works better: 

```java
BankAccount momsSavings = new BankAccount(5000);
String s = momsSavings.toString(); // Sets s to "BankAccount[balance=5000]"
```

#### ```equals``` method

In addition to the toString method, the Object class also provides an equals method, whose purpose is to check whether two objects have the same contents: 

```java
if (stamp1.equals(stamp2))   // Contents are the same
``` 

```The equals method checks whether two objects have the same contents.```

Note! This is different from:
```java
if (stamp1 == stamp2) . . .    // Objects are the same—see Figure 10 
```

Let’s implement the equals method for a Stamp class. We need to override the equals method of the Object class: 
			
```java			
public class Stamp
{ 
    private String color;
    private int value;
    . . .
    public boolean equals(Object otherObject)
    { 
        . . .
    }
    . . .
}
```

Now we have a slight problem. The Object class knows nothing about stamps, so it declares the otherObject parameter variable of the equals method to have the type Object. When overriding the method, you are not allowed to change the type of the parameter variable. Cast the parameter variable to the class Stamp: 

```java
			Stamp other = (Stamp) otherObject;
```

Then you can compare the two stamps:

```java
public boolean equals(Object otherObject)
{ 
    Stamp other = (Stamp) otherObject;
    return color.equals(other.color) 
            && value == other.value; 
}
```

Note that this equals method can access the instance variables of any Stamp object: the access other.color is perfectly legal.


#### ```instanceof``` Operator

As discussed before, it is legal to store a subclass reference in a superclass variable:

```java
ChoiceQuestion cq = new ChoiceQuestion();
Question q = cq; // OK
Object obj = cq; // OK
```

Very occasionally, you need to carry out the opposite conversion, from a superclass reference to a subclass reference. If you know that an object belongs to a given class, use a cast to convert the type.

For example, you may have a variable of type Object, and you happen to know that it actually holds a Question reference. In that case, you can use a cast to convert the type:

```java
Question q = (Question) obj;
```

```If you know that an object belongs to a given class, use a cast to convert the type.```

However, this cast is somewhat dangerous. If you are wrong, and obj actually refers to an object of an unrelated type, then a “class cast” exception is thrown. To protect against bad casts, you can use the instanceof operator. It tests whether an object belongs to a particular type. For example, 

```java
obj instanceof Question 
```

```The instanceof operator tests whether an object belongs to a particular type.```

```instanceof``` returns true if the type of ```obj``` is convertible to ```Question```. This happens if ```obj``` refers to an actual Question or to a subclass such as ChoiceQuestion. Using the ```instanceof``` operator, a safe cast can be programmed as follows: 
```java
if (obj instanceof Question)
{
    Question q = (Question) obj;
}
```

Note that ```instanceof``` is not a method. It is an operator, just like + or <. However, it does not operate on numbers. To the left is an object, and to the right a type name.

Do not use the instanceof operator to bypass polymorphism: 

```java
if (q instanceof ChoiceQuestion) // Don’t do this—see Common Error 9.5
{
    // Do the task the ChoiceQuestion way
}
else if (q instanceof Question)
{
    // Do the task the Question way
}
```
In this case, you should implement a method doTheTask in the Question class, override it in ChoiceQuestion, and call

```java
q.doTheTask();
```

**COMMON ERROR**: Some programmers use specific type tests in order to implement behavior that varies with each class:

```java
if (q instanceof ChoiceQuestion) // Don’t do this
{
    // Do the task the ChoiceQuestion way
}
else if (q instanceof Question)
{
    // Do the task the Question way
}
```

This is a poor strategy. If a new class such as NumericQuestion is added, then you need to revise all parts of your program that make a type test, adding another case:

```java
else if (q instanceof NumericQuestion)
{
    // Do the task the NumericQuestion way
}
```

In contrast, consider the addition of a class NumericQuestion to our quiz program. Nothing needs to change in that program because it uses polymorphism, not type tests. Whenever you find yourself trying to use type tests in a hierarchy of classes, reconsider and use polymorphism instead. Declare a method doTheTask in the superclass, override it in the subclasses, and call

```java
q.doTheTask();
```

**Inheritance and the ```toSring``` method**

You just saw how to write a toString method: Form a string consisting of the class name and the names and values of the instance variables. However, if you want your toString method to be usable by subclasses of your class, you need to work a bit harder. Instead of hardcoding the class name, call the getClass method (which every class inherits from the Object class) to obtain an object that describes a class and its properties. Then invoke the getName method to get the name of the class:

```java
public String toString()
{ 
    return getClass().getName() + "[balance=" + balance + "]";
}
```

Then the toString method prints the correct class name when you apply it to a subclass, say a SavingsAccount. 

```java			
SavingsAccount momsSavings = . . . ;
System.out.println(momsSavings);
// Prints "SavingsAccount[balance=10000]"
```

Of course, in the subclass, you should override toString and add the values of the subclass instance variables. Note that you must call super.toString to get the instance variables of the superclass—the subclass can’t access them directly. 

```java
public class SavingsAccount extends BankAccount
{
    . . .
    public String toString()
    { 
        return super.toString() + "[interestRate=" + interestRate + "]";
    }
}
```

Now a savings account is converted to a string such as ```SavingsAccount[balance= 10000][interestRate=5]```. The brackets show which variables belong to the superclass.

**Inheritance and the equals Method**

You just saw how to write an equals method: Cast the otherObject parameter variable to the type of your class, and then compare the instance variables of the implicit parameter and the explicit parameter.

But what if someone called stamp1.equals(x) where x wasn’t a Stamp object? Then the bad cast would generate an exception. It is a good idea to test whether otherObject really is an instance of the Stamp class. The easiest test would be with the instanceof operator. However, that test is not specific enough. It would be possible for otherObject to belong to some subclass of Stamp. To rule out that possibility, you should test whether the two objects belong to the same class. If not, return false.

```java
if (getClass() != otherObject.getClass()) { return false; }
```

Moreover, the Java language specification demands that the equals method return false when otherObject is null.
Here is an improved version of the equals method that takes these two points into account:

```java
public boolean equals(Object otherObject)
{
    if (otherObject == null) { return false; }
    if (getClass() != otherObject.getClass()) { return false; }
    Stamp other = (Stamp) otherObject;
    return color.equals(other.color) && value == other.value;
}
```

When you implement equals in a subclass, you should first call equals in the superclass to check whether the superclass instance variables match. Here is an example:

```java
public CollectibleStamp extends Stamp
{
    private int year;
    . . .
    public boolean equals(Object otherObject)
    {
        if (!super.equals(otherObject)) { return false; }
        CollectibleStamp other = (CollectibleStamp) otherObject;
        return year == other.year;
    }
}
```

### Interface Types

It is often possible to design a general and reusable mechanism for processing objects by focusing on the essential operations that an algorithm needs. You use interface types to express these operations.

Consider the following method that computes the average balance in an array of BankAccount objects:

```java
			public static double average(BankAccount[] objects)
			{
			   if (objects.length == 0) { return 0; }
			   double sum = 0;
			   for (BankAccount obj : objects)
			   {
			      sum = sum + obj.getBalance();
			   }
			   return sum / objects.length;
			}
```

Now suppose you have an array of Country objects and want to determine the average of the areas: 
```java
public static double average(Country[] objects)
{
    if (objects.length == 0) { return 0; }
    double sum = 0;
    for (Country obj : objects)
    {
        sum = sum + obj.getArea();
    }
    return sum / objects.length;
}
```

Clearly, the algorithm for computing the result is the same in both cases, but the details of measurement differ. How can we write a single method that computes the averages of both bank accounts and countries?
			
Suppose that the classes agree on a single method getMeasure that obtains the measure to be used in the data analysis. For bank accounts, getMeasure returns the balance. For countries, getMeasure returns the area. Other classes can participate too, provided that their getMeasure method returns an appropriate value. Then we can implement a single method that computes

```java
sum = sum + obj.getMeasure();
```

What is the type of the variable obj? Any class that has a getMeasure method. 

In Java, an **interface type** is used to specify required operations. We will declare an interface type that we call Measurable: 

```java
public interface Measurable
{
    double getMeasure();
}
```

The interface declaration lists all methods that the interface type requires. The Measurable interface type requires a single method, but in general, an interface type can require multiple methods.
			
Unlike a class, an interface type provides no implementation.
			
An interface type is similar to a class, but there are several important differences: 

```
•Methods in an interface type must be abstract (that is, without an implementation) or, as of Java 8, static or default methods
•All methods in an interface type are automatically public.
•An interface type cannot have instance variables.
•An interface type cannot have static methods.
```

**SYNTAX: Interface Types**

We can use the interface type Measurable to implement a “universal” method for computing averages:

```java
public static double average(Measurable[] objects)
{
    if (objects.length == 0) { return 0; }
    double sum = 0;
    for (Measurable obj : objects)
    {
        sum = sum + obj.getMeasure();
    }
    return sum / objects.length;
}
```

```By using an interface type for a parameter variable, a method can accept objects from many classes.```

### Implementing an Interface

The **implements** reserved word indicates which interfaces a class implements.

e.g.
```java
public class BankAccount implements Measurable 
{ 
    public double getMeasure()
    {
        return balance;
    }
    . . .
}

public class Country implements Measurable 
{ 
    public double getMeasure()
    {
        return area;
    }
    . . .
}
```

### The Comparable Interface

Implement the ```Comparable``` interface so that objects of your class can be compared, for example, in a sort method.

```java
public class BankAccount implements Comparable
{
    . . .
    public int compareTo(Object otherObject)
    {
        BankAccount other = (BankAccount) otherObject;
        if (balance < other.balance) { return -1; }
        if (balance > other.balance) { return 1; }
        return 0;
    }
    . . .
}
```

**COMMON ERROR: Forgetting to Declare Implementing Methods as Public**: 
The methods in an interface are not declared as public, because they are public by default. However, the methods in a class are not public by default. It is a common error to forget the public reserved word when declaring a method from an interface:

```java
public class BankAccount implements Measurable 
{ 
    double getMeasure() // Oops—should be public 
    {
        return balance;
    }
    . . .
}
```

Then the compiler complains that the method has a weaker access level, namely package access instead of public access. The remedy is to declare the method as public.

**Comparing Integers and Floating-Point Numbers**

When you implement a comparison method, you need to return a negative integer to indicate that the first object should come before the other, zero if they are equal, or a positive integer otherwise. You have seen how to implement this decision with three branches. When you compare nonnegative integers, there is a simpler way: subtract the integers:

```java
public class Person implements Comparable 
{ 
    private int id; // Must be ≥ 0
    . . . 
    public int compareTo(Object otherObject) 
    { 
        Person other = (Person) otherObject; 
        return id - other.id; 
    } 
}
```

The difference is negative if id < other.id, zero if the values are the same, and positive otherwise.
			
This trick doesn’t work if the integers can be negative because the difference can overflow (see Exercise •• R9.15). However, the Integer.
compare method always works:

```java
return Integer.compare(id, other.id); // Safe for negative integers 
```

You cannot compare floating-point values by subtraction (see Exercise •• R9.16). Instead, use the Double.compare method:

```java
public class BankAccount implements Comparable 
{ 
    . . . 
    public int compareTo(Object otherObject) 
    { 
        BankAccount other = (BankAccount) otherObject; 
        return Double.compare(balance, other.balance); 
    } 
}
```

#### Constants in Interfaces**

Interfaces cannot have instance variables, but it is legal to specify constants. 

When declaring a constant in an interface, you can (and should) omit the reserved words public static final, because all variables in an interface are automatically public static final. For example, 

```java
public interface Measurable
{ 
    double OUNCES_PER_LITER = 33.814;
    . . .

}
```

To use this constant in programs, add the interface name: 

```java
Measurable.OUNCES_PER_LITER
```

**Generic Interface Types**

```java
public interface Comparable<T> 
			{
			   int compareTo(T other) 
			}
```

The type parameter specifies the type of the objects that this class is willing to accept for comparison. Usually, this type is the same as the class type itself. For example, the BankAccount class would implement Comparable<BankAccount>, like this:

```java
public class BankAccount implements Comparable<BankAccount> 
{ 
    . . . 
    public int compareTo(BankAccount other) 
    { 
        return Double.compare(balance, other.balance); 
    } 
}
```
			
The type parameter has a significant advantage: You need not use a cast to convert an Object parameter variable into the desired type.

Similarly, the Measurer interface can be improved by making it into a generic type:

```java
public interface Measurer<T>
{
    double measure(T anObject);
}
```

The type parameter specifies the type of the parameter of the measure method. Again, you avoid the cast from Object when implementing the interface:

```java
public class AreaMeasurer implements Measurer<Rectangle>
{
    public double measure(Rectangle anObject)
    {
        double area = anObject.getWidth() * anObject.getHeight();
        return area;
    }
}
```

#### Static Methods in Interfaces

Before Java 8, all methods in an interface had to be abstract. Java 8 allows static methods in interfaces that work exactly like static methods in classes. A static method of an interface does not operate on objects, and its purpose should relate to the interface that contains it.

For example, it would be perfectly sensible to place the average method from Section 9.6.1 into the Measurable interface:

```java
public interface Measurable 
{ 
    double getMeasure();  // An abstract method 
    static double average(Measurable[] objects) // A static method 
    { 
        . . . // Same implementation as in Section 9.6.1
    } 
}
```

To call this method, provide the name of of the interface and the method name:

```java
double meanArea = Measurable.average(countries);
```

Here is a full-fledged example of this implementation
```java
/**
   This program demonstrates a static method of the
   Measurable interface.
*/
public class MeasurableTester
{
   public static void main(String[] args)
   {
      // Calling the static average method
      // with an array of BankAccount objects

      Measurable[] accounts = new Measurable[3];
      accounts[0] = new BankAccount(0);
      accounts[1] = new BankAccount(10000);
      accounts[2] = new BankAccount(2000);

      double averageBalance = Measurable.average(accounts);
      System.out.println("Average balance: " + averageBalance);
      System.out.println("Expected: 4000");

      // Calling the static average method
      // with an array of Country objects
      
      Measurable[] countries = new Measurable[3];
      countries[0] = new Country("Uruguay", 176220);
      countries[1] = new Country("Thailand", 513120);
      countries[2] = new Country("Belgium", 30510);

      double averageArea = Measurable.average(countries);
      System.out.println("Average area: " + averageArea);
      System.out.println("Expected: 239950");
   }
}

public interface Measurable
{
   double getMeasure();  // An abstract method

   static double average(Measurable[] objects) // A static method
   {
      double sum = 0;
      for (Measurable obj : objects)
      {
         sum = sum + obj.getMeasure();
      }
      if (objects.length > 0) { return sum / objects.length; }
      else { return 0; }
   } 
}

/**
   A bank account has a balance that can be changed by 
   deposits and withdrawals.
*/
public class BankAccount implements measurable
{  
   private double balance;

   /**
      Constructs a bank account with a zero balance.
   */
   public BankAccount()
   {   
      balance = 0;
   }

   /**
      Constructs a bank account with a given balance.
      @param initialBalance the initial balance
   */
   public BankAccount(double initialBalance)
   {   
      balance = initialBalance;
   }

   /**
      Deposits money into the bank account.
      @param amount the amount to deposit
   */
   public void deposit(double amount)
   {  
      balance = balance + amount;
   }

   /**
      Withdraws money from the bank account.
      @param amount the amount to withdraw
   */
   public void withdraw(double amount)
   {   
      balance = balance - amount;
   }

   /**
      Gets the current balance of the bank account.
      @return the current balance
   */
   public double getBalance()
   {   
      return balance;
   }

   public double getMeasure()
   {
      return balance;
   }
}

/**
   A country with a name and area.
*/
public class Country implements Measurable
{
   private String name;
   private double area;

   /**
      Constructs a country.
      @param aName the name of the country
      @param anArea the area of the country
   */
   public Country(String aName, double anArea) 
   { 
      name = aName;
      area = anArea; 
   }

   /**
      Gets the country name.
      @return the name
   */
   public String getName() 
   {
      return name;
   }

   /**
      Gets the area of the country.
      @return the area
   */
   public double getArea() 
   {
      return area;
   }

   public double getMeasure() 
   {
      return area;
   }
}
```

#### Default Methods

A **default method** is a non-static method in an interface that has an implementation. A class that implements the method either inherits the default behavior or overrides it. By providing default methods in an interface, it is less work to define a class that implements an interface. 

For example, the Measurable interface can declare getMeasure as a default method:

```java
public interface Measurable 
{ 
    default double getMeasure() { return 0; } 
}
```

If a class implements the interface and doesn’t provide a getMeasure method, then it inherits this default method.
This particular example isn’t all that useful. One doesn’t normally want each object to have measure zero. Here is a more interesting example, in which a default method calls another interface method: 

```java
public interface Measurable 
{ 
    double getMeasure(); // An abstract method 
    default boolean smallerThan(Measurable other) 
    { 
        return getMeasure() < other.getMeasure(); 
    } 
}
```

The smallerThan method tests whether an object has a smaller measure than another, which is useful for arranging objects by increasing measure. A class that implements the Measurable interface only needs to implement getMeasure, and it automatically inherits the smallerThan method. This can be a very useful mechanism. For example, the Comparator interface that is described in Special Topic 14.4 has one abstract method but more than a dozen default methods.

full example
```java
/**
   This program demonstrates the smallerThan default method.
*/
public class MeasurableTester
{
   public static void main(String[] args)
   {
      Measurable[] countries = new Measurable[3];
      countries[0] = new Country("Uruguay", 176220);
      countries[1] = new Country("Thailand", 513120);
      countries[2] = new Country("Belgium", 30510);

      System.out.println("Uruguay is smaller than Thailand: "
         + countries[0].smallerThan(countries[1]));
      System.out.println("Expected: true");
      System.out.println("Uruguay is smaller than Belgium: "
         + countries[0].smallerThan(countries[2]));
      System.out.println("Expected: false");
   }
}

public interface Measurable
{
   double getMeasure(); // An abstract method
   
   default boolean smallerThan(Measurable other)
   {
      return getMeasure() < other.getMeasure();
   }
}

/**
   A bank account has a balance that can be changed by 
   deposits and withdrawals.
*/
public class BankAccount implements Measurable
{  
   private double balance;

   /**
      Constructs a bank account with a zero balance.
   */
   public BankAccount()
   {   
      balance = 0;
   }

   /**
      Constructs a bank account with a given balance.
      @param initialBalance the initial balance
   */
   public BankAccount(double initialBalance)
   {   
      balance = initialBalance;
   }

   /**
      Deposits money into the bank account.
      @param amount the amount to deposit
   */
   public void deposit(double amount)
   {  
      balance = balance + amount;
   }

   /**
      Withdraws money from the bank account.
      @param amount the amount to withdraw
   */
   public void withdraw(double amount)
   {   
      balance = balance - amount;
   }

   /**
      Gets the current balance of the bank account.
      @return the current balance
   */
   public double getBalance()
   {   
      return balance;
   }

   public double getMeasure()
   {
      return balance;
   }
}

/**
   A country with a name and area.
*/
public class Country implements Measurable
{
   private String name;
   private double area;

   /**
      Constructs a country.
      @param aName the name of the country
      @param anArea the area of the country
   */
   public Country(String aName, double anArea) 
   { 
      name = aName;
      area = anArea; 
   }

   /**
      Gets the country name.
      @return the name
   */
   public String getName() 
   {
      return name;
   }

   /**
      Gets the area of the country.
      @return the area
   */
   public double getArea() 
   {
      return area;
   }

   public double getMeasure() 
   {
      return area;
   }
}
```

#### Function Objects

In the preceding section, we used the Measurable interface type to make it possible to provide services that work for many classes—provided they are willing to implement the interface type. But what can you do if a class does not do so? For example, we might want to compute the average length of a collection of strings, but String does not implement Measurable.

Let’s rethink the approach. The average method needs to measure each object. When the objects are required to be of type Measurable, the responsibility for measuring lies with the objects themselves, which is the cause of the limitation that we noted. It would be better if another object could carry out the measurement. Let’s move the measurement method into a different interface:

```java
public interface Measurer
{
    double measure(Object anObject);
}
```

The measure method measures an object and returns its measurement. We use a parameter variable of type Object, the “lowest common denominator” of all classes in Java, because we do not want to restrict which classes can be measured. 

We add a parameter variable of type Measurer to the average method:

```java
public static double average(Object[] objects, Measurer meas)
{
    if (objects.length == 0) { return 0; }
    double sum = 0;
    for (Object obj : objects)
    {
        sum = sum + meas.measure(obj);
    }
    return sum / objects.length;
}
```

When calling the method, you need to supply a Measurer object. That is, you need to implement a class with a measure method, and then create an object of that class. Let’s do that for measuring strings:
```java			
public class StringMeasurer implements Measurer
{
    public double measure(Object obj)
    {
        String str = (String) obj; // Cast obj to String type
        return str.length();
    }
}
```

Note that the measure method must accept an argument of type Object, even though this particular measurer just wants to measure strings. The parameter variable must have the same type as in the Measurer interface. Therefore, the Object parameter variable is cast to the String type. Finally, we are ready to compute the average length of an array of strings:

```java
String[] words = { "Mary", "had", "a", "little", "lamb" };
Measurer lengthMeasurer = new StringMeasurer();
double result = average(words, lengthMeasurer); // result is set to 3.6
```

An object such as lengthMeasurer is called a function object. The sole purpose of the object is to execute a single method, in our case measure. (In mathematics, as well as many other programming languages, the term “function” is used where Java uses “method”.). The ```Comparator``` interface is another example of an interface for function objects.

Full example
```java
/**
   This program demonstrates the string measurer.
*/
public class MeasurerDemo
{
   public static void main(String[] args)
   {
      String[] words = { "Mary", "had", "a", "little", "lamb" };
      Measurer lengthMeasurer = new StringMeasurer();
      System.out.println("Average length: " 
         + average(words, lengthMeasurer));
   }

   /**
      Computes the average of the measures of the given objects.
      @param objects an array of objects
      @param meas the measurer
      @return the average of the measures
   */
   public static double average(Object[] objects, Measurer meas)
   {
      if (objects.length == 0) { return 0; }
      double sum = 0;
      for (Object obj : objects)
      {
         sum = sum + meas.measure(obj);
      }
      return sum / objects.length;
   }
}

/**
   Describes any class whose objects can measure other objects.
*/
public interface Measurer
{
   /**
      Computes the measure of an object.
      @param anObject the object to be measured
      @return the measure
   */
   double measure(Object anObject);
}

/**
   This class measures the length of a string.
*/
public class StringMeasurer implements Measurer
{
   public double measure(Object obj)
   {
      String str = (String) obj;
      return str.length();
   }
}
```

#### Lambda Expressions

Above, we discusses how to use function objects for specifying variations in behavior. The average method needs to measure each object, and it does so by calling the measure method of the supplied Measurer object.

Unfortunately, the caller of the average method has to do a fair amount of work; namely, to define a class that implements the Measurer interface and to construct an object of that class. Java 8 has a convenient shortcut for these steps, provided that the interface has a single abstract method. Such an interface is called a functional interface because its purpose is to define a single function. The Measurer interface is an example of a functional interface.

**Functional interface**: An interface with a single abstract method whose prupose is to define a single function.


To specify that single function, you can use a lambda expression, an expression that defines the parameters and return value of a method in a compact notation.

**Lambda Expression**: An expression that defines the parameters and return value of a method in a compact notation.

Here is an example:

```java
(Object obj) -> ((BankAccount) obj).getBalance()
```

This expression defines a function that, given an object, casts it to a BankAccount and returns the balance. (The term “lambda expression” comes from a mathematical notation that uses the Greek letter lambda (λ) instead of the -> symbol. In other programming languages, such an expression is called a function expression.) A lambda expression cannot stand alone. It needs to be assigned to a variable whose type is a functional interface:

```java
Measurer accountMeas = (Object obj) -> ((BankAccount) obj).getBalance();
```

Now the following actions occur:
```
1.  A class is defined that implements the functional interface. The single abstract method is defined by the lambda expression.
2.  An object of that class is constructed.
3.  The variable is assigned a reference to that object.
```
			
You can also pass a lambda expression to a method. Then the parameter variable of the method is initialized with the constructed object. For example, consider the call

```java
double averageBalance = average(accounts,
    (Object obj) –> ((BankAccount) obj).getBalance());
```

In the same way as before, an object is constructed that belongs to a class implementing Measurer. The object is used to initialize the parameter variable meas of the average method. Recall that the parameter variable has type Measurer:

```java
public static double average(Object[] objects, Measurer meas)
{
    . . .
    sum = sum + meas.measure(obj);
    . . .
}
```

The average method calls the measure method on meas, which in turn executes the body of the lambda expression. In its simplest form, a lambda expression contains a list of parameters and the expression that is being computed from the parameters. If more work needs to be done, you can write a method body in the usual way, enclosed in braces and with a return statement:

```java
Measurer areaMeas = (Object obj) –>
    {
        Rectangle r = (Rectangle) obj;
        return r.getWidth() * r.getHeight();
    };
```

Lambda expressions enable the caller of a method to provide code that is called inside the method, and they enable the implementor of the method to invoke that code as needed. This can be achieved as follows: 

```
1.The implementor of the method defines an interface that describes the purpose of the code to be executed. That interface has a single method.
2.The method receives a parameter of that interface, and calls the single method of the interface whenever the code that can vary needs to be called.
3.The caller of the method provides a lambda expression whose body is the code that should be called in this invocation.  
```

You will see additional examples of using lambda expressions for event handlers (Java 8 Note 10.1) and comparators (Section 14.8). Lambda expressions are extensively used in the “streams” API for processing large data sets.

Full example using lambda expressions
```java
import java.awt.Rectangle;

/**
   This program demonstrates the use of a Measurer.
*/
public class MeasurerTester
{
   public static void main(String[] args)
   {
      BankAccount[] accounts = new BankAccount[3];
      accounts[0] = new BankAccount(0);
      accounts[1] = new BankAccount(10000);
      accounts[2] = new BankAccount(2000);

      double averageBalance = Data.average(accounts,
         (Object obj) -> ((BankAccount) obj).getBalance());
      System.out.println("Average balance: " + averageBalance);
      System.out.println("Expected: 4000");

      Rectangle[] rects = new Rectangle[] 
         {
            new Rectangle(5, 10, 20, 30),
            new Rectangle(10, 20, 30, 40),
            new Rectangle(20, 30, 5, 15)
         };

      Measurer areaMeas = (Object obj) ->
         {
            Rectangle r = (Rectangle) obj;
            return r.getWidth() * r.getHeight();
         };      

      double averageArea = Data.average(rects, areaMeas);
      System.out.println("Average area: " + averageArea);
      System.out.println("Expected: 625");
   }
}

/**
   Describes any class whose objects can measure other objects.
*/
public interface Measurer
{
   /**
      Computes the measure of an object.
      @param anObject the object to be measured
      @return the measure
   */
   double measure(Object anObject);
}

/**
   A bank account has a balance that can be changed by 
   deposits and withdrawals.
*/
public class BankAccount
{  
   private double balance;

   /**
      Constructs a bank account with a zero balance.
   */
   public BankAccount()
   {   
      balance = 0;
   }

   /**
      Constructs a bank account with a given balance.
      @param initialBalance the initial balance
   */
   public BankAccount(double initialBalance)
   {   
      balance = initialBalance;
   }

   /**
      Deposits money into the bank account.
      @param amount the amount to deposit
   */
   public void deposit(double amount)
   {  
      balance = balance + amount;
   }

   /**
      Withdraws money from the bank account.
      @param amount the amount to withdraw
   */
   public void withdraw(double amount)
   {   
      balance = balance - amount;
   }

   /**
      Gets the current balance of the bank account.
      @return the current balance
   */
   public double getBalance()
   {   
      return balance;
   }
}

public class Data
{
   /**
      Computes the average of the measures of the given objects.
      @param objects an array of objects
      @param meas the measurer for the objects
      @return the average of the measures
   */
   public static double average(Object[] objects, Measurer meas)
   {
      double sum = 0;
      for (Object obj : objects)
      {
         sum = sum + meas.measure(obj);
      }
      if (objects.length > 0) { return sum / objects.length; }
      else { return 0; }
   }
}
```

### Interfaces Summary

The notions of inheritance, superclass, and subclass.

•A subclass inherits data and behavior from a superclass.\
•You can always use a subclass object in place of a superclass object.

Implement subclasses in Java.
   
•A subclass inherits all methods that it does not override.\
•A subclass can override a superclass method by providing a new implementation.\
•The extends reserved word indicates that a class inherits from a superclass.

Implement methods that override methods from a superclass. 

•An overriding method can extend or replace the functionality of the superclass method.\
•Use the reserved word super to call a superclass method.\
•Unless specified otherwise, the subclass constructor calls the superclass constructor with no arguments.\
•To call a superclass constructor, use the super reserved word in the first statement of the subclass constructor.\
•The constructor of a subclass can pass arguments to a superclass constructor, using the reserved word super.

Use polymorphism for processing objects of related types.
   
•A subclass reference can be used when a superclass reference is expected.\
•Polymorphism (“having multiple shapes”) allows us to manipulate objects that share a set of tasks, even though the tasks are executed in different ways.\
•An abstract method is a method whose implementation is not specified.\
•An abstract class is a class that cannot be instantiated.

Use the toString method and instanceof operator with objects.

•Override the toString method to yield a string that describes the object’s state.\
•The equals method checks whether two objects have the same contents.\
•If you know that an object belongs to a given class, use a cast to convert the type.\
•The instanceof operator tests whether an object belongs to a particular type.

Use interface types for algorithms that process objects of different classes.  

•A Java interface type contains the return types, names, and parameter variables of a set of methods.\
•Unlike a class, an interface type provides no implementation.\
•By using an interface type for a parameter variable, a method can accept objects from many classes.\
•The implements reserved word indicates which interfaces a class implements.\
•Implement the Comparable interface so that objects of your class can be compared, for example, in a sort method.

#### VarArgs


Pass in a variable number of arguments to a function like so:
```java
// A method that takes variable number of integer
// arguments.
static void fun(int ...a)
{
    System.out.println("Number of arguments: " + a.length);

    // using for each loop to display contents of a
    for (int i: a)
        System.out.print(i + " ");
    System.out.println();
}
```

#### Cloning

Note, if you want to clone an object, you will create a new object whose instance variables are copies of that of the original object. For primitive instance variables, there'll be no issue. For object instance variables, however, you will get a copy of the memory address to the same object. So, if you attempt to mutate the instance variable object of either the original object or the cloned object, you will be mutating the same instance variable object in memory. To get around this, you will want to do a **deep clone**, which means you also perform a clone of the instance variable objects within the cloned object and assign the cloned instance variables to be the new instance variables within the cloned object.

You do not need to perform a deep copy clone with String objects because they are immuatble. As soon as you would attempt to mutate an instance variable object of either the object or its clone, you would instantly create a new string.

## Graphical User Interfaces

### Frame Windows

A graphical application shows information inside a frame: a window with a title bar. To show a frame, construct a ```JFrame``` object, set its size, and make it visible.

```Java
JFrame frame = new JFrame(); 
final int FRAME_WIDTH = 300;
final int FRAME_HEIGHT = 400; 
frame.setSize(FRAME_WIDTH, FRAME_HEIGHT); 

// 3. set title frame
frame.setTitle("An empty frame"); 
//If you omit this step, the title bar is simply left blank. 

// 4.Set the “default close operation”:
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); 
// When the user closes the frame, the program automatically exits. Don’t omit this step. If you do, the program keeps running even after the 
// frame is closed.
 
// 5.Make the frame visible:
frame.setVisible(true);
```

### Adding User-Interface Components to a Frame

If you have more than one component, put them into a panel (a container for other user-interface components), and then add the panel to the frame. Use a JPanel to group multiple user-interface components together.

```java
JPanel panel = new JPanel();
panel.add(button);
panel.add(label);
frame.add(panel);

JButton button = new JButton("Click me!");
JLabel label = new JLabel("Hello, World!");
```

### Using Inheritance to Customize Frames

In Java, you can use inheritance to customize a frame.

```Declare a JFrame subclass for a complex frame.```

As you add more user-interface components to a frame, the frame can get quite complex. Your programs will become easier to understand when you use inheritance for complex frames. To do so, design a subclass of JFrame. Store the components as instance variables. Initialize them in the constructor of your subclass. This approach makes it easy to add helper methods for organizing your code. It is also a good idea to set the frame size in the frame constructor. The frame usually has a better idea of the preferred size than the program displaying it.

```java
public class FilledFrame extends JFrame
{
    // Use instance variables for components 
    private JButton button;
    private JLabel label;
    
    private static final int FRAME_WIDTH = 300;
    private static final int FRAME_HEIGHT = 100;
    
    public FilledFrame()
    { 
        // Now we can use a helper method 
        createComponents();
    
        // It is a good idea to set the size in the frame constructor 
        setSize(FRAME_WIDTH, FRAME_HEIGHT);
    }
    
    private void createComponents()
    {
        button = new JButton("Click me!");
        label = new JLabel("Hello, World!");
        JPanel panel = new JPanel();
        panel.add(button);
        panel.add(label);      
        add(panel);
    }
}

public class FilledFrameViewer2
{ 
    public static void main(String[] args)
    { 
        JFrame frame = new FilledFrame();
        frame.setTitle("A frame with two components");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);      
    }
}
```

#### Adding a main method to the Frame Class

Have another look at the FilledFrame and FilledFrameViewer2 classes. Some programmers prefer to combine these two classes, by adding the main method to the frame class:
```java
public class FilledFrame extends JFrame
{ 
    . . . 
    public static void main(String[] args)
    {
        JFrame frame = new FilledFrame();
        frame.setTitle("A frame with two components");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }
    
    public FilledFrame()
    {
        createComponents();
        setSize(FRAME_WIDTH, FRAME_HEIGHT); 
    }
    . . .
}
```


### Events and Event Handling

In an application that interacts with the user through a console window, user input is under control of the program. The program asks the user for input in a specific order. For example, a program might ask the user to supply first a name, then a dollar amount. But the programs that you use every day on your computer don’t work like that. In a program with a modern graphical user interface, the user is in control. The user can use both the mouse and the keyboard and can manipulate many parts of the user interface in any desired order. For example, the user can enter information into text fields, pull down menus, click buttons, and drag scroll bars in any order. The program must react to the user commands in whatever order they arrive. Having to deal with many possible inputs in random order is quite a bit harder than simply forcing the user to supply input in a fixed order. 

#### Listening to Events

Whenever the user of a graphical program types characters or uses the mouse anywhere inside one of the windows of the program, the program receives a notification that an event has occurred. For example, whenever the mouse moves a tiny interval over a window, a “mouse move” event is generated. Clicking a button or selecting a menu item generates an “action” event. 

Most programs don’t want to be flooded by irrelevant events. For example, when a button is clicked with the mouse, the mouse moves over the button, then the mouse button is pressed, and finally the button is released. Rather than receiving all these mouse events, a program can indicate that it only cares about button clicks, not about the underlying mouse events. On the other hand, if the mouse input is used for drawing shapes on a virtual canvas, a program needs to closely track mouse events.

```User-interface events include key presses, mouse moves, button clicks, menu selections, and so on.```

Every program must indicate which events it needs to receive. It does that by installing event listener objects. These objects are instances of classes that you must provide. The methods of your event listener classes contain the instructions that you want to have executed when the events occur. 

To install a listener, you need to know the event source. The event source is the user-interface component, such as a button, that generates a particular event. You add an event listener object to the appropriate event sources. Whenever the event occurs, the event source calls the appropriate methods of all attached event listeners.

```An event listener belongs to a class created by the application programmer. Its methods describe the actions to be taken when an event occurs.```

This sounds somewhat abstract, so let’s run through an extremely simple program that prints a message whenever a button is clicked. Button listeners must belong to a class that implements the ActionListener interface:

```java
public interface ActionListener
{
    void actionPerformed(ActionEvent event);
}
```

This particular interface has a single method, actionPerformed. It is your job to supply a class whose actionPerformed method contains the instructions that you want executed whenever the button is clicked. Here is a very simple example of such a listener class:

```java

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

/** 
    An action listener that prints a message.
*/
public class ClickListener implements ActionListener
{
    public void actionPerformed(ActionEevent event)
    {
        System.out.println("I was clicked.");
    }
}
```

We ignore the event parameter variable of the actionPerformed method—it contains additional details about the event, such as the time at which it occurred. Note that the event handling classes are defined in the java.awt.event package. (AWT is the Abstract Window Toolkit, the Java library for dealing with windows and events.)
			

```Attach an ActionListener to each button so that your program can react to button clicks.```

Once the listener class has been declared, we need to construct an object of the class and add it to the button:

```java
ActionListener listener = new ClickListener();
button.addActionListener(listener);
```

Whenever the button is clicked, the Java event handling library calls

```java
listener.actionPerformed(event);
```

As a result, the message is printed. 


### Using Inner Classes for Listeners

n the preceding section, you saw how to specify button actions. The code for the button action is placed into a listener class. It is common to implement listener classes as inner classes like this:

```java
public class ButtonFrame2 extends JFrame
{
    . . .
    // This inner class is declared inside the frame class
    class ClickListener implements ActionListener 
    {
        . . .
    }
    
    private void createComponents()
    {
        button = new JButton("Click me!");
        ActionListener listener = new ClickListener();
        button.addActionListener(listener);
        . . .
    }
}
```
An inner class is simply a class that is declared inside another class.

There are two advantages to making a listener class into an inner class. First, listener classes tend to be very short. You can put the inner class close to where it is needed, without cluttering up the remainder of the project. Moreover, inner classes have a very attractive feature: 

Their methods can access instance variables and methods of the surrounding class. 

```Methods of an inner class can access variables from the surrounding class.```

This feature is particularly useful when implementing event handlers. It allows the inner class to access variables without having to receive them as constructor or method arguments. 

Let’s look at an example. Instead of printing the message “I was clicked”, we want to show it in a label. If we make the action listener into an inner class of the frame class, its actionPerformed method can access the label instance variable and call the setText method, which changes the label text.

```java

public class ButtonFrame2 extends JFrame
{
    private JButton button;
    private JLabel label;
    . . . 
    class ClickListener implements ActionListener 
    {
        public void actionPerformed(ActionEvent event)
        {
            // Accesses label variable from surrounding class
            label.setText("I was clicked"); 
        }
    }
    . . .
}
```

#### Common Errors

**Modifying Parameter Types in the Implemeneting Method**

When you implement an interface, you must declare each method exactly as it is specified in the interface. Accidentally making small changes to the parameter variable types is a common error. Here is the classic example,

```java
class MyListener implements ActionListener
{
    public void actionPerformed() 
    // Oops . . . forgot ActionEvent parameter variable
    {
        . . .
    }
}
```

As far as the compiler is concerned, this class fails to provide the method

```java
public void actionPerformed(ActionEvent event)
```

You have to read the error message carefully and pay attention to the parameter variable and return types to find your error.


**Forgetting to Attach a Listener**

If you run your program and find that your buttons seem to be dead, double-check that you attached the button listener. The same holds for other user-interface components. It is a surprisingly common error to program the listener class and the event handler action without actually attaching the listener to the event source. 

**Tip: Don't use a Frame as a Listener**

we use inner classes for event listeners. That approach works for many different event types. Once you master the technique, you don’t have to think about it anymore. Many development environments automatically generate code with inner classes, so it is a good idea to be familiar with them. 

However, some programmers bypass the event listener classes and turn a frame into a listener, like this: 

```java
public class InvestmentFrame extends JFrame
        implements ActionListener  // This approach is not recommended 
{ 
    . . .
    public InvestmentFrame()
    {
        button = new JButton("Add Interest");
        button.addActionListener(this);
        . . .
    }
    
    public void actionPerformed(ActionEvent event)
    {
    }
    . . .
}
```

Now the actionPerformed method is a part of the InvestmentFrame class rather than part of a separate listener class. The listener is installed as this. 

We don’t recommend this technique. If the viewer class contains two buttons that each generate action events, then the actionPerformed method must investigate the event source, which leads to code that is tedious and error-prone. 

**Local Inner Class**

An inner class can be declared completely inside a method. For example,

```java
public static void main(String[] args)
{
    . . . 
    class ClickListener implements ActionListener 
    {
        public void actionPerformed(ActionEvent event)
        {
            . . .
        }
    }
    
    JButton button = new JButton("Click me");
    button.addActionListener(new ClickListener());
    . . .
}
```

This places the inner class exactly where you need it, next to the button. 

The methods of a class that is defined inside a method can access the variables of the enclosing method. Prior to Java 8, it was necessary to declare those variables as final. For example, 

```java
public static void main(String[] args)
{
    final JLabel label = new JLabel("Hello, World!");
    . . . 
    class ClickListener implements ActionListener 
    {
        public void actionPerformed(ActionEvent event)
        {
            label.setText("I was clicked"); 
            // Accesses label variable from enclosing method
        }
    }
    . . . 
    button.addActionListener(new ClickListener());
}
```

As of Java 8, the variable must be effectively final. Such a variable must behave like a final variable (that is, stay unchanged after it has been initialized), but it need not be declared with the final modifier. The requirement to be final or effectively final sounds quite restrictive. However, it is usually not an issue if the variable is an object reference. Keep in mind that an object variable is final when the variable always refers to the same object. The state of the object can change, but the variable can’t refer to a different object. For example, in our program, we never intended to have the label variable refer to multiple labels, so there was no harm in declaring it as final.
However, you can’t change a numeric or Boolean local variable from an inner class. For example, the following would not work:

```java
public static void main(String[] args)
{
    final double balance = INITIAL_BALANCE;
    . . . 

    class AddInterestListener implements ActionListener 
    {
        public void actionPerformed(ActionEvent event)
        {
            double interest = balance * (1 + INTEREST_RATE);
            balance = balance + interest;
            // Error: Can’t modify a final numeric variable
        }
    }
    . . . 
}
```

The remedy is to use an object instead:

```java
public static void main(String[] args)
{
    final BankAccount account = new BankAccount();
    account.deposit(INITIAL_BALANCE);
    . . . 
    class AddInterestListener implements ActionListener 
    {
        public void actionPerformed(ActionEvent event)
        {
            double interest = balance * (1 + INTEREST_RATE);
            account.deposit(interest);
            // Ok––we don’t change the reference, just the object’s state
        }
    }
    . . .
}
```

**Anonymous Inner Classes**
An entity is anonymous if it does not have a name. In a program, something that is only used once doesn’t usually need a name. For example, you can replace

```java
String buttonLabel = "Add Interest";
JButton button = new JButton(buttonLabel);
```

with

```java
JButton button = new JButton("Add Interest");
```

The string "Add Interest" is an anonymous object. Programmers like anonymous objects, because they don’t have to go through the trouble of coming up with a name. If you have struggled with the decision whether to call a label l, label, or buttonLabel, you’ll understand this sentiment.

Event listeners often give rise to a similar situation. You construct a single object of an event listener class. Afterward, the class is never used again. In Java, it is possible to declare an anonymous class if all you ever need is a single object of the class. 
Here is an example:

```java
button = new JButton("Add Interest");
button.addActionListener(new ActionListener()
{
    public void actionPerformed(ActionEvent event)
    {
        double interest = balance * (1 + INTEREST_RATE);
        account.deposit(interest);
    }
});
```
This means: Define a class that implements the ActionListener interface with the given actionPerformed method. Construct an object of that class and pass it to the addActionListener method.

Many programmers like this style because it is so compact. Moreover, GUI builders in integrated development environments often generate code of this form.

**Lambda Expressions for Event Handling**

We discussed lambda expressions for instances of classes that implement “functional” interfaces; that is, interfaces with a single abstract method. This includes event handlers such as ActionListener objects.

For example, instead of declaring a ClickListener class and adding an instance as a listener to a button, you can simply add the listener as follows:

```java
button.addActionListener( 
    (ActionEvent event) –> System.out.println("I was clicked."));
```

#### Processing Text Input

#### Text Fields

The JTextField class provides a text field for reading a single line of text. When you construct a text field, you need to supply the width—the approximate number of characters that you expect the user to type.

```java
final int FIELD_WIDTH = 10;
rateField = new JTextField(FIELD_WIDTH);
```

Users can type additional characters, but then a part of the contents of the field becomes invisible. You will want to label each text field so that the user knows what to type into it. Construct a JLabel object for each label:

```java
JLabel rateLabel = new JLabel("Interest Rate: ");
```

You want to give the user an opportunity to enter all information into the text fields before processing it. Therefore, you should supply a button that the user can press to indicate that the input is ready for processing. 

When that button is clicked, its actionPerformed method should read the user input from each text field, using the getText method of the JTextField class. The getText method returns a String object. In our sample program, we turn the string into a number, using the Double.parseDouble method. After updating the account, we show the balance in another label.

```java
class AddInterestListener implements ActionListener
{
    public void actionPerformed(ActionEvent event)
    {
        double rate = Double.parseDouble(rateField.getText());
        double interest = balance * rate / 100;
        balance = balance + interest;
        resultLabel.setText("Balance: " + balance);
    }
}
```

#### Text Areas

When constructing a text area, you can specify the number of rows and columns: 

```java
final int ROWS = 10; // Lines of text
final int COLUMNS = 30; // Characters in each row
JTextArea textArea = new JTextArea(ROWS, COLUMNS);
```

Use the setText method to set the text of a text field or text area. The append method adds text to the end of a text area. Use newline characters to separate lines, like this:

```java
textArea.append(balance + "\n");
```

If you want to use a text field or text area for display purposes only, call the setEditable method like this 

```java
textArea.setEditable(false);
```

Now the user can no longer edit the contents of the field, but your program can still call setText and append to change it. 

As shown in Figure 6, the JTextField and JTextArea classes are subclasses of the class JTextComponent. The methods setText and setEditable are declared in the JTextComponent class and inherited by JTextField and JTextArea. However, the append method is declared in the JTextArea class.

![alt text](pics\text_areas.JPG "Title")

To add scroll bars to a text area, use a JScrollPane, like this: 

```java
JTextArea textArea = new JTextArea(ROWS, COLUMNS);
JScrollPane scrollPane = new JScrollPane(textArea);
```

```You can add scroll bars to any component with a JScrollPane.```

#### Creating Drawings

#### Drawing on a Component

You cannot draw directly onto a frame. Instead, you add a component to the frame and draw on the component. To do so, extend the JComponent class and override its paintComponent method.

```java
public class ChartComponent extends JComponent
{
    public void paintComponent(Graphics g)
    { 
        Drawing instructions.
    }
}
```

```In order to display a drawing, provide a class that extends the JComponent class.```

Place drawing instructions inside the paintComponent method. That method is called whenever the component needs to be repainted.

When the component is shown for the first time, its paintComponent method is called automatically. The method is also called when the window is resized, or when it is shown again after it was hidden. 

The paintComponent method receives an object of type Graphics. The Graphics object stores the graphics state—the current color, font, and so on, that are used for drawing operations. The Graphics class has methods for drawing geometric shapes. The call

```java
g.fillRect(x, y, width, height)
```

draws a solid rectangle with upper-left corner (x, y) and the given width and height. If you call the drawRect method, you obtain the outline of the rectangle instead, without having the interior filled.

```The Graphics class has methods to draw rectangles and other shapes.```

Here we produce three filled rectangles. They line up on the left because they all have x = 0. They also all have the same height.

```java
public class ChartComponent extends JComponent
{ 
    public void paintComponent(Graphics g)
    { 
        g.fillRect(0, 10, 200, 10);
        g.fillRect(0, 30, 300, 10);
        g.fillRect(0, 50, 100, 10);
    }
}
```

#### Ovals, Lines, Text, and Color

To draw an oval, you specify its bounding box (see Figure 9) in the same way that you would specify a rectangle, namely by the x- and y-coordinates of the top-left corner and the width and height of the box. Then the call

```java
g.drawOval(x, y, width, height);   
```

draws the outline of an oval. To draw a circle, simply set the width and height to the same values: 

```java
g.drawOval(x, y, diameter, diameter);
```

Notice that (x, y) is the top-left corner of the bounding box, not the center of the circle.

```Use drawRect, drawOval, and drawLine to draw geometric shapes.```

```Use drawRect, drawOval, and drawLine to draw geometric shapes.```

When you set a new color in the graphics context, it is used for subsequent drawing operations.

```java
g.setColor(Color.YELLOW);
g.fillOval(350, 25, 35, 20); // Fills the oval in yellow
```

```java
// Call the repaint method whenever the state of a painted component changes.
// When placing a painted component into a panel, you need to specify its preferred size.

chart.setPreferredSize(new Dimension(CHART_WIDTH, CHART_HEIGHT));
```

#### Common Errors

When you change the data in a painted component, the component is not automatically painted with the new data. You must call the repaint method of the component. Your component’s paintComponent method will then be invoked. Note that you should not call the paintComponent method directly. 

The best place to call repaint is in the method of your component that modifies the data values:

```java
void changeData(. . .)
{
    Update data values.
    repaint();
}
```

This is a concern only for your own painted components. When you make a change to a standard Swing component such as a JLabel, the component is automatically repainted.

**By Default, Components Have Zero Width and Height**

You must be careful when you add a painted component, such as a component displaying a chart, to a panel. The default size for a JComponent is 0 by 0 pixels, and the component will not be visible. The remedy is to call the setPreferredSize method: 

```java
chart.setPreferredSize(new Dimension(CHART_WIDTH, CHART_HEIGHT));
```

This is an issue only for painted components. Buttons, labels, and so on, know how to compute their preferred size.

## Layout Management

```User-interface components are arranged by placing them inside containers. Containers can be placed inside larger containers.```

Up to now, you have had limited control over the layout of user-interface components. You learned how to add components to a panel, and the panel arranged the components from left to right. However, in many applications, you need more sophisticated arrangements. 

In Java, you build up user interfaces by adding components into containers such as panels. Each container has its own **layout manager**, which determines how components are laid out.

```Each container has a layout manager that directs the arrangement of its components.```

By default, a JPanel uses a **flow layout**. A flow layout simply arranges its components from left to right and starts a new row when there is no more room in the current row. 

Another commonly used layout manager is the border layout. The **border layout** groups components into five areas: center, north, south, west, and east (see Figure 1). Each area can hold a single component, or it can be empty.

```Three useful layout managers are the border layout, flow layout, and grid layout.```

The border layout is the default layout manager for a frame (or, more technically, the frame’s content pane). But you can also use the border layout in a panel:

```When adding a component to a container with the border layout, specify the NORTH, SOUTH, WEST, EAST, or CENTER position.```

panel.setLayout(new BorderLayout());
Now the panel is controlled by a border layout, not the flow layout. When adding a component, you specify the position, like this:
panel.add(component, BorderLayout.NORTH);

```The content pane of a frame has a border layout by default. A panel has a flow layout by default.```

The **grid layout** manager arranges components in a grid with a fixed number of rows and columns. All components are resized so that they all have the same width and height. Like the border layout, it also expands each component to fill the entire allotted area. (If that is not desirable, you need to place each component inside a panel.) Figure 2 shows a number pad panel that uses a grid layout. 

To create a grid layout, you supply the number of rows and columns in the constructor, then add the components, row by row, left to right: 

```java
JPanel buttonPanel = new JPanel();
buttonPanel.setLayout(new GridLayout(4, 3));
buttonPanel.add(button7);
buttonPanel.add(button8);
buttonPanel.add(button9);
buttonPanel.add(button4);
```

### Radio Buttons

```For a small set of mutually exclusive choices, use a group of radio buttons or a combo box.```

If the choices are mutually exclusive, use a set of radio buttons. In a radio button set, only one button can be selected at a time. When the user selects another button in the same set, the previously selected button is automatically turned off. (These buttons are called radio buttons because they work like the station selector buttons on a car radio: If you select a new station, the old station is automatically deselected.) For example, in Figure 4, the font sizes are mutually exclusive. You can select small, medium, or large, but not a combination of them. 
			
```Add radio buttons to a ButtonGroup so that only one button in the group is selected at any time.```

To create a set of radio buttons, first create each button individually, and then add all buttons in the set to a ButtonGroup object: 

```java
JRadioButton smallButton = new JRadioButton("Small");
JRadioButton mediumButton = new JRadioButton("Medium");
JRadioButton largeButton = new JRadioButton("Large");
    
ButtonGroup group = new ButtonGroup();
group.add(smallButton);
group.add(mediumButton);
group.add(largeButton);
```

The isSelected method is called to find out whether a button is currently selected or not. For example, 

```java
if (largeButton.isSelected()) { size = LARGE_SIZE; }
```

Unfortunately, there is no convenient way of finding out which button in a group is currently selected. You have to call isSelected on each button. Because users will expect one radio button in a radio button group to be selected, call setSelected(true) on the default radio button before making the enclosing frame visible. 

```You can place a border around a panel to group its contents visually.```

If you have multiple button groups, it is a good idea to group them together visually. It is a good idea to use a panel for each set of radio buttons, but the panels themselves are invisible. You can add a border to a panel to make it visible. In Figure 4, for example, the panels containing the Size radio buttons and Style check boxes have borders. 

#### Check Boxes

```For a binary choice, use a check box. ```
			
A check box is a user-interface component with two states: checked and unchecked. You use a group of check boxes when one selection does not exclude another. For example, the choices for “Bold” and “Italic” in Figure 4 are not exclusive. You can choose either, both, or neither. Therefore, they are implemented as a set of separate check boxes. Radio buttons and check boxes have different visual appearances. Radio buttons are round and have a black dot when selected. Check boxes are square and have a check mark when selected. 

You construct a check box by providing the name in the constructor: 

```java
JCheckBox italicCheckBox = new JCheckBox("Italic");
```


#### Combo Boxes

If you have a large number of choices, you don’t want to make a set of radio buttons, because that would take up a lot of space. Instead, you can use a combo box. This component is called a combo box because it is a combination of a list and a text field. The text field displays the name of the current selection. When you click on the arrow to the right of the text field of a combo box, a list of selections drops down, and you can choose one of the items in the list 

```For a large set of choices, use a combo box.```

If the combo box is editable, you can also type in your own selection. To make a combo box editable, call the setEditable method. 

You add strings to a combo box with the addItem method. 

```java
JComboBox facenameCombo = new JComboBox();
facenameCombo.addItem("Serif");
facenameCombo.addItem("SansSerif");
. . .
```

You get the item that the user has selected by calling the getSelectedItem method. However, because combo boxes can store other objects in addition to strings, the getSelectedItem method has return type Object. Hence, in our example, you must cast the returned value back to String:

```java
String selectedString = (String) facenameCombo.getSelectedItem();  
```

You can select an item for the user with the setSelectedItem method.

Radio buttons, check boxes, and combo boxes generate an ActionEvent whenever the user selects an item. In the following program, we don’t care which component was clicked—all components notify the same listener object. Whenever the user clicks on any one of them, we simply ask each component for its current content, using the isSelected and getSelectedItem methods. We then redraw the label with the new font.

```Radio buttons, check boxes, and combo boxes generate action events, just as buttons do.```

**PROGRAMMING TIP: Use a GUI Builder**

### Menus

```A frame contains a menu bar. The menu bar contains menus. A menu contains submenus and menu items.```

You add the menu bar to the frame:

```java
public class MyFrame extends JFrame
{
    public MyFrame()
    {
        JMenuBar menuBar = new JMenuBar();
        setJMenuBar(menuBar);
        . . .
    }
    . . .
}
```

Menus are then added to the menu bar:

```java
JMenu fileMenu = new JMenu("File");
JMenu fontMenu = new JMenu("Font");
menuBar.add(fileMenu);
menuBar.add(fontMenu);
```

You add menu items and submenus with the add method: 

```java
JMenuItem exitItem = new JMenuItem("Exit");
fileMenu.add(exitItem);
    
JMenu styleMenu = new JMenu("Style");
fontMenu.add(styleMenu); // A submenu
```


Menu items generate action events.

A menu item has no further submenus. When the user selects a menu item, the menu item sends an action event. Therefore, you want to add a listener to each menu item: 

```java
ActionListener listener = new ExitItemListener();
exitItem.addActionListener(listener);
```

You add action listeners only to menu items, not to menus or the menu bar. When the user clicks on a menu name and a submenu opens, no action event is sent. 

To keep the program readable, it is a good idea to use a separate method for each menu or set of related menus. For example,

```java
public JMenu createFaceMenu()
{
    JMenu menu = new JMenu("Face");
    menu.add(createFaceItem("Serif"));
    menu.add(createFaceItem("SansSerif"));
    menu.add(createFaceItem("Monospaced"));
    return menu;
}  
```

Now consider the createFaceItem method. It has a string parameter variable for the name of the font face. When the item is selected, its action listener needs to 

1.Set the current face name to the menu item text.

2.Make a new font from the current face, size, and style, and apply it to the label.
We have three menu items, one for each supported face name. Each of them needs to set a different name in the first step. Of course, we can make three listener classes SerifListener, SansSerifListener, and MonospacedListener, but that is not very elegant. After all, the actions only vary by a single string. We can store that string inside the listener class and then make three objects of the same listener class:

```java
class FaceItemListener implements ActionListener
{
    private String name;
    
    public FaceItemListener(String newName) { name = newName; }
    

    public void actionPerformed(ActionEvent event)
    {
        facename = name; // Sets an instance variable of the frame class
        setLabelFont(); 
    }
}
```

Now we can install a listener object with the appropriate name:

```java
public JMenuItem createFaceItem(String name)
{
    JMenuItem item = new JMenuItem(name);      
    ActionListener listener = new FaceItemListener(name);
    item.addActionListener(listener);
    return item;
}
```

This approach is still a bit tedious. We can do better by using a local inner class (see Special Topic 10.2). When we move the declaration of the inner class inside the createFaceItem method, the actionPerformed method can access the name parameter variable directly. Before Java 8, it was necessary to declare name as a final variable in order for it to be accessible from an inner class method. 

```java
public JMenuItem createFaceItem(final String name) 
{
    class FaceItemListener implements ActionListener // A local inner class
    {
        public void actionPerformed(ActionEvent event)
        {
            facename = name; // Accesses the local variable name
            setLabelFont();
        }
    }      
    
    JMenuItem item = new JMenuItem(name);      
    ActionListener listener = new FaceItemListener();
    item.addActionListener(listener);
    return item;
}
```

The same strategy is used for the createSizeItem and createStyleItem methods.

### Exploring the Swing Documentation

```You should learn to navigate the API documentation to find out more about user-interface components.```

E.g.
```java
public JSlider()
    //Creates a horizontal slider with the range 0 to 100 and an initial value of 50.
```


### Using Timer Events for Animations

The Timer class in the javax.swing package generates a sequence of action events, spaced at even time intervals. (You can think of a timer as an invisible button that is automatically clicked.) This is useful whenever you want to send continuous updates to a component. For example, in an animation, you may want to update a scene ten times per second and redisplay the image to give the illusion of movement. 

```A timer generates action events at fixed intervals.```

When you use a timer, you specify the frequency of the events and an object of a class that implements the ActionListener interface. Place whatever action you want to occur inside the actionPerformed method. Finally, start the timer.

```java
class MyListener implements ActionListener
{
    public void actionPerformed(ActionEvent event)
    {
        // Action that is executed at each timer event. 
    }
}
    
MyListener listener = new MyListener();
Timer t = new Timer(interval, listener);
t.start();
```

Then the timer calls the actionPerformed method of the listener object every interval milliseconds. 

Our sample program will display a moving rectangle. We first supply a RectangleComponent class with a moveRectangleBy method that moves the rectangle by a given amount. 

Note the call to repaint in the moveRectangleBy method. This call is necessary to ensure that the component is repainted after the position of the rectangle has been changed. The call to repaint forces a call to the paintComponent method. The paintComponent method redraws the component, causing the rectangle to appear at the updated location. 

The actionPerformed method of the timer listener moves the rectangle one pixel down and to the right:

```java
scene.moveRectangleBy(1, 1); 
```

```To make an animation, the timer listener should update and repaint a component several times per second. ```

Because the actionPerformed method is called many times per second, the rectangle appears to move smoothly across the frame. 

### Mouse Events

If you write programs that show drawings, and you want users to manipulate the drawings with a mouse, then you need to listen to mouse events. Mouse listeners are more complex than action listeners, the listeners that process button clicks and timer ticks.

```You use a mouse listener to capture mouse events.```

A mouse listener must implement the MouseListener interface, which contains the following five methods: 

```java
public interface MouseListener
{ 
    void mousePressed(MouseEvent event);
        // Called when a mouse button has been pressed on a component 
    void mouseReleased(MouseEvent event);
        // Called when a mouse button has been released on a component 
    void mouseClicked(MouseEvent event);
        // Called when the mouse has been clicked on a component 
    void mouseEntered(MouseEvent event);
        // Called when the mouse enters a component 
    void mouseExited(MouseEvent event);
        // Called when the mouse exits a component 
}
```

The mousePressed and mouseReleased methods are called whenever a mouse button is pressed or released. If a button is pressed and released in quick succession, and the mouse has not moved, then the mouseClicked method is called as well. The mouseEntered and mouseExited methods can be used to highlight a user-interface component whenever the mouse is pointing inside it. 

The most commonly used method is mousePressed. Users generally expect that their actions are processed as soon as the mouse button is pressed. 
You add a mouse listener to a component by calling the addMouseListener method:

```java
public class MyMouseListener implements MouseListener
{
    public void mousePressed(MouseEvent event)
    { 
        int x = event.getX();
        int y = event.getY();
        Process mouse event at (x, y).
    }
    
    // Do-nothing methods
    public void mouseReleased(MouseEvent event) {}
    public void mouseClicked(MouseEvent event) {}
    public void mouseEntered(MouseEvent event) {}
    public void mouseExited(MouseEvent event) {}
}
    
MouseListener listener = new MyMouseListener();
component.addMouseListener(listener);
```

In the sample program, a user clicks on a component containing a rectangle. Whenever the mouse button is pressed, the rectangle is moved to the mouse location. We first enhance the RectangleComponent class and add a moveRectangleTo method to move the rectangle to a new position. 

Note the call to repaint in the moveRectangleTo method. As you saw before, this call causes the component to repaint itself and show the rectangle in the new position. 

Now, add a mouse listener to the component. Whenever the mouse is pressed, the listener moves the rectangle to the mouse location. 

```java
class MousePressListener implements MouseListener
{ 
    public void mousePressed(MouseEvent event)
    { 
        int x = event.getX();
        int y = event.getY();
        scene.moveRectangleTo(x, y);
    }
    . . .
}
```

It often happens that a particular listener specifies actions only for one or two of the listener methods. Nevertheless, all five methods of the interface must be implemented. The unused methods are simply implemented as do-nothing methods. 

### Keyboard Events

If you program a game, you may want to process keystrokes, such as the arrow keys. Add a key listener to the component on which you draw the game scene. The KeyListener interface has three methods. As with a mouse listener, you are most interested in key press events, and you can leave the other two methods empty. Your key listener class should look like this:

```java
class MyKeyListener implements KeyListener
{ 
    public void keyPressed(KeyEvent event)
    { 
        String key = KeyStroke.getKeyStrokeForEvent(event).toString();
        key = key.replace("pressed ", ""); 
        Process key.
    }
    

    // Do-nothing methods
    public void keyReleased(KeyEvent event) {}
    public void keyTyped(KeyEvent event) {}
}
```

The call KeyStroke.getKeyStrokeForEvent(event).toString() turns the event object into a text description of the key, such as "pressed LEFT". In the next line, we eliminate the "pressed " prefix. The remainder is a string such as "LEFT" or "A" that describes the key that was pressed. 

You can find a list of all key names in the API documentation of the KeyStroke class.

```Whenever the program user presses a key, a key event is generated.```
    
As always, remember to attach the listener to the event source:

```java
KeyListener listener = new MyKeyListener();
scene.addKeyListener(listener);
```

In order to receive key events, your component must call 

```java
scene.setFocusable(true);
```

### Event Adapters

In the preceding section you saw how to install a mouse listener in a mouse event source and how the listener methods are called when an event occurs. Usually, a program is not interested in all listener notifications. For example, a program may only be interested in mouse clicks and may not care that these mouse clicks are composed of “mouse pressed” and “mouse released” events. Of course, the program could supply a listener that declares all those methods in which it has no interest as “do-nothing” methods, for example: 

```java
class MouseClickListener implements MouseListener
{ 
    public void mouseClicked(MouseEvent event) 
    { 
        Mouse click action
    }
    
    // Four do-nothing methods 
    public void mouseEntered(MouseEvent event) {}
    public void mouseExited(MouseEvent event) {}
    public void mousePressed(MouseEvent event) {}
    public void mouseReleased(MouseEvent event) {}
}
```

To avoid this labor, some friendly soul has created a MouseAdapter class that implements the MouseListener interface such that all methods do nothing. You can extend that class, inheriting the do-nothing methods and overriding the methods that you care about, like this:

```java
class MouseClickListener extends MouseAdapter
{ 
    public void mouseClicked(MouseEvent event)
    { 
        Mouse click action
    }
}
```

There is also a KeyAdapter that implements the KeyListener interface, providing three do-nothing methods.