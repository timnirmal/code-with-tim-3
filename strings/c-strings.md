# C Strings

## Initialization

```cpp
char c[] = "abcd";

char c[50] = "abcd";

char c[] = {'a', 'b', 'c', 'd', '\0'};

char c[5] = {'a', 'b', 'c', 'd', '\0'};
```

### Assigning Values to Strings

```cpp
char c[100];
c = "C programming";  // Error! array type is not assignable.
```

But we can use `strcpy()` function instead.

### Input \(Read\) String from the user <a id="read"></a>

We can use the `scanf()` function to read a string.

The `scanf()` function reads the sequence of characters until it encounters whitespace \(space, newline, tab, etc.\)

{% tabs %}
{% tab title="C++" %}
```cpp
    cin >> name;
    cout<<"Your name is "<< name;
or
    scanf("%s", name);
    printf("Your name is %s.", name);
    
//Input : Thimira Nirmal
Output : Your Name is Thimira
```
{% endtab %}

{% tab title="Full Code" %}
```cpp
using namespace std;

int main () {
    char name[20];
    cout <<"Enter name: ";
    cin >> name;
    //scanf("%s", name);
    cout<<"Your name is "<< name;
    //printf("Your name is %s.", name);
    return 0;
}
```
{% endtab %}
{% endtabs %}

### Strings and Pointers <a id="pointers"></a>

```cpp
#include <iostream>

using namespace std;

int main () {
    char name[] = "Harry Potter";

    cout<< *name<<endl;
    cout<< *(name+1)<<endl;
    cout<< *(name+7)<<endl;

    char *namePtr = "12345678";

    cout<< *namePtr<<endl;
    cout<< *(namePtr+1)<<endl;
    cout<< *(namePtr+7)<<endl;
}

//Output:
Hao128
```



* **strcpy\(str1, str2\)**: Copies string str2 into string str1.
* **strcat\(str1, str2\)**: Concatenates \(joins\) string str2 onto the end of string str1.
* **strlen\(str1\)**: Returns the length of string str1.
* **strcmp\(str1, str2\)**: Returns 0 if str1 and str2 are the same; less than 0 if str1&lt;str2; greater than 0 if str1&gt;str2. \(compare\)
* **strlwr\(\):** converts string to lowercase
* **strupr\(\):** converts string to uppercase
* **strchr\(str1, ch\)**: Returns a pointer to the first occurrence of character ch in string str1.
* **strstr\(str1, str2\)**: Returns a pointer to the first occurrence of string str2 in string str1.





