# Operations and Search

| **Operations** |  |
| :--- | :--- |
| [clear](https://en.cppreference.com/w/cpp/string/basic_string/clear) | clears the contents |
| [insert](https://en.cppreference.com/w/cpp/string/basic_string/insert) | [inserts characters](./#insert) |
| [erase](https://en.cppreference.com/w/cpp/string/basic_string/erase) | [removes characters](./#erase) |
| [push\_back](https://en.cppreference.com/w/cpp/string/basic_string/push_back) | appends a character to the end |
| [pop\_back](https://en.cppreference.com/w/cpp/string/basic_string/pop_back)\(C++11\) | removes the last character \(equal to `erase(end()-1)`\) |
| [append](https://en.cppreference.com/w/cpp/string/basic_string/append) | [appends characters to the end](./#append) |
| [operator+=](https://en.cppreference.com/w/cpp/string/basic_string/operator%2B%3D) | [appends characters to the end](./#operator) |
| [compare](https://en.cppreference.com/w/cpp/string/basic_string/compare) | [compares two strings](./#compare) |
| [starts\_with](https://en.cppreference.com/w/cpp/string/basic_string/starts_with)\(C++20\) | [checks if the string starts with the given prefix](./#start_with-end_with) |
| [ends\_with](https://en.cppreference.com/w/cpp/string/basic_string/ends_with)\(C++20\) | checks if the string ends with the given suffix |
| [contains](https://en.cppreference.com/w/cpp/string/basic_string/contains)\(C++23\) | checks if the string contains the given substring or character |
| [replace](https://en.cppreference.com/w/cpp/string/basic_string/replace) | [replaces specified portion of a string](./#replace) |
| [substr](https://en.cppreference.com/w/cpp/string/basic_string/substr) | [returns a substring](./#substr) |
| [copy](https://en.cppreference.com/w/cpp/string/basic_string/copy) | [copies characters](./#copy) |
| [resize](https://en.cppreference.com/w/cpp/string/basic_string/resize) | [changes the number of characters stored](./#resize) |
| [swap](https://en.cppreference.com/w/cpp/string/basic_string/swap) | [swaps the contents](./#swap) |



| **Search** |  |
| :--- | :--- |
| [find](https://en.cppreference.com/w/cpp/string/basic_string/find) | find characters in the string |
| [rfind](https://en.cppreference.com/w/cpp/string/basic_string/rfind) | find the last occurrence of a substring |
| [find\_first\_of](https://en.cppreference.com/w/cpp/string/basic_string/find_first_of) | find first occurrence of characters |
| [find\_first\_not\_of](https://en.cppreference.com/w/cpp/string/basic_string/find_first_not_of) | find first absence of characters |
| [find\_last\_of](https://en.cppreference.com/w/cpp/string/basic_string/find_last_of) | find last occurrence of characters |
| [find\_last\_not\_of](https://en.cppreference.com/w/cpp/string/basic_string/find_last_not_of) | find last absence of characters |

## Operrations

### Insert

{% tabs %}
{% tab title="Code" %}
```cpp
#include <cassert>
#include <iterator>
#include <string>
#include <iostream>

using namespace std;
using namespace std::string_literals;

int main()
{
    string s = "xmplr";

    // insert(size_type index, size_type count, char ch)
    s.insert(0, 1, 'E');
    assert("Exmplr" == s);
    
    // insert(size_type index, const char* s)
    s.insert(2, "e");
    assert("Exemplr" == s);

    // insert(size_type index, string const& str)
    s.insert(6, "a"s);
    assert("Exemplar" == s);

    // insert(size_type index, string const& str,
    //     size_type index_str, size_type count)
    s.insert(8, " is an example string."s, 0, 14);
    assert("Exemplar is an example" == s);

    // insert(const_iterator pos, char ch)
    s.insert(s.cbegin() + s.find_first_of('n') + 1, ':');
    assert("Exemplar is an: example" == s);

    // insert(const_iterator pos, size_type count, char ch)
    s.insert(s.cbegin() + s.find_first_of(':') + 1, 2, '=');
    assert("Exemplar is an:== example" == s);

    // insert(const_iterator pos, InputIt first, InputIt last)
    {
        string seq = " string";
        s.insert(s.begin() + s.find_last_of('e') + 1,
                 begin(seq), end(seq));
        assert("Exemplar is an:== example string" == s);
    }

    // insert(const_iterator pos, initializer_list<char>)
    s.insert(s.cbegin() + s.find_first_of('g') + 1, { '.' });
    assert("Exemplar is an:== example string." == s);
}
```
{% endtab %}

{% tab title="Theory" %}
### **Parameters**

| index | position at which the content will be inserted |
| :--- | :--- |
| pos | iterator before which the characters will be inserted |
| ch | character to insert |
| count | number of characters to insert |
| s | pointer to the character string to insert |
| str | string to insert |
| first, last | range defining characters to insert |
| index\_str | position of the first character in the string `str` to insert |
| ilist | [std::initializer\_list](https://en.cppreference.com/w/cpp/utility/initializer_list) to insert the characters from |
| t | object \(convertible to [std::basic\_string\_view](https://en.cppreference.com/w/cpp/string/basic_string_view)\) to insert the characters from |

| Type requirements |  |
| :--- | :--- |
| -`InputIt` must meet the requirements of [LegacyInputIterator](https://en.cppreference.com/w/cpp/named_req/InputIterator). |  |

### Return value

11\) \*this

6-9\) An iterator which refers to the copy of the first inserted character or `pos` if no characters were inserted \(`count==0` or `first==last` or `ilist.size()==0`\)

### Exceptions

1-4, 10\) [std::out\_of\_range](https://en.cppreference.com/w/cpp/error/out_of_range) if index &gt; size\(\)

5\) Throws [std::out\_of\_range](https://en.cppreference.com/w/cpp/error/out_of_range) if index &gt; size\(\) or if index\_str &gt; str.size\(\).

11\) Throws [std::out\_of\_range](https://en.cppreference.com/w/cpp/error/out_of_range) if index &gt; size\(\) or if index\_str &gt; sv.size\(\).

In all cases, throws [std::length\_error](https://en.cppreference.com/w/cpp/error/length_error) if size\(\) + ins\_count &gt; max\_size\(\) where `ins_count` is the number of characters that will be inserted and may throw any exceptions thrown by `Allocator::allocate`.

Inserts characters into the string.

1\) Inserts `count` copies of character `ch` at the position `index`

2\) Inserts null-terminated character string pointed to by `s` at the position `index`. The length of the string is determined by the first null character using Traits::length\(s\).

3\) Inserts the characters in the range `[s, s+count)` at the position `index`. The range can contain null characters.

4\) Inserts string `str` at the position `index`

5\) Inserts a string, obtained by str.substr\(index\_str, count\) at the position `index`

6\) Inserts character `ch` before the character pointed by `pos`

7\) Inserts `count` copies of character `ch` before the element \(if any\) pointed by `pos`

8\) Inserts characters from the range `[first, last)` before the element \(if any\) pointed by `pos`. This overload does not participate in overload resolution if `InputIt` does not satisfy [LegacyInputIterator](https://en.cppreference.com/w/cpp/named_req/InputIterator). \(since C++11\)

9\) Inserts elements from initializer list `ilist` before the element \(if any\) pointed by `pos`

10\) Implicitly converts `t` to a string view `sv` as if by [std::basic\_string\_view](http://en.cppreference.com/w/cpp/string/basic_string_view)&lt;CharT, Traits&gt; sv = t;, then inserts the elements from `sv` before the element \(if any\) pointed by `pos`, as if by insert\(pos, sv.data\(\), sv.size\(\)\). This overload participates in overload resolution only if [std::is\_convertible\_v](http://en.cppreference.com/w/cpp/types/is_convertible)&lt;const T&, [std::basic\_string\_view](http://en.cppreference.com/w/cpp/string/basic_string_view)&lt;CharT, Traits&gt;&gt; is true and [std::is\_convertible\_v](http://en.cppreference.com/w/cpp/types/is_convertible)&lt;const T&, const CharT\*&gt; is false.

11\) Implicitly converts `t` to a string view `sv` as if by [std::basic\_string\_view](http://en.cppreference.com/w/cpp/string/basic_string_view)&lt;CharT, Traits&gt; sv = t;, then inserts, before the element \(if any\) pointed by `pos`, the characters from the subview `[index_str, index_str+count)` of `sv`. If the requested subview lasts past the end of `sv`, or if count == npos, the resulting subview is `[index_str, sv.size())`. If index\_str &gt; sv.size\(\), or if index &gt; size\(\), [std::out\_of\_range](https://en.cppreference.com/w/cpp/error/out_of_range) is thrown. This overload participates in overload resolution only if [std::is\_convertible\_v](http://en.cppreference.com/w/cpp/types/is_convertible)&lt;const T&, [std::basic\_string\_view](http://en.cppreference.com/w/cpp/string/basic_string_view)&lt;CharT, Traits&gt;&gt; is true and [std::is\_convertible\_v](http://en.cppreference.com/w/cpp/types/is_convertible)&lt;const T&, const CharT\*&gt; is false.
{% endtab %}

{% tab title="" %}


<table>
  <thead>
    <tr>
      <th style="text-align:left">(1)</th>
      <th style="text-align:left">+basic_string&amp; insert( size_type index, size_type count, CharT ch
        );</th>
      <th style="text-align:left">(until C++20)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">constexpr basic_string&amp; insert( size_type index, size_type count,
        CharT ch );</td>
      <td style="text-align:left">(since C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">(2)</td>
      <td style="text-align:left">basic_string&amp; insert( size_type index, const CharT* s );</td>
      <td style="text-align:left">(until C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">constexpr basic_string&amp; insert( size_type index, const CharT* s );</td>
      <td
      style="text-align:left">(since C++20</td>
    </tr>
    <tr>
      <td style="text-align:left">(3)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">basic_string&amp; insert( size_type index, const CharT* s, size_type count
        );</td>
      <td style="text-align:left">(until C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">constexpr basic_string&amp; insert( size_type index,
        <br />const CharT* s, size_type count );</td>
      <td style="text-align:left">(since C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left">(4)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">basic_string&amp; insert( size_type index, const basic_string&amp; str
        );</td>
      <td style="text-align:left">(until C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">constexpr basic_string&amp; insert( size_type index, const basic_string&amp;
        str );</td>
      <td style="text-align:left">(since C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left">(5)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">basic_string&amp; insert( size_type index, const basic_string&amp; str,
        <br
        />size_type index_str, size_type count );</td>
      <td style="text-align:left">(until C++14)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">basic_string&amp; insert( size_type index, const basic_string&amp; str,
        <br
        />size_type index_str, size_type count = npos);</td>
      <td style="text-align:left">(since C++14)
        <br />(until C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">constexpr basic_string&amp; insert( size_type index, const basic_string&amp;
        str,
        <br />size_type index_str, size_type count = npos);</td>
      <td style="text-align:left">(since C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left">(6)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">iterator insert( iterator pos, CharT ch );</td>
      <td style="text-align:left">(until C++11)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">iterator insert( const_iterator pos, CharT ch );</td>
      <td style="text-align:left">(since C++11)
        <br />(until C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">constexpr iterator insert( const_iterator pos, CharT ch );</td>
      <td style="text-align:left">(since C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left">(7)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">void insert( iterator pos, size_type count, CharT ch );</td>
      <td style="text-align:left">(until C++11)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">iterator insert( const_iterator pos, size_type count, CharT ch );</td>
      <td
      style="text-align:left">(since C++11)
        <br />(until C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">constexpr iterator insert( const_iterator pos, size_type count, CharT
        ch );</td>
      <td style="text-align:left">(since C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left">(8)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">template&lt; class InputIt &gt;
        <br />void insert( iterator pos, InputIt first, InputIt last );</td>
      <td style="text-align:left">(until C++11)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">template&lt; class InputIt &gt;
        <br />iterator insert( const_iterator pos, InputIt first, InputIt last );</td>
      <td
      style="text-align:left">(since C++11)
        <br />(until C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">template&lt; class InputIt &gt;
        <br />constexpr iterator insert( const_iterator pos, InputIt first, InputIt
        last );</td>
      <td style="text-align:left">(since C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left">(9)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">iterator insert( const_iterator pos, <a href="http://en.cppreference.com/w/cpp/utility/initializer_list">std::initializer_list</a>&lt;CharT&gt;
        ilist );</td>
      <td style="text-align:left">(since C++11)
        <br />(until C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">constexpr iterator insert( const_iterator pos,
        <br /> <a href="http://en.cppreference.com/w/cpp/utility/initializer_list">std::initializer_list</a>&lt;CharT&gt;
        ilist );</td>
      <td style="text-align:left">(since C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left">(10)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">template &lt; class T &gt;
        <br />basic_string&amp; insert( size_type pos, const T&amp; t );</td>
      <td style="text-align:left">(since C++17)
        <br />(until C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">template &lt; class T &gt;
        <br />constexpr basic_string&amp; insert( size_type pos, const T&amp; t );</td>
      <td
      style="text-align:left">(since C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left">(11)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>template &lt; class T &gt;
          <br />
        </p>
        <p>basic_string&amp; insert( size_type index, const T&amp; t,
          <br />size_type index_str, size_type count = npos);</p>
      </td>
      <td style="text-align:left">(since C++17)
        <br />(until C++20)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>template &lt; class T &gt;
          <br />
        </p>
        <p>constexpr basic_string&amp; insert( size_type index, const T&amp; t,
          <br
          />size_type index_str, size_type count = npos);</p>
      </td>
      <td style="text-align:left">(since C++20)</td>
    </tr>
  </tbody>
</table>
{% endtab %}
{% endtabs %}

### Erase

{% tabs %}
{% tab title="First Tab" %}
```cpp
#include <iostream>
#include <algorithm>
#include <string>
 
int main()
{
    std::string s = "This is an example";
    std::cout << s << '\n';
 
    s.erase(0, 5); // Erase "This "
    std::cout << s << '\n';
 
    s.erase(std::find(s.begin(), s.end(), ' ')); // Erase ' '
    std::cout << s << '\n';
 
    s.erase(s.find(' ')); // Trim from ' ' to the end of the string
    std::cout << s << '\n';
}

//This is an example
//is an example
//isan example
//isan
```
{% endtab %}

{% tab title="Second Tab" %}
#### Parameters

| index | - | first character to remove |
| :--- | :--- | :--- |
| count | - | number of characters to remove |
| position | - | iterator to the character to remove |
| first, last | - | range of the characters to remove |

#### Return value

1\) \*this2\) iterator pointing to the character immediately following the character erased, or `end()` if no such character exists3\) iterator pointing to the character `last` pointed to before the erase, or `end()` if no such character exists

#### Exceptions

1\) [std::out\_of\_range](https://en.cppreference.com/w/cpp/error/out_of_range) if index &gt; size\(\).2-3\) Throws nothing.

In any case, if an exception is thrown for any reason, this function has no effect \(strong exception guarantee\). \(since C++11\)
{% endtab %}

{% tab title="" %}


| basic\_string& erase\( size\_type index = 0, size\_type count = npos \); | \(until C++20\) |  |
| :--- | :--- | :--- |
| constexpr basic\_string& erase\( size\_type index = 0, size\_type count = npos \); | \(since C++20\) |  |
|  | \(2\) |  |
| iterator erase\( iterator position \); | \(until C++11\) |  |
| iterator erase\( const\_iterator position \); | \(since C++11\) \(until C++20\) |  |
| constexpr iterator erase\( const\_iterator position \); | \(since C++20\) |  |
|  | \(3\) |  |
| iterator erase\( iterator first, iterator last \); | \(until C++11\) |  |
| iterator erase\( const\_iterator first, const\_iterator last \); | \(since C++11\) \(until C++20\) |  |
| constexpr iterator erase\( const\_iterator first, const\_iterator last \); | \(since C++20\) |  |
|  |  |  |

Removes specified characters from the string.1\) Removes min\(`count`, [size\(\)](https://en.cppreference.com/w/cpp/string/basic_string/size) `- index`\) characters starting at `index`.2\) Removes the character at `position`.3\) Removes the characters in the range `[first, last)`.
{% endtab %}
{% endtabs %}

### append

{% tabs %}
{% tab title="C++" %}
```cpp
std::basic_string<char> str = "string";
const char* cptr = "C-string";
const char carr[] = "Two and one";

string output;

// 1) Append a char 3 times.
// Notice, this is the only overload accepting chars.
output.append(3, '*');
//***

//  2) Append a whole string
output.append(str);
//***string

// 3) Append part of a string (last 3 letters, in this case)
output.append(str, 3, 3);
//***stringing

// 4) Append part of a C-string
// Notice, because `append` returns *this, we can chain calls together
output.append(1, ' ').append(carr, 4);
//***stringing Two

// 5) Append a whole C-string
output.append(cptr);
//***stringing Two C-string

// 6) Append range
output.append(&carr[3], std::end(carr));
//***stringing Two C-string and one

// 7) Append initializer list
output.append({ ' ', 'l', 'i', 's', 't' });
//***stringing Two C-string and one  list

```
{% endtab %}

{% tab title="Code" %}
```cpp
std::basic_string<char> str = "string";
const char* cptr = "C-string";
const char carr[] = "Two and one";

string output;

// 1) Append a char 3 times.
// Notice, this is the only overload accepting chars.
output.append(3, '*');
//***

//  2) Append a whole string
output.append(str);
//***string

// 3) Append part of a string (last 3 letters, in this case)
output.append(str, 3, 3);
//***stringing

// 4) Append part of a C-string
// Notice, because `append` returns *this, we can chain calls together
output.append(1, ' ').append(carr, 4);
//***stringing Two

// 5) Append a whole C-string
output.append(cptr);
//***stringing Two C-string

// 6) Append range
output.append(&carr[3], std::end(carr));
//***stringing Two C-string and one

// 7) Append initializer list
output.append({ ' ', 'l', 'i', 's', 't' });
//***stringing Two C-string and one  list

```
{% endtab %}

{% tab title="" %}
#### Parameters

| count | - | number of characters to append |
| :--- | :--- | :--- |
| pos | - | the index of the first character to append |
| ch | - | character value to append |
| first, last | - | range of characters to append |
| str | - | string to append |
| s | - | pointer to the character string to append |
| ilist | - | initializer list with the characters to append |
| t | - | object convertible to [std::basic\_string\_view](https://en.cppreference.com/w/cpp/string/basic_string_view) with the characters to append |

#### Return value

\*this

#### Complexity

There are no standard complexity guarantees, typical implementations behave similar to [std::vector::insert](https://en.cppreference.com/w/cpp/container/vector/insert).

#### Exceptions

If an exception is thrown for any reason, this function has no effect \(strong exception guarantee\). \(since C++11\)

If the operation would result in `size() > max_size()`, throws [std::length\_error](https://en.cppreference.com/w/cpp/error/length_error).
{% endtab %}

{% tab title="" %}
<table>
  <thead>
    <tr>
      <th style="text-align:left">basic_string&amp; append( size_type count, CharT ch );</th>
      <th style="text-align:left">(until C++20)</th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">constexpr basic_string&amp; append( size_type count, CharT ch );</td>
      <td
      style="text-align:left">(since C++20)</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">(2)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">basic_string&amp; append( const basic_string&amp; str );</td>
      <td style="text-align:left">(until C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">constexpr basic_string&amp; append( const basic_string&amp; str );</td>
      <td
      style="text-align:left">(since C++20)</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">(3)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">basic_string&amp; append( const basic_string&amp; str,
        <br />size_type pos, size_type count );</td>
      <td style="text-align:left">(until C++14)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">basic_string&amp; append( const basic_string&amp; str,
        <br />size_type pos, size_type count = npos );</td>
      <td style="text-align:left">(since C++14)
        <br />(until C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">constexpr basic_string&amp; append( const basic_string&amp; str,
        <br />size_type pos, size_type count = npos );</td>
      <td style="text-align:left">(since C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">(4)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">basic_string&amp; append( const CharT* s, size_type count );</td>
      <td style="text-align:left">(until C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">constexpr basic_string&amp; append( const CharT* s, size_type count );</td>
      <td
      style="text-align:left">(since C++20)</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">(5)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">basic_string&amp; append( const CharT* s );</td>
      <td style="text-align:left">(until C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">constexpr basic_string&amp; append( const CharT* s );</td>
      <td style="text-align:left">(since C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">(6)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">template&lt; class InputIt &gt;
        <br />basic_string&amp; append( InputIt first, InputIt last );</td>
      <td style="text-align:left">(until C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">template&lt; class InputIt &gt;
        <br />constexpr basic_string&amp; append( InputIt first, InputIt last );</td>
      <td
      style="text-align:left">(since C++20)</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">(7)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">basic_string&amp; append( <a href="http://en.cppreference.com/w/cpp/utility/initializer_list">std::initializer_list</a>&lt;CharT&gt;
        ilist );</td>
      <td style="text-align:left">(since C++11)
        <br />(until C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">constexpr basic_string&amp; append( <a href="http://en.cppreference.com/w/cpp/utility/initializer_list">std::initializer_list</a>&lt;CharT&gt;
        ilist );</td>
      <td style="text-align:left">(since C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">(8)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">template &lt; class T &gt;
        <br />basic_string&amp; append( const T&amp; t );</td>
      <td style="text-align:left">(since C++17)
        <br />(until C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">template &lt; class T &gt;
        <br />constexpr basic_string&amp; append( const T&amp; t );</td>
      <td style="text-align:left">(since C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">(9)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template &lt; class T &gt;
          <br />
        </p>
        <p>basic_string&amp; append( const T&amp; t,
          <br />size_type pos, size_type count = npos );</p>
      </td>
      <td style="text-align:left">(since C++17)
        <br />(until C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template &lt; class T &gt;
          <br />
        </p>
        <p>constexpr basic_string&amp; append( const T&amp; t,
          <br />size_type pos, size_type count = npos );</p>
      </td>
      <td style="text-align:left">(since C++20)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

Appends additional characters to the string.1\) Appends `count` copies of character `ch`2\) Appends string `str`3\) Appends a substring `[pos, pos+count)` of `str`. If the requested substring lasts past the end of the string, or if count == npos, the appended substring is `[pos, size())`. If pos &gt; str.size\(\), [std::out\_of\_range](https://en.cppreference.com/w/cpp/error/out_of_range) is thrown.4\) Appends characters in the range `[s, s + count)`. This range can contain null characters.5\) Appends the null-terminated character string pointed to by `s`. The length of the string is determined by the first null character using Traits::length\(s\).6\) Appends characters in the range `[first, last)`.

| This overload has the same effect as overload \(1\) if `InputIt` is an integral type. | \(until C++11\) |
| :--- | :--- |
| This overload only participates in overload resolution if `InputIt` qualifies as an [LegacyInputIterator](https://en.cppreference.com/w/cpp/named_req/InputIterator) | \(since C++11\) |

7\) Appends characters from the initializer list `ilist`.8\) Implicitly converts `t` to a string view `sv` as if by [std::basic\_string\_view](http://en.cppreference.com/w/cpp/string/basic_string_view)&lt;CharT, Traits&gt; sv = t;, then appends all characters from `sv` as if by append\(sv.data\(\), sv.size\(\)\). This overload participates in overload resolution only if [std::is\_convertible\_v](http://en.cppreference.com/w/cpp/types/is_convertible)&lt;const T&, [std::basic\_string\_view](http://en.cppreference.com/w/cpp/string/basic_string_view)&lt;CharT, Traits&gt;&gt; is true and [std::is\_convertible\_v](http://en.cppreference.com/w/cpp/types/is_convertible)&lt;const T&, const CharT\*&gt; is false.9\) Implicitly converts `t` to a string view `sv` as if by [std::basic\_string\_view](http://en.cppreference.com/w/cpp/string/basic_string_view)&lt;CharT, Traits&gt; sv = t;, then appends the characters from the subview `[pos, pos+count)` of `sv`. If the requested subview extends past the end of `sv`, or if count == npos, the appended subview is `[pos, sv.size())`. If pos &gt;= sv.size\(\), [std::out\_of\_range](https://en.cppreference.com/w/cpp/error/out_of_range) is thrown. This overload participates in overload resolution only if [std::is\_convertible\_v](http://en.cppreference.com/w/cpp/types/is_convertible)&lt;const T&, [std::basic\_string\_view](http://en.cppreference.com/w/cpp/string/basic_string_view)&lt;CharT, Traits&gt;&gt; is true and [std::is\_convertible\_v](http://en.cppreference.com/w/cpp/types/is_convertible)&lt;const T&, const CharT\*&gt; is false.
{% endtab %}
{% endtabs %}

### Operator +=

```cpp
#include <iostream>
#include <iomanip>
#include <string>
 
int main()
{
   std::string str;
   str.reserve(50); //reserves sufficient storage space to avoid memory reallocation
   std::cout << std::quoted(str) << '\n'; //empty string
 
   str += "This";
   std::cout << std::quoted(str) << '\n';
 
   str += std::string(" is ");
   std::cout << std::quoted(str) << '\n';
 
   str += 'a';
   std::cout << std::quoted(str) << '\n';
 
   str += {' ','s','t','r','i','n','g','.'};
   std::cout << std::quoted(str) << '\n';
 
   str += 76.85; // equivalent to str += static_cast<char>(76.85), might not be the intent
   std::cout << std::quoted(str) << '\n';
}
```

### Compare

Lexographic Order

{% hint style="info" %}
-1 0  9 A S a s                   is in Lexographic Order
{% endhint %}

We can use `(str1 < str 2)` ,`(str1 > str 2),(str1 == str 2)`instead of this.

{% tabs %}
{% tab title="C++" %}
```cpp
#include <cassert>

    // 1) Compare with other string
    {
        int compare_value{
            std::string{"Batman"}.compare(std::string{"Superman"})
        };
        //Batman comes before Superman
    }
 
    // 2) Compare substring with other string
    {
        int compare_value{
            std::string{"Batman"}.compare(3, 3, std::string{"Superman"})
        };
        std::cout << (
            compare_value < 0 ? "man comes before Superman\n" :
            compare_value > 0 ? "Superman comes before man\n" :
            "man and Superman are the same.\n"
        );
    }
 
    // 3) Compare substring with other substring
    {
        std::string a{"Batman"};
        std::string b{"Superman"};
 
        int compare_value{a.compare(3, 3, b, 5, 3)};
 
        std::cout << (
            compare_value < 0 ? "man comes before man\n" :
            compare_value > 0 ? "man comes before man\n" :
            "man and man are the same.\n"
        );
        // Compare substring with other substring
        // defaulting to end of other string
        assert(compare_value == a.compare(3, 3, b, 5));
    }
 
    // 4) Compare with char pointer
    {
        int compare_value{std::string{"Batman"}.compare("Superman")};
 
        std::cout << (
            compare_value < 0 ? "Batman comes before Superman\n" :
            compare_value > 0 ? "Superman comes before Batman\n" :
            "Superman and Batman are the same.\n"
        );
    }
 
    // 5) Compare substring with char pointer
    {
        int compare_value{std::string{"Batman"}.compare(3, 3, "Superman")};
 
        std::cout << (
            compare_value < 0 ? "man comes before Superman\n" :
            compare_value > 0 ? "Superman comes before man\n" :
            "man and Superman are the same.\n"
        );
    }
 
    // 6) Compare substring with char pointer substring
    {
        int compare_value{std::string{"Batman"}.compare(0, 3, "Superman", 5)};
 
        std::cout << (
            compare_value < 0 ? "Bat comes before Super\n" :
            compare_value > 0 ? "Super comes before Bat\n" :
            "Super and Bat are the same.\n"
        );
    }
}

//Batman comes before Superman
//Superman comes before man
//man and man are the same.
//Batman comes before Superman
//Superman comes before man
//Bat comes before Super
```
{% endtab %}

{% tab title="Code" %}
```cpp
#include <cassert>
#include <string>
#include <iostream>
 
int main() 
{
    // 1) Compare with other string
    {
        int compare_value{
            std::string{"Batman"}.compare(std::string{"Superman"})
        };
        std::cout << (
            compare_value < 0 ? "Batman comes before Superman\n" :
            compare_value > 0 ? "Superman comes before Batman\n" :
            "Superman and Batman are the same.\n"
        );
    }
 
    // 2) Compare substring with other string
    {
        int compare_value{
            std::string{"Batman"}.compare(3, 3, std::string{"Superman"})
        };
        std::cout << (
            compare_value < 0 ? "man comes before Superman\n" :
            compare_value > 0 ? "Superman comes before man\n" :
            "man and Superman are the same.\n"
        );
    }
 
    // 3) Compare substring with other substring
    {
        std::string a{"Batman"};
        std::string b{"Superman"};
 
        int compare_value{a.compare(3, 3, b, 5, 3)};
 
        std::cout << (
            compare_value < 0 ? "man comes before man\n" :
            compare_value > 0 ? "man comes before man\n" :
            "man and man are the same.\n"
        );
        // Compare substring with other substring
        // defaulting to end of other string
        assert(compare_value == a.compare(3, 3, b, 5));
    }
 
    // 4) Compare with char pointer
    {
        int compare_value{std::string{"Batman"}.compare("Superman")};
 
        std::cout << (
            compare_value < 0 ? "Batman comes before Superman\n" :
            compare_value > 0 ? "Superman comes before Batman\n" :
            "Superman and Batman are the same.\n"
        );
    }
 
    // 5) Compare substring with char pointer
    {
        int compare_value{std::string{"Batman"}.compare(3, 3, "Superman")};
 
        std::cout << (
            compare_value < 0 ? "man comes before Superman\n" :
            compare_value > 0 ? "Superman comes before man\n" :
            "man and Superman are the same.\n"
        );
    }
 
    // 6) Compare substring with char pointer substring
    {
        int compare_value{std::string{"Batman"}.compare(0, 3, "Superman", 5)};
 
        std::cout << (
            compare_value < 0 ? "Bat comes before Super\n" :
            compare_value > 0 ? "Super comes before Bat\n" :
            "Super and Bat are the same.\n"
        );
    }
}

//Batman comes before Superman
//Superman comes before man
//man and man are the same.
//Batman comes before Superman
//Superman comes before man
//Bat comes before Super
```
{% endtab %}

{% tab title="Link" %}
{% embed url="https://www.geeksforgeeks.org/comparing-two-strings-cpp/" %}

{% embed url="https://en.cppreference.com/w/cpp/string/basic\_string/compare" %}
{% endtab %}
{% endtabs %}

### start\_with , end\_with

{% tabs %}
{% tab title="start\_with" %}
```cpp
#include <iostream>
#include <string_view>
#include <string>
 
template <typename PrefixType>
void test_prefix_print(const std::string& str, PrefixType prefix)
{
    std::cout << '\'' << str << "' starts with '" << prefix << "': " <<
        str.starts_with(prefix) << '\n';
}
 
int main()
{
    std::boolalpha(std::cout);    
    auto helloWorld = std::string("hello world");
 
    test_prefix_print(helloWorld, std::string_view("hello"));
 
    test_prefix_print(helloWorld, std::string_view("goodbye"));
 
    test_prefix_print(helloWorld, 'h');
 
    test_prefix_print(helloWorld, 'x');
}
```
{% endtab %}

{% tab title="end\_with" %}
```cpp
#include <iostream>
#include <string_view>
#include <string>
 
template <typename SuffixType>
void test_suffix_print(const std::string& str, SuffixType suffix)
{
    std::cout << '\'' << str << "' ends with '" << suffix << "': " <<
        str.ends_with(suffix) << '\n';
}
 
int main()
{
    std::boolalpha(std::cout);    
    auto helloWorld = std::string("hello world");
 
    test_suffix_print(helloWorld, std::string_view("world"));
 
    test_suffix_print(helloWorld, std::string_view("goodbye"));
 
    test_suffix_print(helloWorld, 'd');
 
    test_suffix_print(helloWorld, 'x');
}
```
{% endtab %}

{% tab title="contains" %}
```cpp
#include <iostream>
#include <string_view>
#include <string>
 
template <typename SubstrType>
void test_substring_print(const std::string& str, SubstrType subs)
{
    std::cout << '\'' << str << "' contains '" << subs << "': " <<
        str.contains(subs) << '\n';
}
 
int main()
{
    std::boolalpha(std::cout);    
    auto helloWorld = std::string("hello world");
 
    test_substring_print(helloWorld, std::string_view("hello"));
 
    test_substring_print(helloWorld, std::string_view("goodbye"));
 
    test_substring_print(helloWorld, 'w');
 
    test_substring_print(helloWorld, 'x');
}
```
{% endtab %}
{% endtabs %}

### Replace

{% tabs %}
{% tab title="" %}
```

```
{% endtab %}

{% tab title="Code" %}
```cpp
#include <cassert>
#include <cstddef>
#include <iostream>
#include <string>
#include <string_view>
 
std::size_t replace_all(std::string& inout, std::string_view what, std::string_view with);
std::size_t remove_all(std::string& inout, std::string_view what);
void test_replace_remove_all();
 
int main()
{
    std::string str{"The quick brown fox jumps over the lazy dog."};
 
    str.replace(10, 5, "red"); // (5)
 
    str.replace(str.begin(), str.begin() + 3, 1, 'A'); // (6)
 
    std::cout << str << "\n\n";
 
    test_replace_remove_all();
}
 
 
std::size_t replace_all(std::string& inout, std::string_view what, std::string_view with)
{
    std::size_t count{};
    for (std::string::size_type pos{};
         inout.npos != (pos = inout.find(what.data(), pos, what.length()));
         pos += with.length(), ++count) {
        inout.replace(pos, what.length(), with.data(), with.length());
    }
    return count;
}
 
std::size_t remove_all(std::string& inout, std::string_view what) {
    return replace_all(inout, what, "");
}
 
void test_replace_remove_all()
{
    std::string str2{"ftp: ftpftp: ftp:"};
    std::cout << "#1 " << str2 << '\n';
 
    auto count = replace_all(str2, "ftp", "http");
    assert(count == 4);
    std::cout << "#2 " << str2 << '\n';
 
    count = replace_all(str2, "ftp", "http");
    assert(count == 0);
    std::cout << "#3 " << str2 << '\n';
 
    count = remove_all(str2, "http");
    assert(count == 4);
    std::cout << "#4 " << str2 << '\n';
}
```
{% endtab %}

{% tab title="Second Tab" %}
#### Parameters

| pos | - | start of the substring that is going to be replaced |
| :--- | :--- | :--- |
| count | - | length of the substring that is going to be replaced |
| first, last | - | range of characters that is going to be replaced |
| str | - | string to use for replacement |
| pos2 | - | start of the substring to replace with |
| count2 | - | number of characters to replace with |
| cstr | - | pointer to the character string to use for replacement |
| ch | - | character value to use for replacement |
| first2, last2 | - | range of characters to use for replacement |
| ilist | - | initializer list with the characters to use for replacement |
| t | - | object \(convertible to [std::basic\_string\_view](https://en.cppreference.com/w/cpp/string/basic_string_view)\) with the characters to use for replacement |

#### Return value

\*this.

#### Exceptions

* [std::out\_of\_range](https://en.cppreference.com/w/cpp/error/out_of_range) if `pos > length()` or `pos2 > str.length()`
* [std::length\_error](https://en.cppreference.com/w/cpp/error/length_error) if the resulting string will exceed maximum possible string length \([max\_size\(\)](https://en.cppreference.com/w/cpp/string/basic_string/max_size)\)

In any case, if an exception is thrown for any reason, this function has no effect \(strong exception guarantee\). \(since C++11\)
{% endtab %}
{% endtabs %}

### substr

{% tabs %}
{% tab title="First Tab" %}
```cpp
#include <string>
#include <iostream>
 
int main()
{
    std::string a = "0123456789abcdefghij";
 
    // count is npos, returns [pos, size())
    std::string sub1 = a.substr(10);
    std::cout << sub1 << '\n';
 
    // both pos and pos+count are within bounds, returns [pos, pos+count)
    std::string sub2 = a.substr(5, 3);
    std::cout << sub2 << '\n';
 
    // pos is within bounds, pos+count is not, returns [pos, size()) 
    std::string sub4 = a.substr(a.size()-3, 50);
    // this is effectively equivalent to
    // std::string sub4 = a.substr(17, 3);
    // since a.size() == 20, pos == a.size()-3 == 17, and a.size()-pos == 3
 
    std::cout << sub4 << '\n';
 
    try {
        // pos is out of bounds, throws
        std::string sub5 = a.substr(a.size()+3, 50);
        std::cout << sub5 << '\n';
    } catch(const std::out_of_range& e) {
        std::cout << "pos exceeds string size\n";
    }
}
```
{% endtab %}

{% tab title="Second Tab" %}
Returns a substring `[pos, pos+count)`. If the requested substring extends past the end of the string, i.e. the `count` is greater than size\(\) - pos \(e.g. if count == npos\), the returned substring is `[pos,` [`size()`](https://en.cppreference.com/w/cpp/string/basic_string/size)`)`.

#### Parameters

| pos | - | position of the first character to include |
| :--- | :--- | :--- |
| count | - | length of the substring |

#### Return value

String containing the substring `[pos, pos+count)` or `[pos,` [`size()`](https://en.cppreference.com/w/cpp/string/basic_string/size)`)`.

#### Exceptions

[std::out\_of\_range](https://en.cppreference.com/w/cpp/error/out_of_range) if `pos >` [`size()`](https://en.cppreference.com/w/cpp/string/basic_string/size)

#### Complexity

Linear in `count`

#### Notes

The returned string is constructed as if by basic\_string\(data\(\)+pos, count\), which implies that the returned string's allocator will be default-constructed — the new allocator might not be a copy of `this->`[`get_allocator()`](https://en.cppreference.com/w/cpp/string/basic_string/get_allocator).

| basic\_string substr\( size\_type pos = 0, size\_type count = npos \) const; |  | \(until C++20\) |
| :--- | :--- | :--- |
| constexpr basic\_string substr\( size\_type pos = 0, size\_type count = npos \) const; |  | \(since C++20\) |
{% endtab %}
{% endtabs %}

### Copy

{% tabs %}
{% tab title="First Tab" %}
```cpp
#include <string>
#include <iostream>

int main()
{
    std::string foo("quuuux");
    char bar[7]{};
    foo.copy(bar, sizeof bar,2);
    std::cout << bar << '\n';
}

//uuux
```
{% endtab %}

{% tab title="Second Tab" %}


| size\_type copy\( CharT\* dest, size\_type count, size\_type pos = 0 \) const; |  | \(until C++20\) |
| :--- | :--- | :--- |
| constexpr size\_type copy\( CharT\* dest, size\_type count, size\_type pos = 0 \) const; |  | \(since C++20\) |
|  |  |  |

Copies a substring `[pos, pos+count)` to character string pointed to by `dest`. If the requested substring lasts past the end of the string, or if count == npos, the copied substring is `[pos, size())`. The resulting character string is not null-terminated.

If pos &gt; size\(\), [std::out\_of\_range](https://en.cppreference.com/w/cpp/error/out_of_range) is thrown.

#### Parameters

| dest | - | pointer to the destination character string |
| :--- | :--- | :--- |
| count | - | length of the substring |
| pos | - | position of the first character to include |

#### Return value

number of characters copied

#### Exceptions

[std::out\_of\_range](https://en.cppreference.com/w/cpp/error/out_of_range) if pos &gt; size\(\).

#### Complexity

linear in `count`
{% endtab %}
{% endtabs %}

### Resize

{% tabs %}
{% tab title="First Tab" %}
Resizes the string to contain `count` characters.

If the current size is less than `count`, additional characters are appended.

If the current size is greater than `count`, the string is reduced to its first `count` elements.

The first version initializes new characters to CharT\(\), the second version initializes new characters to `ch`.

```text
    const unsigned  desired_length(8);
    string     long_string( "Where is the end?" );
    string     short_string( "Ha" );
    
// Shorten
 long_string.resize( desired_length );
  
// Lengthen
 short_string.resize( desired_length, 'a' );
```
{% endtab %}

{% tab title="Code" %}
```cpp
#include <iostream>
#include <stdexcept>
 
int main()
{
    std::cout << "Basic functionality:\n";
    const unsigned  desired_length(8);
    std::string     long_string( "Where is the end?" );
    std::string     short_string( "Ha" );
 
    // Shorten
    std::cout << "Before: \"" << long_string << "\"\n";
    long_string.resize( desired_length );
    std::cout << "After: \"" << long_string <<  "\"\n";
 
    // Lengthen
    std::cout << "Before: \"" << short_string <<  "\"\n";
    short_string.resize( desired_length, 'a' );
    std::cout << "After: \"" << short_string <<  "\"\n";
 
    std::cout  << "\nErrors:\n";
    {
        std::string s;    
 
        try {
            // size is OK, no length_error
            // (may throw bad_alloc)
            s.resize(s.max_size() - 1, 'x');
        } catch (const std::bad_alloc&) {
            std::cout << "1. bad alloc\n";
        }
 
        try {
            // size is OK, no length_error
            // (may throw bad_alloc)
            s.resize(s.max_size(), 'x');
        } catch (const std::bad_alloc& exc) {
            std::cout << "2. bad alloc\n";
        }
 
        try {
            // size is BAD, throw length_error
            s.resize(s.max_size() + 1, 'x');
        } catch (const std::length_error&) {
            std::cout << "3. length error\n";
        }
     }
}

//OUTPUT :
Basic functionality:
Before: "Where is the end?"
After: "Where is"
Before: "Ha"
After: "Haaaaaaa"
 
Errors:
1. bad alloc
2. bad alloc
3. length error
```
{% endtab %}

{% tab title="" %}


| void resize\( size\_type count \); | \(until C++20\) |  |
| :--- | :--- | :--- |
| constexpr void resize\( size\_type count \); | \(since C++20\) |  |
|  | \(2\) |  |
| void resize\( size\_type count, CharT ch \); | \(until C++20\) |  |
| constexpr void resize\( size\_type count, CharT ch \); | \(since C++20\) |  |
|  |  |  |

Resizes the string to contain `count` characters.

If the current size is less than `count`, additional characters are appended.

If the current size is greater than `count`, the string is reduced to its first `count` elements.

The first version initializes new characters to CharT\(\), the second version initializes new characters to `ch`.

#### Parameters

| count | - | new size of the string |
| :--- | :--- | :--- |
| ch | - | character to initialize the new characters with |

#### Return value

\(none\)

#### Exceptions

[std::length\_error](https://en.cppreference.com/w/cpp/error/length_error) if count &gt; max\_size\(\). Any exceptions thrown by corresponding `Allocator`.

If an exception is thrown for any reason, this function has no effect \(strong exception guarantee\). \(since C++11\)
{% endtab %}
{% endtabs %}

###  swap

{% tabs %}
{% tab title="First Tab" %}
```text
 std::string a = "AAA";
 std::string b = "BBB";
 
 a.swap(b);
```
{% endtab %}

{% tab title="Second Tab" %}
```cpp
#include <string>
#include <iostream>
 
int main() 
{
    std::string a = "AAA";
    std::string b = "BBB";
 
    std::cout << "before swap" << '\n';
    std::cout << "a: " << a << '\n';
    std::cout << "b: " << b << '\n';
 
    a.swap(b);
 
    std::cout << "after swap" << '\n';
    std::cout << "a: " << a << '\n';
    std::cout << "b: " << b << '\n';
}
```

Output:

```text
before swap
a: AAA
b: BBB
after swap
a: BBB
b: AAA
```
{% endtab %}

{% tab title="" %}
| void swap\( basic\_string& other \); |  | \(until C++17\) |
| :--- | :--- | :--- |
| void swap\( basic\_string& other \) noexcept\(/\* see below \*/\); |  | \(since C++17\) \(until C++20\) |
| constexpr void swap\( basic\_string& other \) noexcept\(/\* see below \*/\); |  | \(since C++20\) |
|  |  |  |

Exchanges the contents of the string with those of `other`. All iterators and references may be invalidated.

| The behavior is undefined if `Allocator` does not propagate on swap and the allocators of `*this` and `other` are unequal. | \(since C++11\) |
| :--- | :--- |


#### Parameters

| other | - | string to exchange the contents with |
| :--- | :--- | :--- |


#### Return value

\(none\)

#### Complexity

Constant.

| [noexcept](https://en.cppreference.com/w/cpp/language/noexcept_spec) specification:  noexcept\([std::allocator\_traits](http://en.cppreference.com/w/cpp/memory/allocator_traits)&lt;Allocator&gt;::propagate\_on\_container\_swap::value \|\| [std::allocator\_traits](http://en.cppreference.com/w/cpp/memory/allocator_traits)&lt;Allocator&gt;::is\_always\_equal::value\) |
| :--- |
| [noexcept](https://en.cppreference.com/w/cpp/language/noexcept_spec) specification:  noexcept\(noexcept\(lhs.swap\(rhs\)\)\) |
|  |
{% endtab %}
{% endtabs %}



