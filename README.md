<div align="center">
   <h1 align="center">
       <img src="https://github.com/devicons/devicon/blob/master/icons/kotlin/kotlin-original.svg" title="Kotlin" alt="Kotlin" width="26" height="26"/>otlin Koans
   </h1>
   <p align="center"><i>Solution for 'Kotlin Koans' course from JetBrains s.r.o.</i></p>
</div>

<a name="table-of-contents"></a>
### Table of Contents:
- [**Introduction**](#introduction)
	- [Simple Functions](#simple-functions)
	- [Named arguments](#named-arguments)
	- [Default arguments](#default-arguments)
	- [Triple-quoted strings](#triple-quoted-strings)
   	- [String templates](#string-templates)
  	- [Nullable types](#nullable-types)
  	- [Nothing type](#nothing-type)
  	- [Lambdas](#lambdas)
- [**Classes**](#classes)
	- [Data classes](#data-classes)
</br>

<a name="introduction"></a>
## Introduction

<a name="simple-functions"></a>
### Simple Functions
:label: Check out the <a href="https://kotlinlang.org/docs/basic-syntax.html#functions">function syntax</a> and change the code to make the function start return the string "OK".
```Kotlin
fun start(): String = TODO()
```
* #### Solution
```Kotlin
fun start() = "OK"
```
</br>
<p align="right"><a href="#table-of-contents">back to contents</a></p>

##

<a name="named-arguments"></a>
### Named arguments
:label: Make the function `joinOptions()` return the list in a JSON format (for example, `[a, b, c]`) by specifying only two arguments.

<a href="https://kotlinlang.org/docs/functions.html#default-arguments">Default and named</a> arguments help to minimize the number of overloads and improve the readability of the function invocation. The library function <a href="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/join-to-string.html">`joinToString()`</a> is declared with default values for parameters:
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
</br>
<p align="right"><a href="#table-of-contents">back to contents</a></p>

##

<a name="default-arguments"></a>
### Default arguments
:label: Imagine you have several overloads of `foo()` in Java:
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
You can replace all these Java overloads with one function in Kotlin. Change the declaration of the `foo()` function in a way that makes the code using `foo()` compile. Use <a href="https://kotlinlang.org/docs/functions.html#default-arguments">default and named</a> arguments.
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
</br>
<p align="right"><a href="#table-of-contents">back to contents</a></p>

##

<a name="triple-quoted-strings"></a>
### Triple-quoted strings
:label: Learn about the <a href="https://kotlinlang.org/docs/strings.html#string-literals">different string literals and string templates</a> in Kotlin. 

You can use the handy library functions <a href="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/trim-indent.html">`trimIndent()`</a> and <a href="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/trim-margin.html">`trimMargin()`</a> to format multiline triple-quoted strings in accordance with the surrounding code. 

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
</br>
<p align="right"><a href="#table-of-contents">back to contents</a></p>

##

<a href="string-templates"></a>
### String templates
:label: Triple-quoted strings are not only useful for multiline strings but also for creating regex patterns as you don't need to escape a backslash with a backslash. 

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
</br>
<p align="right"><a href="#table-of-contents">back to contents</a></p>

##

<a href="#nullable-types"></a>
### Nullable types
:label: Learn about <a href="https://kotlinlang.org/docs/null-safety.html">null safety and safe calls</a> in Kotlin and rewrite the following Java code so that it only has one `if` expression:
```Java
public void sendMessageToClient(@Nullable Client client, @Nullable String message, @NotNull Mailer mailer) {
    if (client == null || message == null) return;

    PersonalInfo personalInfo = client.getPersonalInfo();
    if (personalInfo == null) return;

    String email = personalInfo.getEmail();
    if (email == null) return;

    mailer.sendMessage(email, message);
}
```
* #### Solution
```Kotlin
fun sendMessageToClient(
	client: Client?,
	message: String?,
	mailer: Mailer
) {
    mailer.sendMessage(client?.personalInfo?.email?:return, message?:return)
}

class Client(val personalInfo: PersonalInfo?)

class PersonalInfo(val email: String?)

interface Mailer {
    fun sendMessage(email: String, message: String)
}
```
</br>
<p align="right"><a href="#table-of-contents">back to contents</a></p>

##

<a name="nothing-type"></a>
### Nothing type
:label: <a href="https://kotlinlang.org/docs/exceptions.html#the-nothing-type">Nothing type</a> can be used as a return type for a function that always throws an exception. When you call such a function, the compiler uses the information that the execution doesn't continue beyond the function.

Specify Nothing return type for the failWithWrongAge function. Note that without the Nothing type, the checkAge function doesn't compile because the compiler assumes the age can be `null`.
```Kotlin
import java.lang.IllegalArgumentException

fun failWithWrongAge(age: Int?) // GOTO {
    throw IllegalArgumentException("Wrong age: $age")
}

fun checkAge(age: Int?) {
    if (age == null || age !in 0..150) failWithWrongAge(age)
    println("Congrats! Next year you'll be ${age + 1}.")
}

fun main() {
    checkAge(10)
}
```
* #### Solution
```Kotlin
import java.lang.IllegalArgumentException

fun failWithWrongAge(age: Int?): Nothing {
    throw IllegalArgumentException("Wrong age: $age")
}

fun checkAge(age: Int?) {
    if (age == null || age !in 0..150) failWithWrongAge(age)
    println("Congrats! Next year you'll be ${age + 1}.")
}

fun main() {
    checkAge(10)
}
```
</br>
<p align="right"><a href="#table-of-contents">back to contents</a></p>

##

<a name="lambdas"></a>
### Lambdas
:label: Kotlin supports functional programming. Learn about <a href="https://kotlinlang.org/docs/lambdas.html#lambda-expressions-and-anonymous-functions">lambdas</a> in Kotlin.

Pass a lambda to the <a href="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/any.html">`any()`</a> function to check if the collection contains an even number. The any function gets a predicate as an argument and returns true if at least one element satisfies the predicate.
```Kotlin
fun containsEven(collection: Collection<Int>): Boolean = collection.any { TODO() }
```
* #### Solution
```Kotlin
fun containsEven(collection: Collection<Int>): Boolean = collection.any { it % 2 == 0 }
```
</br>
<p align="right"><a href="#table-of-contents">back to contents</a></p>

##

<a name="#classes"></a>
## Classes

<a name="data-classes"></a>
### Data classes
:label: Learn about <a href="https://kotlinlang.org/docs/classes.html">classes</a>, <a href="https://kotlinlang.org/docs/properties.html">properties</a> and <a href="https://kotlinlang.org/docs/data-classes.html">data classes</a> and then rewrite the following Java code to Kotlin:
```Java
public class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```
* #### Solution
```Kotlin
data class Person(val name: String, val age: Int)

fun getPeople(): List<Person> {
    return listOf(Person("Alice", 29), Person("Bob", 31))
}

fun comparePeople(): Boolean {
    val p1 = Person("Alice", 29)
    val p2 = Person("Alice", 29)
    return p1 == p2  // should be true
}
```
</br>
<p align="right"><a href="#table-of-contents">back to contents</a></p>
