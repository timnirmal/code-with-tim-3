# Print Unicode \(card pack\)

### For \_O\_U16TEXT was not declared in this scope error

Well, there's a simple workaround: just use values of these constants instead of their names. For example, `_O_U16TEXT` is `0x00020000` and `_O_U8TEXT` is `0x00040000`.

I've just confirmed that it works with `_setmode` using g++ 4.8.1 on Windows 10:

```cpp
#include <iostream>
#include <fcntl.h>
#include <io.h>
#include <stdio.h>

int main() {
    _setmode(_fileno(stdout), 0x00020000); // _O_U16TEXT
    std::wcout << L"Русский текст\n";
}
```

For print suits

| U+2660 | U+2665 | U+2666 | U+2663 |
| :--- | :--- | :--- | :--- |
| ♠ | ♥ | ♦ | ♣ |
| Black Spade Suit | Black Heart Suit | Black Diamond Suit | Black Club Suit |
| &spades; | &hearts; | &diams; | &clubs; |
| U+2664 | U+2661 | U+2662 | U+2667 |
| ♤ | ♡ | ♢ | ♧ |
| White Spade Suit | White Heart Suit | White Diamond Suit | White Club Suit |

```cpp
#include <io.h>
#include <fcntl.h>

int main(){
    _setmode(_fileno(stdout), 0x00020000);
    wprintf(L"\u2660\n");
}
```



