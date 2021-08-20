
# What is Kotlin
Kotlin is a general-purpose, statically typed, and open-source programming language. It runs on JVM and can be used anywhere Java is used today. It can be used to develop Android apps, server-side apps and much more.

# History of Kotlin
Kotlin was developed by JetBrains team. A project was started in 2010 to develop the language and officially, first released in February 2016. Kotlin was developed under the Apache 2.0 license.

# Features of Kotlin
* Concise: Kotlin reduces writing the extra codes. This makes Kotlin more concise.
* Null safety: Kotlin is null safety language. Kotlin aimed to eliminate the NullPointerException (null reference) from the code.Interoperable.
* Interoperable: Kotlin easily calls the Java code in a natural way as well as Kotlin code can be used by Java.
* Smart cast: It explicitly typecasts the immutable values and inserts the value in its safe cast automatically.
* Compilation Time: It has better performance and fast compilation time.
* Tool-friendly: Kotlin programs are build using the command line as well as any of Java IDE.
* Extension function: Kotlin supports extension functions and extension properties which means it helps to extend the functionality of classes without touching their code.

# Kotlin Environment Setup (Command line)

## Prerequisite

Since Kotlin runs on JVM, it is necessary to install JDK and setup the JDK and JRE path in local system environment variable.

To setup Kotlin for command line, you have to pre install JDK 1.6+ or above. To install JDK and set path of JDK and JRE refer link Set Path in Java .

## Setup Kotlin for Command Line

To setup Kotlin for command line, we need to go through following steps:

1. Download the Kotlin Compiler from GitHub Releases https://github.com/JetBrains/kotlin/releases/tag/v1.2.21 .



2. Extract downloaded zip in any of system location (in my case it is in C drive).

3. Copy the path up to bin directory of kotlinc.

