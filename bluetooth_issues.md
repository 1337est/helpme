There's an issue where sometimes I can't get a bluetooth connection. and I get the error message:
"No default controller available" when trying to connect via bluetoothctl.
I've found that issuing:

sudo modprobe -r btusb && sudo modprobe btusb

fixes my issue and my device can then connect again without any issues.

Additional info:
https://wiki.archlinux.org/title/bluetooth#bluetoothctl:_No_default_controller_available
