# String Class

```cpp
// string library
#include <string>

string str = "HelloWorld";
cout << str;
```

### String Concatenation \(join\)

```cpp
string firstName = "Tim";
string lastName = "Nirmal";
string fullName = firstName + " " +lastName;

string fullName = firstName.append(lastName);
```

`append()` function is more faster than using + operator.

string + number cause an error.

## String Functinos

### assign\(\)

{% tabs %}
{% tab title="C++" %}
```cpp
string s = "ab";
//Create string s with "ab"
    
s.assign(4, 'a');
//Assign 'a' 4 times to string -> "aaaa"
    
string const c("Exemplary");
s.assign(c);
//s -> "Exemplary"
    
s.assign(s, 0, s.length() - 4);
//Delete 4 characters from string s
    
s.assign("Get only 8 chars", 8);
//s will be "Get only"
    
s.assign("C-style\0string");
//Terminate after \0  s -> "C-style"
```
{% endtab %}

{% tab title="Code" %}
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main () {

    string s = "ab";
    s.assign(4, '4');
    cout << s<<endl;
    std::string const c("Exemplary");
    s.assign(c);
    cout << s<<endl;
    s.assign(s, 0, s.length() - 4);
    cout << s<<endl;
    s.assign("Get only 8 chars", 8);
    cout << s<<endl;
    s.assign("C-style\0string");
    cout << s<<endl;

    return 0;
}

```
{% endtab %}
{% endtabs %}

### = Operator

{% tabs %}
{% tab title="C++" %}
```cpp
string str1;
string str2 { "Thimira" };

str1 = str2;
//str1 -> "Thimira"  str2 -> "Thimira"

str1 = move(str2);
//str1 -> "Thimira"  str2 -> ""

str2 = "Nirmal";
//str1 -> "Thimira"  str2 -> "Nirmal"

str1 = '!';
//str1 -> "!"

str1 = {'g','a','m','m','a'};    //initializer list
//str1 -> "gamma"

str1 = 35U; // equivalent to str1 = static_cast<char>(35U);
cout << str1 << '\n'; // "#" (ASCII = 35)
```
{% endtab %}

{% tab title="Code" %}
```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main () {

    string str1;
    string str2 { "Thimira" };


    str1 = move(str2);
    cout << quoted(str1) << ' ' // "alpha"
    << quoted(str2) << '\n'; // "" or "alpha" (unspecified)

    // (3) operator=( const CharT* );
    str1 = "beta";
    cout << str1 << '\n'; // "beta"

    // (4) operator=( CharT );
    str1 = '!';
    cout << str1 << '\n'; // "!"

    // (5) operator=( initializer_list<CharT> );
    str1 = {'g','a','m','m','a'};
    cout << str1 << '\n'; // "gamma"

    // (6) operator=( const T& );
    str1 = 35U; // equivalent to str1 = static_cast<char>(35U);
    cout << str1 << '\n'; // "#" (ASCII = 35)

    return 0;
}
```
{% endtab %}

{% tab title="CPP Ref" %}
```cpp
#include <string>
#include <iostream>
#include <iomanip>
 
