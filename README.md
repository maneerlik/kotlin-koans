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
            <li><a href="#default-arguments">Default arguments</a></li>
            <li><a href="#triple-quoted-strings">Triple-quoted strings</a></li>
            <li><a href="#string-templates">String templates</a></li>
        </ul>
    </li>
    <!-- second part  -->
    <li><a href="#classes">Classes</a>
    </li>
  </ol>
</details>

<a name="introduction"></a>
## Introduction
  ### :label: Simple Functions
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
  
  ### :label: Named arguments
  <a name="named-arguments"></a>
  Make the function `joinOptions()` return the list in a JSON format (for example, `[a, b, c]`) by specifying only two arguments.
  <a href="https://kotlinlang.org/docs/functions.html#default-arguments">Default and named</a> arguments help to minimize the number of overloads and improve the readability of the function invocation. The library function <a href="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/join-to-string.html">`joinToString`</a> is declared with default values for parameters:
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
  ##

  ### :label: Default arguments
  <a name="default-arguments"></a>
  Imagine you have several overloads of 'foo()' in Java:
  ```Java
  public String foo(String name, int number, boolean toUpperCase) {
      return (toUpperCase ? name.toUpperCase() : name) + number;
  }
  public String foo(String name, int number) {
      return foo(name, number, false);
  }
  public String foo(String name, boolean toUpperCase) {
      return foo(name, 42, toUpperCase);
  }
  public String foo(String name) {
      return foo(name, 42);
  }
  ```
  You can replace all these Java overloads with one function in Kotlin. Change the declaration of the `foo` function in a way that makes the code using `foo` compile. Use <a href="https://kotlinlang.org/docs/functions.html#default-arguments">default and named</a> arguments.
  * #### Solution
  ```Kotlin
  fun foo(
      name: String,
      number: Int = 42,
      toUpperCase: Boolean = false
  ) = (if (toUpperCase) name.uppercase() else name) + number

  fun useFoo() = listOf(
      foo("a"),
      foo("b", number = 1),
      foo("c", toUpperCase = true),
      foo(name = "d", number = 2, toUpperCase = true)
  )
  ```
  ##

### :label: Triple-quoted strings
  <a name="triple-quoted-strings"></a>
  Learn about the <a href="https://kotlinlang.org/docs/strings.html#string-literals">different string literals and string templates</a> in Kotlin.

  You can use the handy library functions <a href="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/trim-indent.html">`trimIndent`</a> and <a href="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/trim-margin.html">`trimMargin`</a> to format multiline triple-quoted strings in accordance with the surrounding code.

  Replace the `trimIndent` call with the `trimMargin` call taking `#` as the prefix value so that the resulting string doesn't contain the prefix character.
  ```Kotlin
  const val question = "life, the universe, and everything"
  const val answer = 42

  val tripleQuotedString = """
      #question = "$question"
      #answer = $answer""".trimIndent()

  fun main() {
      println(tripleQuotedString)
  }
  ```
  * #### Solution
  ```Kotlin
  const val question = "life, the universe, and everything"
  const val answer = 42

  val tripleQuotedString = """
      #question = "$question"
      #answer = $answer""".trimMargin("#")

  fun main() {
      println(tripleQuotedString)
  }
  ```
  ##

  ### :label: Simple Functions
  <a href="#string-templates"></a>
  Triple-quoted strings are not only useful for multiline strings but also for creating regex patterns as you don't need to escape a backslash with a backslash.

  The following pattern matches a date in the format `13.06.1992` (two digits, a dot, two digits, a dot, four digits):
  
  ```Kotlin
  fun getPattern() = """\d{2}\.\d{2}\.\d{4}"""
  ```
  Using the `month` variable, rewrite this pattern in such a way that it matches the date in the format `13 JUN 1992` (two digits, one whitespace, a month abbreviation, one whitespace, four digits).
  ```Kotlin
  val month = "(JAN|FEB|MAR|APR|MAY|JUN|JUL|AUG|SEP|OCT|NOV|DEC)"
  fun getPattern(): String = TODO()
  ```
  * #### Solution
  ```Kotlin
  val month = "(JAN|FEB|MAR|APR|MAY|JUN|JUL|AUG|SEP|OCT|NOV|DEC)"
  fun getPattern() = """\d{2} $month \d{4}"""
  ```
  ##
