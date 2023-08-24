# 3 Button Hello World

A basic example of the 3-button LCD mode and a callback function.

## Further Reading

- [LCD Docs](https://pros.cs.purdue.edu/v5/api/cpp/llemu.html)
- [Callback Functions](https://www.learncpp.com/cpp-tutorial/function-pointers/)
- [Bitmasking](https://www.learncpp.com/cpp-tutorial/bit-manipulation-with-bitwise-operators-and-bit-masks/)
- [Static](https://en.cppreference.com/w/cpp/language/static)

## Code

```cpp
#include "main.h"

// callback for center button
void on_center_button()
{
  //the value of pressed will persist until the button is pressed again
  //because it's declared "static"
  static bool pressed = false;
  pressed = !pressed;

  if (pressed)
  {
    pros::lcd::set_text(2, "I was pressed!");
  }
  else
  {
    // reset line 2
    pros::lcd::clear_line(2);
  }
}

//this function is the first to run when the robot starts up
void initialize()
{
  // initialize the LCD screen
  pros::lcd::initialize();

  //sets line 1 (remember, lines are 0-indexed) to "Hello World!"
  pros::lcd::set_text(1, "Hello World!");

  // bind on_center_button() to the center button
  pros::lcd::register_btn1_cb(on_center_button);
}

//this function is called when the driver control period starts
void opcontrol()
{

  while (true)
  {
    // print the "0 0 0" status string
    // NOTE: pros::lcd::read_buttons() returns a 3-bit bitmask, not an integer
    // For now, don't worry about how this works. You'll learn about this later
    pros::lcd::print(0, "%d %d %d", (pros::lcd::read_buttons() & LCD_BTN_LEFT) >> 2,
                     (pros::lcd::read_buttons() & LCD_BTN_CENTER) >> 1,
                     (pros::lcd::read_buttons() & LCD_BTN_RIGHT) >> 0);

    // wait 20 milliseconds until next look
    pros::delay(20);
  }
}
```

## Images

### Default

![Default Screenshot](/examples/3btn-helloworld/3btn-helloworld-default.png)

### Pressed

![Pressed Screenshot](/examples/3btn-helloworld/3btn-helloworld-pressed.png)