int main()
{
    std::string str1;
    std::string str2 { "alpha" };
 
    // (1) operator=( const basic_string& );
    str1 = str2;
    std::cout << std::quoted(str1) << ' ' // "alpha"
              << std::quoted(str2) << '\n'; // "alpha"
 
    // (2) operator=( basic_string&& );
    str1 = std::move(str2);
    std::cout << std::quoted(str1) << ' ' // "alpha"
              << std::quoted(str2) << '\n'; // "" or "alpha" (unspecified)
 
    // (3) operator=( const CharT* );
    str1 = "beta";
    std::cout << std::quoted(str1) << '\n'; // "beta"
 
    // (4) operator=( CharT );
    str1 = '!'; 
    std::cout << std::quoted(str1) << '\n'; // "!"
 
    // (5) operator=( std::initializer_list<CharT> );
    str1 = {'g','a','m','m','a'};
    std::cout << std::quoted(str1) << '\n'; // "gamma"
 
    // (6) operator=( const T& );
    str1 = 35U; // equivalent to str1 = static_cast<char>(35U);
    std::cout << std::quoted(str1) << '\n'; // "#" (ASCII = 35)
}
```
{% endtab %}
{% endtabs %}

## **Element access**

### **at**

**Parameter -** position of the character to return

**Return value -** Reference to the requested character

{% tabs %}
{% tab title="C++" %}
```cpp
s = "abc";
s.at(2) = 'x';
//s -> abx
//Execption Handeling included in
```
{% endtab %}

{% tab title="Code" %}
```cpp
#include <stdexcept>
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string s;

    s = "abc";
    s.at(2) = 'x';
    //s -> abx

    //Ex 2 : Throws out_of_range if pos >= size().
    try {
        // This will throw since the requested offset is greater than the current size.
        s.at(3) = 'x';
    }
    catch (out_of_range const& exc) {
        cout << exc.what() << '\n';
    }
}
```
{% endtab %}
{% endtabs %}

### \[ \] Operator

{% tabs %}
{% tab title="C++" %}
```cpp
s[5] = '5';
```
{% endtab %}

{% tab title="Code" %}
```cpp
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string const e("Exemplar");
    for (unsigned i = e.length() - 1; i != 0; i/=2)
        cout << e[i];
    cout << '\n';
    //Output -> rmx

    // print as a C string -> output : Exemplar
    const char* c = &e[0];
    cout << c << '\n';

    //Change the last character of s into a 'y'
    string s("Exemplar ");
    s[s.size()-1] = 'y'; // equivalent to s.back() = 'y';
    cout << s << '\n';
    //output -> Exemplary
}
```
{% endtab %}
{% endtabs %}

### front\(\) & back\(\)

{% tabs %}
{% tab title="C++" %}
```cpp
s.front()
s.back()
```
{% endtab %}

{% tab title="Code" %}
```cpp
#include <iostream>
#include <string>

int main()
{
    {
        std::string s("Exemplary");
        char& f = s.front(); f = 'e';
        //or
        s.front()= 'e';
        std::cout << s << '\n'; // "exemplary"
    }

    {
        std::string const c("Exemplary");
        char const& f = c.front();
        std::cout << &f << '\n'; // "Exemplary"
    }
}
```
{% endtab %}
{% endtabs %}

## **Iterators**

{% tabs %}
{% tab title="begin" %}
```cpp
#include <string>
#include <iostream>
 
int main()
{
    std::string s("Exemplar");
    *s.begin() = 'e';
    std::cout << s <<'\n';
 
    auto i = s.cbegin();
    std::cout << *i << '\n';
//  *i = 'E'; // error: i is a constant iterator
}

//Output : 
//exemplar
//e
```
{% endtab %}

{% tab title="end" %}
```cpp
#include <iostream>
#include <algorithm>
#include <iterator>
#include <string>
 
int main()
{
    std::string s("Exemparl");
    std::next_permutation(s.begin(), s.end());
 
    std::string c;
    std::copy(s.cbegin(), s.cend(), std::back_inserter(c));
    std::cout << c <<'\n'; // "Exemplar"
}

//Output :
//Exemplar
```
{% endtab %}

{% tab title="rbegin" %}
```cpp
#include <iostream>
#include <algorithm>
#include <iterator>
#include <string>
 
int main()
{
    std::string s("Exemplar!");
    *s.rbegin() = 'y';
    std::cout << s << '\n'; // "Exemplary"
 
    std::string c;
    std::copy(s.crbegin(), s.crend(), std::back_inserter(c));
    std::cout << c << '\n'; // "yralpmexE"
}

//Exemplary
//yralpmexE
```
{% endtab %}

{% tab title="rend" %}
```cpp
#include <algorithm>
#include <iostream>
#include <iterator>
#include <string>
 
int main()
{
  std::string s("A man, a plan, a canal: Panama");
  {
    std::string c;
    std::copy(s.rbegin(), s.rend(), std::back_inserter(c));
    std::cout << c <<'\n'; // "amanaP :lanac a ,nalp a ,nam A"
  }
 
  {
    std::string c;
    std::copy(s.crbegin(), s.crend(), std::back_inserter(c));
    std::cout << c <<'\n'; // "amanaP :lanac a ,nalp a ,nam A"
  }
}

//amanaP :lanac a ,nalp a ,nam A
//amanaP :lanac a ,nalp a ,nam A
```
{% endtab %}
{% endtabs %}

## Capacity / Size

### empty\(\)

check if the string is empty and return boolean.

