
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
    
   
    
    
```

```
















