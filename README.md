<h1 align="center">
  <br>
  <a href="https://github.com/utsanjan/Android-Pin-Bruteforce/">
  <img src="https://1.bp.blogspot.com/-44v0nOnyEcI/YEHLlPVW9uI/AAAAAAAAbf8/s76TUfyZW7UE-MOdJwK2is5KRZLtbU5oQCLcBGAsYHQ/s200/imageonline-co-hueshifted%2B%25281%2529.png"
  alt="Android Pin Bruteforce">
  </a><br>
  Android PIN Bruteforce
  <br>
</h1>
<p align="center">Unlock an Android phone or device<br>by bruteforcing the lockscreen PIN.
<br>Turn any Kali Nethunter phone into<br>bruteforce PIN cracker of Android!</p> <br>

## 🧭 How it works

[![Buy Me A Coffee](https://img.shields.io/open-vsx/stars/redhat/java?color=D8B024&label=buy%20me%20a%20coffee&style=plastic)](https://www.buymeacoffee.com/utsanjan)‎ ‎
[![](https://img.shields.io/github/languages/count/utsanjan/Android-Pin-Bruteforce?style=plastic)](https://github.com/utsanjan/Android-Pin-Bruteforce)‎ ‎
[![](https://img.shields.io/github/license/utsanjan/Android-Pin-Bruteforce?logoColor=red&style=plastic)](https://github.com/utsanjan/Android-Pin-Bruteforce)‎ ‎
[![](https://img.shields.io/github/languages/top/utsanjan/Android-Pin-Bruteforce?color=light%20green&style=plastic)](https://github.com/utsanjan/Android-Pin-Bruteforce)‎ ‎

To learn about the commands and other usage details [Click Here.](https://github.com/utsanjan/Android-Pin-Bruteforce#-installation--usage)
<br>It uses a USB OTG cable to connect the locked phone to the Nethunter device.
<br>It emulates a keyboard, automatically tries PINs, and waits after trying too many wrong guesses.
<br><br>
**[Nethunter phone] ⇌ [USB cable] ⇌ [USB OTG adaptor] ⇌ [Locked Android phone]**

The USB HID Gadget driver provides emulation of USB Human Interface Devices (HID).
<br>This enables an Android Nethunter device to emulate keyboard input to the locked phone.
<br>It's just like plugging a keyboard into the locked phone and pressing keys.

⏳ This takes a bit over 16.6 hours to try all possible 4 digit PINs,<br>
but with the optimised PIN list it should take you much less time.

### ✔ You will need

- A locked Android phone
- A Nethunter phone (or any rooted Android with HID kernel support)
- USB OTG (On The Go) cable/adapter (USB male Micro-B to female USB A),<br>
and a standard charging cable (USB male Micro-B to male A).

## ✨ Benefits

- Turn your NetHunter phone into an Android PIN cracking machine
- Unlike other methods, you do not need ADB or USB debugging enabled on the locked phone
- You don't need to buy special hardware, e.g. Rubber Ducky, Teensy, Cellebrite, XPIN Clip, etc.
- You can easily modify the backoff time to crack other types of devices
- It works!

## 👉🏻 Features

- Optimised PIN list
- Bypasses phone pop-ups including the Low Power warning
- Detects when the phone is unplugged or powered off, and waits while retrying every 5 seconds
- Configurable delays of N seconds after every X PIN attempts
- Log file gets created for further debugging

## ⚙ Installation & Usage

```

Android-PIN-Bruteforce is used to unlock an Android phone (or device) by bruteforcing the lockscreen PIN.

  Find more information at: https://github.com/utsanjan/Android-Pin-Bruteforce

Commands:
  crack             Begin cracking PINs
  resume            Resume from a chosen PIN
  rewind            Crack PINs in reverse from a chosen PIN
  diag              Display diagnostic information

Options:
  -f, --from PIN    Resume from this PIN
  -m, --mask REGEX  Use a mask for known digits in the PIN
  -t, --type TYPE   Select PIN or PATTERN cracking
  -l, --length NUM  Crack PINs of NUM length
  -d, --dry-run     Dry run for testing. Doesn't send any keys.
  -v, --verbose     Output verbose logs.

Usage:
  android-pin-bruteforce <command> [options]
```

## 📌 PIN Lists

### Optimised PIN list

`pinlist.txt` is an optimised list of all possible 4 digit PINs,<br>
sorted by order of likelihood. pinlist.txt is from the following:<br>
https://github.com/mandatoryprogrammer/droidbrute

This list is used with permission from Justin Engler & Paul Vines from Senior Security Engineer, iSEC Partners,
and was used in their Defcon talk, [Electromechanical PIN Cracking with Robotic Reconfigurable Button Basher (and C3BO)](https://www.defcon.org/html/defcon-21/dc-21-speakers.html#Engler)

### 🎭 Cracking with Masks

Masks use regular expressions with the standard grep extended format.

`./android-pin-bruteforce crack --mask "...[45]" --dry-run`

- To try all years from 1900 to 1999, use a mask of `19..`
- To try PINs that have a 1 in the first digit, and a 1 in the last digit, use a mask of `1..1`
- To try PINs that end in 4 or 5, use `...[45]`


## 🙁 Troubleshooting

### Executing the script

If you installed the script to /sdcard/, you can
<br>execute it with the following command.

```bash ./android-pin-bruteforce``` 

Note that Android mounts /sdcard with the noexec flag. You can verify this with ```mount```.

### Check the cables

The OTG cable should be connected to the locked Android phone.
<br>The regular USB cable should be connected to the Nethunter phone.

### Diagnostics

Use the diagnostic command.

```bash ./android-pin-bruteforce diag```

Note that Nethunter USB HID support was inconsistent during testing and development.<br>
However after it starts working, it should continue working until you crack the PIN.

If you receive this message when the USB cable is plugged in then try taking<br>
the battery out of the locked Android phone and power cycling it.

```[FAIL] HID USB device not ready. Return code from /system/xbin/hid-keyboard was 5.```

### Known Issues
- This cannot detect when it unlocks

### Tips & Tricks

- Try powering off the phone and taking out the battery
- Try sending keys to your PC or laptop
- Note that the ```Device not Found``` messages<br>
are not as important as sending keys successfully.

## 🧑🏻‍💻 Technical Details

This works from an Android phone because the USB ports<br>
are not bidirectional, unlike the ports on a laptop.

Keys are sent using `/system/xbin/hid-keyboard`. <br>
To test this and send the key 1 you can use the following: <br>
`echo 1 | /system/xbin/hid-keyboard dev/hidg0 keyboard`

Before each PIN, we send the escape and enter keys. This is to keep the Android responsive and dismiss any popups about the number of incorrect PIN attempts or a low battery warning. My original motivation to develop this was to unlock a Samsung S5 Android phone. It had belonged to someone who had passed away, and their family needed access to the data on it. As I didn't have a USB Rubber Ducky or any other hardware handy, I tried using a variety of methods, and eventually realised I had to develop something new.

## ✒️ Credits 
### [Andrew Horton](https://github.com/urbanadventurer)<br>
**Work: Andrew Horton designed the Bruteforce tool<br>
which helped me a lot to design my piece of Bash Script**<br>
**[Click here](https://github.com/urbanadventurer/Android-PIN-Bruteforce)  to visit his Bruteforce Bash Script Repository.**<br>

### [Justin Engler & Paul Vines](https://defcon.org/html/defcon-21/dc-21-speakers.html#Engler)<br>
**Work: The optimised PIN list is from Justin Engler & Paul Vines<br>
from Senior Security Engineer, iSEC Partners and was used in their<br>
Defcon talk, Electromechanical PIN Cracking with Robotic <br>
Reconfigurable Button Basher and C3BO.**<br>

## 🌎 Contact me  

For Queries: [My Instagram Profile](https://www.instagram.com/utsanjan/)  
[Check Out My YouTube Channel](https://www.youtube.com/DopeSatan)
