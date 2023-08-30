<a name="readme-top"></a>
<div align="center">
   <h3 align="center">Kotlin Koans</h3>
   <p align="center"> Solution for 'Kotlin Koans' course from JetBrains s.r.o.</p>
</div>

<details>
  <summary>contents</summary>
  <ol>
    <!-- first part  -->
    <li><a href="#introduction">Introduction</a>
        <ul>
            <li><a href="#simple-functions">Simple Functions</a></li>
            <li><a href="#named-arguments">Named arguments</a></li>
        </ul>
    </li>
    <!-- second part  -->
    <li><a href="#classes">Classes</a>
    </li>
  </ol>
</details>

<a name="introduction"></a>
## Introduction
  ### Simple Functions
  <a name="simple-functions"></a>
  Check out the <a href="https://kotlinlang.org/docs/basic-syntax.html#functions">function syntax</a> and change the code to make the function start return the string "OK".
  ```Kotlin
  fun start(): String = TODO()
  ```

  * #### Solution
  ```Kotlin
  fun start() = "OK"
  ```
  ##
  
  ### Named arguments
  <a name="named-arguments"></a>
  Make the function `joinOptions()` return the list in a JSON format (for example, `[a, b, c]`) by specifying only two arguments.
  <a href="https://kotlinlang.org/docs/functions.html#default-arguments">Default and named</a> arguments help to minimize the number of overloads and improve the readability of the function invocation. The library function joinToString is declared with default values for parameters:
  ```Kotlin
  fun joinToString(
    separator: String = ", ",
    prefix: String = "",
    postfix: String = "",
    /* ... */
  ): String
  ```
  It can be called on a collection of Strings.
  
  * #### Solution
  ```Kotlin
  fun joinOptions(options: Collection<String>) = options.joinToString(prefix = "[", postfix = "]")
  ```
