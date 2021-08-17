# Operations and Search

| **Operations** |  |
| :--- | :--- |
| [clear](https://en.cppreference.com/w/cpp/string/basic_string/clear) | clears the contents |
| [insert](https://en.cppreference.com/w/cpp/string/basic_string/insert) | inserts characters |
| [erase](https://en.cppreference.com/w/cpp/string/basic_string/erase) | removes characters |
| [push\_back](https://en.cppreference.com/w/cpp/string/basic_string/push_back) | appends a character to the end |
| [pop\_back](https://en.cppreference.com/w/cpp/string/basic_string/pop_back)\(C++11\) | removes the last character |
| [append](https://en.cppreference.com/w/cpp/string/basic_string/append) | appends characters to the end |
| [operator+=](https://en.cppreference.com/w/cpp/string/basic_string/operator%2B%3D) | appends characters to the end |
| [compare](https://en.cppreference.com/w/cpp/string/basic_string/compare) | compares two strings |
| [starts\_with](https://en.cppreference.com/w/cpp/string/basic_string/starts_with)\(C++20\) | checks if the string starts with the given prefix |
| [ends\_with](https://en.cppreference.com/w/cpp/string/basic_string/ends_with)\(C++20\) | checks if the string ends with the given suffix |
| [contains](https://en.cppreference.com/w/cpp/string/basic_string/contains)\(C++23\) | checks if the string contains the given substring or character |
| [replace](https://en.cppreference.com/w/cpp/string/basic_string/replace) | replaces specified portion of a string |
| [substr](https://en.cppreference.com/w/cpp/string/basic_string/substr) | returns a substring |
| [copy](https://en.cppreference.com/w/cpp/string/basic_string/copy) | copies characters |
| [resize](https://en.cppreference.com/w/cpp/string/basic_string/resize) | changes the number of characters stored |
| [swap](https://en.cppreference.com/w/cpp/string/basic_string/swap) | swaps the contents |

sss

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
{% endtabs %}



