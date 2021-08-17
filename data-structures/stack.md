# Stack

A stack is a data structure that uses two main methods to manipulate data:

* Push: adds a new piece of data in the stack.
* Pop: removes the last piece of data added.

In addition, there is another useful method that is usually implemented in a stack:

* Top: returns the last element added, without removing it.

LIFO\(Last In First Out\) type of working

## Stack Class

{% tabs %}
{% tab title="C++" %}
```cpp
#include <stack>
using namespace std;

stack <int> stack;

stack.push(11);     //Insert value at top
stack.pop();        //Delete the top most element in stack
stack.top();        //Returns a reference to the top most element of the stack
stack.empty();      //Return true if empty
stack.size();       //Size of stack
```
{% endtab %}

{% tab title="Code" %}
```cpp
#include <iostream>
#include <stack>
using namespace std;

int main() {
    stack<int> stack;
    stack.push(11);
    stack.push(12);
    stack.push(14);
    stack.push(15);

    stack.pop();

    while (!stack.empty()) {
        cout << stack.top() << " ";
        stack.pop();
    }
}
```
{% endtab %}
{% endtabs %}

### stack::swap\(\)

This function is used to swap the contents of one stack with another stack of the same type but the size may vary.

```cpp
stack1.swap(stack2)
```

#### Print Stack

```cpp
//Recomended : Use as a function. So copy of stack will be processed
void showStack(stack <int> st){
    while (!st.empty()) {
        cout << st.top();
        st.pop();
    }
}
```





### Sort using temp Array

{% tabs %}
{% tab title="Algorithm" %}
1. Create a temporary stack say **tmpStack**.
2. While input stack is NOT empty do this:
   * Pop an element from input stack call it **temp**
   * while temporary stack is NOT empty and top of temporary stack is greater than temp, pop from temporary stack and push it to the input stack
   * push **temp** in temporary stack
3. The sorted numbers are in tmpStack

[https://www.geeksforgeeks.org/sort-stack-using-temporary-stack/?ref=rp](https://www.geeksforgeeks.org/sort-stack-using-temporary-stack/?ref=rp)

Sort using
{% endtab %}

{% tab title="Code" %}
```cpp
#include <iostream>
#include <stack>
using namespace std;

void showStack(stack <int> st){
    while (!st.empty()) {
        cout << st.top() <<" ";
        st.pop();
    }
}

////======================================Function for Sort Ascending
stack<int> sortStack(stack<int> st){
    stack<int> tmpStack;

    while(!st.empty()){
        //Pop out first element
        int temp = st.top();
        st.pop();
    
        ////================================ Change < to > make Descending
        // while temporary stack is not empty and top of stack is greater than temp
        while (!tmpStack.empty() && tmpStack.top() < temp){
            // pop from temporary stack and push it to the input stack
            st.push(tmpStack.top());
            tmpStack.pop();
        }

        // push temp in tempory of stack
        tmpStack.push(temp);
    }

    return tmpStack;
}

int main() {
    stack<int> stack;
    stack.push(33);
    stack.push(98);
    stack.push(94);
    stack.push(25);
    stack.push(12);


    showStack(stack);

    cout<<endl<<endl;

    showStack(sortStack(stack));
}
```
{% endtab %}
{% endtabs %}



