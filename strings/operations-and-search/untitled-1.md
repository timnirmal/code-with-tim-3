# Untitled

| [operator+](https://en.cppreference.com/w/cpp/string/basic_string/operator%2B) | concatenates two strings or a string and a char  |
| :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/operator_cmp">operator==</a>
        </p>
        <p><b>(removed in C++20)</b>
        </p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/operator_cmp">operator!=</a>
        </p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/operator_cmp">operator&lt;</a>
        </p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/operator_cmp">operator&gt;</a>
        </p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/operator_cmp">operator&lt;=</a>
        </p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/operator_cmp">operator&gt;=</a>
        </p>
        <p>(C++20)</p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/operator_cmp">operator&lt;=&gt;</a>
        </p>
      </th>
      <th style="text-align:left">lexicographically compares two strings</th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

| [std::swap\(std::basic\_string\)](https://en.cppreference.com/w/cpp/string/basic_string/swap2) | specializes the [std::swap](https://en.cppreference.com/w/cpp/algorithm/swap) algorithm |
| :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/erase2">erase(std::basic_string)</a>
        </p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/erase2">erase_if(std::basic_string)</a>(C++20)</p>
      </th>
      <th style="text-align:left">Erases all elements satisfying specific criteria</th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

### **Input/output**

| \*\*\*\* |  |
| :--- | :--- |
| [operator&lt;&lt;operator&gt;&gt;](https://en.cppreference.com/w/cpp/string/basic_string/operator_ltltgtgt) | performs stream input and output on strings \(function template\) |
| [getline](https://en.cppreference.com/w/cpp/string/basic_string/getline) | read data from an I/O stream into a string \(function template\) |

### **Numeric conversions**

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/stol">stoi</a>
        </p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/stol">stol</a>
        </p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/stol">stoll</a>
        </p>
      </th>
      <th style="text-align:left">converts a string to a signed integer
        <br />(function)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/stoul">stoul</a>
        </p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/stoul">stoull</a>
        </p>
      </td>
      <td style="text-align:left">converts a string to an unsigned integer
        <br />(function)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/stof">stof</a>
        </p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/stof">stod</a>
        </p>
        <p><a href="https://en.cppreference.com/w/cpp/string/basic_string/stof">stold</a>
        </p>
      </td>
      <td style="text-align:left">converts a string to a floating point value
        <br />(function)</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://en.cppreference.com/w/cpp/string/basic_string/to_string">to_string</a>
      </td>
      <td style="text-align:left">converts an integral or floating point value to <code>string</code>
        <br
        />(function)</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://en.cppreference.com/w/cpp/string/basic_string/to_wstring">to_wstring</a>
      </td>
      <td style="text-align:left">converts an integral or floating point value to <code>wstring</code>
        <br
        />(function)</td>
    </tr>
  </tbody>
</table>

## erase and erase if <a id="firstHeading"></a>

{% tabs %}
{% tab title="C++" %}
```cpp
  std::erase(cnt, '3');
  
  auto erased = std::erase_if(cnt, [](char x) { return (x - '0') % 2 == 0; });
    print_container("Erase all even numbers:\n", cnt);
//Return number of erased items
```
{% endtab %}

{% tab title="" %}
```cpp
#include <iostream>
#include <numeric>
#include <string_view>
#include <string>
 
void print_container(std::string_view comment, const std::string& c)
{
    std::cout << comment;
    for (auto x : c) {
        std::cout << x << ' ';
    }
    std::cout << '\n';
}
 
int main()
{
    std::string cnt(10, ' ');
    std::iota(cnt.begin(), cnt.end(), '0');
    print_container("Init:\n", cnt);
 
    std::erase(cnt, '3');
    print_container("Erase '3':\n", cnt);
 
    auto erased = std::erase_if(cnt, [](char x) { return (x - '0') % 2 == 0; });
    print_container("Erase all even numbers:\n", cnt);
    std::cout << "In all " << erased << " even numbers were erased.\n";
}

//OUTPUT

//Init:
//0 1 2 3 4 5 6 7 8 9 
//Erase '3':
//0 1 2 4 5 6 7 8 9 
//Erase all even numbers:
//1 5 7 9
//In all 5 even numbers were erased.
```
{% endtab %}

{% tab title="" %}
#### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">c</th>
      <th style="text-align:left">-</th>
      <th style="text-align:left">container from which to erase</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">value to be removed</td>
    </tr>
    <tr>
      <td style="text-align:left">pred</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">
        <p>unary predicate which returns &#x200B;true if the element should be erased.
          <br
          />
        </p>
        <p>The expression pred(v) must be convertible to bool for every argument <code>v</code> of
          type (possibly const) <code>CharT</code>, regardless of <a href="https://en.cppreference.com/w/cpp/language/value_category">value category</a>,
          and must not modify <code>v</code>. Thus, a parameter type of CharT&amp;is
          not allowed, nor is CharT unless for <code>CharT</code> a move is equivalent
          to a copy (since C++11).&#x200B;</p>
      </td>
    </tr>
  </tbody>
</table>

#### Return value

The number of erased elements.

#### Complexity

Linear.
{% endtab %}
{% endtabs %}





