# AhkPedal

**AhkPedal** is an [AutoHotkey](https://www.autohotkey.com/) library meant to
facilitate interaction with a USB foot pedal. Its core functionality allows
for arbitrary functions to be run upon a foot pedal button being pressed.

Currently, it only supports the [Infinity
IN-USB-2](http://www.veccorp.com/foot-controls.html) foot pedal. Contributions
with support for more pedals are welcomed.

## Usage

Place the `AhkPedal.ahk` file in your [library
directory](https://autohotkey.com/docs/Functions.htm#lib). This brings the
`AhkPedal` class into scope. When instantiating a new `AhkPedal`, you may use
the optional parameter `allowRelease` to define whether button release events
are handled in addition to the normal button press events. By default, it is
`true`. If you encounter issues like the foot pedal becoming unresponsive if
you release it too quickly, try setting it to `false`.

After creating the `AhkPedal`, you may use its method `SetHandler` to
register a new pedal handler. Its first argument is the (zero-based) index of
the pedal button to assign to, going from left to right (so the left pedal
would be 0, the center, 1, and the right, 2). `SetHandler` additionally takes
either or both of the optional arguments `onPress` and `onRelease`; these
should be a name of a function to call on the respective event.

### Example

```
#import <AhkPedal>

pedal := new AhkPedal()

; Send the Enter key when  the center pedal button is pressed.
pedal.SetHandler(1, onPress:="CenterButtonPressed")

CenterButtonPressed() {
    send {Enter}
}
```