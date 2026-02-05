# ch32fun OneButton Library

OneButton for CH32V/ch32fun: simple pushbutton handling with debounce.

This project is a ch32fun port of the OneButton library, originally from [mathertel/OneButton](https://github.com/mathertel/OneButton).

## Getting Started

Add this library to your PlatformIO project.

```c++
#include <cstdio>
#include "ch32fun.h"

#include "OneButtonTiny.h"
#include "OneButton.h"
#include "millis.h"

int main() {
    SystemInit();
    systick_init(); // Initialize for `millis()`.

    funGpioInitC(); // Enable GPIO

    // Initialize OneButton after enable GPIOs.
    OneButton button = OneButton(PC4, true, true);
    // OneButtonTiny button(PC4, true, true);

    button.setClickMs(100);
    button.attachClick([] {
        printf("button click %d\n", millis());
    });
    while (true) {
        button.tick();
        Delay_Ms(1);
    }
}
```