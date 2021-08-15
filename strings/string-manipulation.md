# String Manipulation

A string is a sequence of character.  Null character based terminated array of characters to store and manipulate strings are termed as _C Strings._ ANSI standard C++ introduces a new class called **string** which is an improvised version of C strings in several ways.

## C Style String

The C style string belongs to C language and continues to support in C++ also strings in C are the one-dimensional array of characters which gets terminated by \0 \(null character\). The C++ compiler automatically places the \0 at the end of the string when it initializes the array.

```cpp
char ch[6] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

### Manipulate Null String

* **strcpy\(str1, str2\)**: Copies string str2 into string str1.
* **strcat\(str1, str2\)**: Concatenates string str2 onto the end of string str1.
* **strlen\(str1\)**: Returns the length of string str1.
* **strcmp\(str1, str2\)**: Returns 0 if str1 and str2 are the same; less than 0 if str1&lt;str2; greater than 0 if str1&gt;str2.
* **strchr\(str1, ch\)**: Returns a pointer to the first occurrence of character ch in string str1.
* **strstr\(str1, str2\)**: Returns a pointer to the first occurrence of string str2 in string str1.

{% tabs %}
{% tab title="C++" %}
```cpp
Example of Above -> Navigate through Tabs
```
{% endtab %}

{% tab title="Code C++" %}
```cpp

```
{% endtab %}
{% endtabs %}

## String Class

The string class is huge and includes many constructors, member functions, and operators.

Programmers may use the constructors, operators and member functions to achieve the following:

* Creating string objects
* Reading string objects from keyboard
* Displaying string objects to the screen
* Finding a substring from a string
* Modifying string
* Adding objects of string
* Comparing strings
* Accessing characters of a string
* Obtaining the size or length of a string, etc...

### Functions Supported by String Class

* **append\(\)**: This function appends a part of a string to another string
* **assign\(\)**:This function assigns a partial string
* **at\(\)**: This function obtains the character stored at a specified location
* **begin\(\)**: This function returns a reference to the start of the string
* **capacity\(\)**: This function gives the total element that can be stored
* **compare\(\)**: This function compares a string against the invoking string
* **empty\(\)**: This function returns true if the string is empty
* **end\(\)**: This function returns a reference to the end of the string
* **erase\(\)**: This function removes character as specified
* **find\(\)**: This function searches for the occurrence of a specified substring
* **length\(\)**: It gives the size of a string or the number of elements of a string
* **swap\(\)**: This function swaps the given string with the invoking one

### Constructors obtained by String Class

* **String\(\)**: This constructor is used for creating an empty string
* **String\(const char \*str\)**: This constructor is used for creating string objects from a null-terminated string
* **String\(const string \*str\)**: This constructor is used for creating a string object from another string object

### Operations used By String Class

1. **=**: assignment
2. **+**: concatenation
3. **==**: Equality
4. **!=**: Inequality
5. **&lt;**: Less than
6. **&lt;=**: Less than or equal
7. **&gt;**: Greater than
8. **&gt;=**: Greater than or equal
9. **\[\]**: Subscription
10. **&lt;&lt;**: Output
11. **&gt;&gt;**: Input





