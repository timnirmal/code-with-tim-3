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