![b](https://user-images.githubusercontent.com/51777024/128830600-dbe57430-6953-4363-93b2-3f8ef464188a.png)

4. Open Computer properties and click Environment variables.

![c](https://user-images.githubusercontent.com/51777024/128830614-465c1cfb-7078-4698-b1fc-a87626edddf7.png)

5. Click on edit path

![d](https://user-images.githubusercontent.com/51777024/128830627-0a210135-0e19-4a9e-a494-d5ea5a1bb3ad.png)

6. Past the path of kotlinc bin directory in variable value.

![e](https://user-images.githubusercontent.com/51777024/128830641-4a022726-13a4-469c-a44b-dac0f0405a31.png)

# Kotlin Hello World Program in Command line.

To write Kotlin program, we can use any text editor like: Notepad++. Put the following code into any text file and save.


```
fun main(args: Array<String>){  
    println("Hello World!")  
}  

```
Save the file with name hello.kt, .kt extension is used for Kotlin file.

# Compile Kotlin File

Open command prompt and go to directory location where file is stored. Compile hello.kt file with following command.

```
kotlinc hello.kt -include-runtime -d hello.jar  

```
![aa](https://user-images.githubusercontent.com/51777024/128831545-dd5e9184-92a7-4e0f-bb62-82bf6e1d0184.png)

#  Run Kotlin File

To run the Kotlin .jar (hello.jar) file run the following command.

```
java -jar hello.jar  

```
![bb](https://user-images.githubusercontent.com/51777024/128831796-f48d3829-e1c0-48c1-a144-ee8785af71c4.png)

# Kotlin First Program Concept

Let's understand the concepts and keywords of Kotlin program 'Hello World.kt'.

```
fun main(args: Array<String>) {  
    println("Hello World!")  
}  

```
1. The first line of program defines a function called main(). In Kotlin, function is a group of statements that performs a group of tasks. Functions start with a keyword fun followed by function name (main in this case).

The main () function takes an array of string (Array<String>) as a parameter and returns Unit. Unit is used to indicate the function and does not return any value (void as in Java). Declaring Unit is an optional, we do not declare it explicitly.

```
    fun main(args: Array<String>): Unit {  
//  
}

```
The main() function is the entry point of the program, it is called first when Kotlin program starts execution.

2. The second line used to print a String "Hello World!". To print standard output we use wrapper println() over standard Java library functions (System.out.println()).   
    
```
println("Hello World!")  
    
```
# Kotlin Environment Setup (IDE)
    
## Install JDK and Setup JDK path
    
Since, Kotlin runs on JVM, it is necessary to install JDK and setup the JDK and JRE path in local system environment variable. Use this link https://www.javatpoint.com/how-to-set-path-in-java to setup JDK path.

## Install IDE for Kotlin
    
There are various Java IDE available which supports Kotlin project development. We can choose these IDE according to our compatibility. The download links of these IDE's are given below.

IDE Name	    Download links
    
IntelliJ IDEA	https://www.jetbrains.com/idea/download/
    
Android Studio	https://developer.android.com/studio/preview/index.html
    
Eclipse     	https://www.eclipse.org/downloads/
    
In this tutorial, we are going to use IntelliJ IDEA for our Kotlin program development.

# Steps to Setup IntelliJ IDEA
    
1. Download IntelliJ IDEA.     
![cc](https://user-images.githubusercontent.com/51777024/128833129-d78d6ed5-8763-4930-a2a0-4da8a685a638.png)
2. Run the downloaded setup.    
![dd](https://user-images.githubusercontent.com/51777024/128833154-674da498-2090-40a6-a69b-81e5398e80c0.png)
3. Click next to continue   
![ee](https://user-images.githubusercontent.com/51777024/128833165-80a601fa-d078-469f-a507-498aafde7d75.png)
4. Choose installation location.    
![ff](https://user-images.githubusercontent.com/51777024/128833177-f1cd47bc-a390-4722-a7fd-df847bdb512d.png)
5. Choose start menu folder and click Install.    
![gg](https://user-images.githubusercontent.com/51777024/128833187-f4cddf4e-5651-45ac-a727-5a5d051a6033.png)
6. Click Finish to complete Installation.    
![hh](https://user-images.githubusercontent.com/51777024/128833220-2cc41cc2-a5f2-462b-bcd3-68b8656e7e97.png)
 
# Kotlin First Program Printing 'HelloWorld'
    
Let's create a Kotlin first example using IntelliJ IDEA IDE.

## Steps to Create First Example
    
1. Open IntelliJ IDEA and click on Create New Project'.    
![0](https://user-images.githubusercontent.com/51777024/128834074-14133645-89e0-42cb-9019-ac4c5f03b8f1.png)
    
2. Select Java option, provide project SDK path and mark check on Kotlin/JVM frameworks.    
![1](https://user-images.githubusercontent.com/51777024/128834081-1b6c6e35-8831-498d-ba9f-f231cb9cf9ea.png)
    
3. Provide the project details in new frame and click 'Finish'.    
![2](https://user-images.githubusercontent.com/51777024/128834088-31992d98-cc29-48c7-8ac7-053c40dcfcaf.png)
    
4. Create a new Kotlin file to run Kotlin first example. Go to src ->New->Kotlin File/Class.    
![3](https://user-images.githubusercontent.com/51777024/128834100-1756a31e-9378-4735-be91-33a8b5d4e976.png)
    
5. Enter the file name 'HelloWorld' and click 'OK'.    
![4](https://user-images.githubusercontent.com/51777024/128834128-af1b9997-f181-4457-8bc7-cec82aacbe02.png)
6. Write the following code in 'HelloWorld.kt' file. Kotlin files and classes are saved with ".kt" extension.
    
    
    fun main(args: Array<String>) {  
    println("Hello World!")  
}  
    
We will discuss the detail of this code later in upcoming tutorial.
    
![5](https://user-images.githubusercontent.com/51777024/128834149-02a45418-e9a2-4b1e-ad6d-899f8dcd2c82.png)
    
7. Now we can run this program by right clicking on file and select Run option.
    
![6](https://user-images.githubusercontent.com/51777024/128834164-2dff7c53-2301-470c-a035-b5280be14a3d.png)
    
 8. Finally, we got the output of program on console, displaying 'HelloWorld' message.   
    
![7](https://user-images.githubusercontent.com/51777024/128834176-0c7dff18-26e0-4de6-9dbe-4a44622b0874.png)
    
![8](https://user-images.githubusercontent.com/51777024/128834192-ccb44040-6c47-487d-8d23-a0b71f6261b4.png)
    
# Kotlin Variable
    
Variable refers to a memory location. It is used to store data. The data of variable can be changed and reused depending on condition or on information passed to the program.

# Variable Declaration
    
Kotlin variable is declared using keyword var and val.   

```
var language ="Java"  
val salary = 30000  
```    

The difference between var and val is specified later on this page.

Here, variable language is String type and variable salary is Int type. We don't require specifying the type of variable explicitly. Kotlin complier knows this by initilizer expression ("Java" is a String and 30000 is an Int value). This is called type inference in programming.    
We can also explicitly specify the type of variable while declaring it.    
    
```
var language: String ="Java"  
val salary: Int = 30000  
    
```
It is not necessary to initialize variable at the time of its declaration. Variable can be initialized later on when the program is executed.    
    
```
var language: String  
... ... ...  
language = "Java"  
val salary: Int  
... ... ...  
salary = 30000
    
``` 
# Difference between var and val

var (Mutable variable): We can change the value of variable declared using var keyword later in the program.
val (Immutable variable): We cannot change the value of variable which is declared using val keyword.

## Example    
    
```
var salary = 30000  
salary = 40000 //execute  
    
```
Here, the value of variable salary can be changed (from 30000 to 40000) because variable salary is declared using var keyword.    
    
```
val language = "Java"  
language = "Kotlin" //Error  
    
``` 
Here, we cannot re-assign the variable language from "Java" to "Kotlin" because the variable is declared using val keyword.

# Kotlin Data Type
    
Data type (basic type) refers to type and size of data associated with variables and functions. Data type is used for declaration of memory location of variable which determines the features of data.

In Kotlin, everything is an object, which means we can call member function and properties on any variable.

Kotlin built in data type are categorized as following different categories:

* Number
* Character
* Boolean
* Array
* String
    
# Number Types
    
Number types of data are those which hold only number type data variables. It is further categorized into different Integer and Floating point.    
 
Data Type	Bit Width (Size)	Data Range
Byte	    8 bit	            -128 to 127
Short	    16 bit	            -32768 to 32767
Int	        32 bit	            -2,147,483,648 to 2,147,483,647
Long	    64 bit	            -9,223,372,036,854,775,808 to +9,223,372,036,854,775,807
Float	    32 bit	             1.40129846432481707e-45 to 3.40282346638528860e+38
Double   	64 bit	             4.94065645841246544e-324 to 1.79769313486231570e+308

# Character (Char) Data Type    

Characters are represented using the keyword Char. Char types are declared using single quotes ('').   
    
Data Type	Bit Width (Size)	Data Range

Char      	4 bit	            -128 to 127    
    
## Example    
       
```
val value1 = 'A'  
//or  
val  value2: Char  
value2= 'A'  
    
```    
# Boolean Data Types
    
Boolean data is represented using the type Boolean. It contains values either true or false.

 Data Type	Bit Width (Size)	Data Value
 Boolean	1 bit	            true or false   
 
# Example    
    
```
val flag = true  
```
# Array
    
Arrays in Kotlin are represented by the Array class. Arrays are created using library function arrayOf() and Array() constructor. Array has get (), set() function, size property as well as some other useful member functions.

# Creating Array using library function arrayOf()
    
The arrayOf() function creates array of wrapper types. The item value are passed inside arrayOf() function like arrayOf(1,2,3) which creates an array[1,2,3].

The elements of array are accessed through their index values (array[index]). Array index are start from zero.    
    
```
val id = arrayOf(1,2,3,4,5)  
val firstId = id[0]  
val lasted = id[id.size-1]  
    
```
# Creating Array using Array() constructor

Creating array using Array() constructor takes two arguments in Array() constructor:
    
 # Kotlin Type Conversion

Type conversion is a process in which one data type variable is converted into another data type. In Kotlin, implicit conversion of smaller data type into larger data type is not supported (as it supports in java). For example Int cannot be assigned into Long or Double.

# In Java
```
int value1 = 10;  
long value2 = value1;  //Valid code 
    
```             
In Kotlin
 ```
var value1 = 10  
val value2: Long = value1  //Compile error, type mismatch  
    
``` 
However in Kotlin, conversion is done by explicit in which smaller data type is converted into larger data type and vice-versa. This is done by using helper function.

var value1 = 10  
val value2: Long = value1.toLong()  
The list of helper functions used for numeric conversion in Kotlin is given below:

* toByte()
* toShort()
* toInt()
* toLong()
* toFloat()
* toDouble()
* toChar()   
# Kotlin Type Conversion Example
    
Let see an example to convert from Int to Long.    
     
 ```
fun main(args : Array<String>) {  
    var value1 = 100  
    val value2: Long =value1.toLong()  
    println(value2)  
}  
```
We can also converse from larger data type to smaller data type.    
       
 ```
fun main(args : Array<String>) {  
    var value1: Long = 200  
    val value2: Int =value1.toInt()  
    println(value2)  
} 
    
```        
 # Kotlin Operator

Operators are special characters which perform operation on operands (values or variable).There are various kind of operators available in Kotlin.

* Arithmetic operator
* Relation operator
* Assignment operator
* Unary operator
* Bitwise operation
* Logical operator

# Arithmetic Operator
    
Arithmetic operators are used to perform basic mathematical operations such as 
* addition (+)  a+b	
* subtraction (-)  a-b
* multiplication (*)  a*b	  
* division (/) a/b
* Modulo (%)  a%b	
    
# Example of Arithmetic Operator    
    
 ```
fun main(args : Array<String>) {  
var a=10;  
var b=5;  
println(a+b);  
println(a-b);  
println(a*b);  
println(a/b);  
println(a%b);  
}  

```    
## Output:
* 15
* 5
* 50
* 2
* 0   
    
# Relation Operator
    
Relation operator shows the relation and compares between operands. Following are the different relational operators:    

Operator	Description	                      Expression	Translate to
>	        greater than	                    a>b	        a.compateTo(b)>0
<	        Less than	                        a<b	        a.compateTo(b)<0
>=	        greater than or equal to           	a>=b	    a.compateTo(b)>=0
<=      	less than or equal to	            a<=b	    a?.equals(b)?:(b===null)
==	        is equal to	                        a==b	    a?.equals(b)?:(b===null)
!=	        not equal to	                    a!=b	    !(a?.equals(b)?:(b===null))    
 
## Example of Relation Operator    
    
 ```
fun main(args : Array<String>) {  
    val a = 5  
    val b = 10  
    val max = if (a > b) {  
        println("a is greater than b.")  
        a  
    } else{  
        println("b is greater than a.")  
        b  
    }  
    println("max = $max")  
}  
    
```  
## Output:

* b is greater than a.
* max = 10

# Assignment operator
    
Assignment operator "=" is used to assign a value to another variable. The assignment of value takes from right to left.    
    
 Operator	Description	          Expression	Convert to
+=	        add and assign	        a+=b	   a.plusAssign(b)
-=	        subtract and assign  	a-=b	   a.minusAssign(b)
*=	        multiply and assign 	a*=b	   a.timesAssign(b)
/=	        divide and assign	    a/=b	   a.divAssign(b)
%=	        mod and assign	        a%=b	   a.remAssign(b)   
    
## Example of Assignment operator   

 ```
fun main(args : Array<String>) {  
  
    var a =20;var b=5  
    a+=b  
    println("a+=b :"+ a)  
    a-=b  
    println("a-=b :"+ a)  
    a*=b  
    println("a*=b :"+ a)  
    a/=b  
    println("a/=b :"+ a)  
    a%=b  
    println("a%=b :"+ a)  
  
}  
```   
## Output:

* a+=b :25
* a-=b :20
* a*=b :100
* a/=b :20
* a%=b :0

# Unary Operator
    
Unary operator is used with only single operand. Following are some unary operator given below.

Operator	Description  	Expression	Convert to
+	        unary plus	    +a	        a.unaryPlus()
-	        unary minus	    -a	        a.unaryMinus()
++	        increment by 1	++a	        a.inc()
--	        decrement by 1	--a	        a.dec()
!	        not	            !a	        a.not()

## Example of Unary Operator    
    
 ```
fun main(args: Array<String>){  
    var a=10  
    var b=5  
    var flag = true  
    println("+a :"+ +a)  
    println("-b :"+ -b)  
    println("++a :"+ ++a)  
    println("--b :"+ --b)  
    println("!flag :"+ !flag)  
}  
``` 
## Output:

* +a :10
* -b :-5
* ++a :11
* --b :4
* !flag :false   

# Logical Operator
    
Logical operators are used to check conditions between operands. List of logical operators are given below.

Operator	Description	                              Expression	Convert to
&&	        return true if all expression are true	(a>b) && (a>c)	(a>b) and (a>c)
||	        return true if any expression are true	(a>b) || (a>c)	(a>b) or(a>c)
!	        return complement of expression	        !a	             a.not()
 
    
## Example of Logical Operator    
    
 ```
fun main(args: Array<String>){  
    var a=10  
    var b=5  
    var c=15  
    var flag = false  
    var result: Boolean  
    result = (a>b) && (a>c)  
    println("(a>b) && (a>c) :"+ result)  
    result = (a>b) || (a>c)  
    println("(a>b) || (a>c) :"+ result)  
    result = !flag  
    println("!flag :"+ result)  
  
}  
``` 
## Output:

* (a>b) && (a>c) :false
* (a>b) || (a>c) :true
* !flag :true    

# Bitwise Operation
    
In Kotlin, there is not any special bitwise operator. Bitwise operation is done using named function.    
    
 Named Function	     Description	         Expression
shl (bits)	         signed shift left	     a.shl(b)
shr (bits)	         signed shift right	     a.shr(b)
ushr (bits)	         unsigned shift right	 a.ushr(b)
and (bits)	         bitwise and	         a.and(b)
or (bits)	         bitwise or	             a.or(b)
xor (bits)	         bitwise xor	         a.xor(b)
inv()	             bitwise inverse	     a.inv()   
    
## Example of Bitwise Operation
    
```
fun main(args: Array<String>){  
    var a=10  
    var b=2  
  
    println("a.shl(b): "+a.shl(b))  
    println("a.shr(b): "+a.shr(b))  
    println("a.ushr(b:) "+a.ushr(b))  
    println("a.and(b): "+a.and(b))  
    println("a.or(b): "+a.or(b))  
    println("a.xor(b): "+a.xor(b))  
    println("a.inv(): "+a.inv())  
  
} 
```  
## Output:

* a.shl(b): 40
* a.shr(b): 2
* a.ushr(b:) 2
* a.and(b): 2
* a.or(b): 10
* a.xor(b): 8
* a.inv(): -11

# Kotlin Classes and Objects
    
## Kotlin Classes/Objects

Everything in Kotlin is associated with classes and objects, along with its properties and functions. For example: in real life, a car is an object. The car has properties, such as brand, weight and color, and functions, such as drive and brake.

A Class is like an object constructor, or a "blueprint" for creating objects.
    
# Create a Class
    
To create a class, use the class keyword, and specify the name of the class:
    
## Example
    
Create a Car class along with some properties (brand, model and year)   
    
 ```
class Car {
  var brand = ""
  var model = ""
  var year = 0
}
``` 
# Create an Object
    
Now we can use the class named Car to create objects.

In the example below, we create an object of Car called c1, and then we access the properties of c1 by using the dot syntax (.), just like we did to access array and string properties:    
    
## Example   
```
// Create a c1 object of the Car class
val c1 = Car()

// Access the properties and add some values to it
c1.brand = "Ford"
c1.model = "Mustang"
c1.year = 1969

println(c1.brand)   // Outputs Ford
println(c1.model)   // Outputs Mustang
println(c1.year)    // Outputs 1969
``` 
## output  
* Ford
* Mustang
* 1969   
    
# Multiple Objects
    
You can create multiple objects of one class:

## Example
        
 ```
val c1 = Car()
c1.brand = "Ford"
c1.model = "Mustang"
c1.year = 1969

val c2 = Car()
c2.brand = "BMW"
c2.model = "X5"
c2.year = 1999

println(c1.brand)  // Ford
println(c2.brand)  // BMW
```
## output
* Ford
* BMW   
# Kotlin Class Functions
    
## Kotlin Class Functions
    
You can also use functions inside a class, to perfom certain actions:    

## Example
    
Create a drive() function inside the Car class and call it:
    
```
class Car(var brand: String, var model: String, var year: Int) {
  // Class function
  fun drive() {
    println("Wrooom!")
  }
}

fun main() {
  val c1 = Car("Ford", "Mustang", 1969)

  // Call the function
  c1.drive() 
}
```   
## Output    
* Ford Mustang 1969
* Wrooom!

# Class Function Parameters
    
Just like with regular functions, you can pass parameters to a class function:    
    
## Example
    
Create two functions: drive() and speed(), and pass parameters to the speed() function:    

 ```
class Car(var brand: String, var model: String, var year: Int) {
  // Class function
  fun drive() {
    println("Wrooom!")
  }

  // Class function with parameters
  fun speed(maxSpeed: Int) {
    println("Max speed is: " + maxSpeed)
  }
}

fun main() {
  val c1 = Car("Ford", "Mustang", 1969)

  // Call the functions
  c1.drive()
  c1.speed(200)
}
```
## Output
* Ford Mustang 1969
* Wrooom!
* Max speed is: 200   
    
    

```

```    

    
 ```

```    





