# AhkPedal

**AhkPedal** is an [AutoHotkey](https://www.autohotkey.com/) library meant to
facilitate interaction with a USB foot pedal. It allows for arbitrary
functions to be run upon a foot pedal button being pressed.

## Setup

I can only test on foot pedals I own, so for now this only works with the
[Infinity IN-USB-2](http://www.veccorp.com/foot-controls.html) foot pedal.
Additionally, please note that the library will only work on 64-bit machines.

### Installation

Place the `AhkPedal.ahk` file in your [library
directory](https://autohotkey.com/docs/Functions.htm#lib). If you manage your
libraries in a different way then you should already know what to do here.

## Usage

Import the library with `#include <AhkPedal>`. This brings the `AhkPedal`
class into scope. Use `new AhkPedal()` to get access to the API. Upon
instantiation, an `AhkPedal` will automatically connect to the USB device
and register itself to wait for messages from it.

After creating the `AhkPedal`, you may use its method `SetHandler` to
register a new pedal handler. Its first argument is the (zero-based) index of
the pedal button to assign to, going from left to right (so the left pedal
would be 0, the center, 1, and the right, 2). `SetHandler` additionally takes
either or both of the optional arguments `onPress` and `onRelease`; these
should be a name of a function to call on the respective event.

When instantiating a new `AhkPedal`, you may use the
optional parameter `allowRelease` to define whether button release events are
handled in addition to the normal button press events. By default, it is
`true`. If you encounter issues like the foot pedal becoming unresponsive if
you release it too quickly after a press, try setting it to `false`.

### Example

```ahk
#include <AhkPedal>

pedal := new AhkPedal()

; Send the Enter key when  the center pedal button is pressed.
pedal.SetHandler(1, onPress:="CenterButtonPressed")

CenterButtonPressed() {
    send {Enter}
}
```

## Acknowledgements

I would not have been able to come up with the Windows API-related parts of
the code without [musings from the
underground](http://musingsfromtheunderground.blogspot.com/2011/05/dream-autohotkey-powered-foot-pedal-for.html)'s
code. Furthermore, AutoHotkey forum user [just
me](https://autohotkey.com/board/topic/91506-broken-dllcall-to-registerrawinputdevices/)
provided relevant 64-bit compatible code.
