
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



```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
















