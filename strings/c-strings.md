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

The `scanf()` function reads the sequence of characters until it encounters whitespace \(space, newline, tab, etc.\).

{% tabs %}
{% tab title="C++" %}
```cpp
    cin >> name;
    cout<<"Your name is "<< name;

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
    cout<<"Your name is "<< name;
    return 0;
}
```
{% endtab %}
{% endtabs %}



