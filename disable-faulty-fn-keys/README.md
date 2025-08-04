### Issue -> My hp notebook has a faulty keyboard which performs few auto-function keypresses.

### Resolution -> I have disabled that using udevmon, interception-tools and dual-function-keys

[[Note: The /interception folder here lives in the /etc folder as a /etc/interception/ ]]

**udevmon** listens for input events from your keyboard device "AT Translated Set 2 keyboard".

It intercepts raw key events using `intercept -g $DEVNODE`

These events are passed through dual-function-keys which applies your `disable_fn_keys.yaml` remapping.

The remapping changes all `F1–F12` key presses and holds to `KEY_UNKNOWN`, effectively disabling them.

Finally, the modified events are sent back to the system as virtual input via `uinput -d $DEVNODE`, so the function keys produce no effect.
