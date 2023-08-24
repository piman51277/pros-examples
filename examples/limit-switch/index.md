# Limit Switch

An example of digital input through ADI ports.

## Sensor Wiring
- 3-wire limit switch / push button
  - Connect to 3-wire port A

## Further Reading

- [ADIDigitalIn Docs](https://pros.cs.purdue.edu/v5/api/cpp/adi.html#pros-adidigitalin)

## Code

```cpp
#include "main.h"
#include <cstdint>

void initialize()
{
	pros::lcd::initialize();
}

void opcontrol()
{

	// sets port A to an digital input
	pros::ADIDigitalIn limitSwitch(1);

	while (true)
	{
		// get_value() returns 1 or 0 (pressed or not pressed)
		std::int32_t limitSwitchValue = limitSwitch.get_value();

		// print the value of the limit switch
		if (limitSwitchValue == 1)
		{
			pros::lcd::print(0, "Limit switch is pressed");
		}
		else
		{
			pros::lcd::print(0, "Limit switch is not pressed");
		}

		pros::delay(20);
	}
}

```
