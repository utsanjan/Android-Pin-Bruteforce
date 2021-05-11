<h1 align="center">
  <br>
  <a href="https://github.com/utsanjan/Android-Pin-Bruteforce/">
  <img src="https://1.bp.blogspot.com/-44v0nOnyEcI/YEHLlPVW9uI/AAAAAAAAbf8/s76TUfyZW7UE-MOdJwK2is5KRZLtbU5oQCLcBGAsYHQ/s200/imageonline-co-hueshifted%2B%25281%2529.png"
  alt="Android Pin Bruteforce">
  </a><br>
  Android PIN Bruteforce
  <br>
</h1>
<p align="center">Unlock an Android phone (or device)<br>by bruteforcing the lockscreen PIN.
<br>Turn your Kali Nethunter phone into a<br>bruteforce PIN cracker for Android devices!</p>

## 🧭 How it works 

To learn about the commands and other usage details [Click Here.](https://github.com/utsanjan/Android-Pin-Bruteforce#-installation--usage)
<br>It uses a USB OTG cable to connect the locked phone to the Nethunter device.
<br>It emulates a keyboard, automatically tries PINs, and waits after trying too many wrong guesses.
<br><br>
[Nethunter phone] ⇌ [USB cable] ⇌ [USB OTG adaptor] ⇌ [Locked Android phone]

The USB HID Gadget driver provides emulation of USB Human Interface Devices (HID).
<br>This enables an Android Nethunter device to emulate keyboard input to the locked phone.
<br>It's just like plugging a keyboard into the locked phone and pressing keys.

⏳ This takes a bit over 16.6 hours to try all possible 4 digit PINs, but with the optimised PIN list it should take you much less time.

### ✔ You will need

- A locked Android phone
- A Nethunter phone (or any rooted Android with HID kernel support)
- USB OTG (On The Go) cable/adapter (USB male Micro-B to female USB A), and a standard charging cable (USB male Micro-B to male A).
- That's all!

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
- Log file

## ⚙ Installation & Usage

```

Android-PIN-Bruteforce is used to unlock an Android phone (or device) by bruteforcing the lockscreen PIN.

  Find more information at: https://github.com/urbanadventurer/Android-PIN-Bruteforce

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


## 📲 Supported Android Phones

It has been tested with these devices:
- Samsung S5 with Android 6.0.1


## 📌 PIN Lists

### Optimised PIN list

`pinlist.txt` is an optimised list of all possible 4 digit PINs, sorted by order of likelihood.
pinlist.txt is from https://github.com/mandatoryprogrammer/droidbrute

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

Note that Nethunter USB HID support was inconsistent during testing and development. However after it starts working, it should continue working until you crack the PIN.

If you receive this message when the USB cable is plugged in then try taking the battery out of the locked Android phone and power cycling it.

```[FAIL] HID USB device not ready. Return code from /system/xbin/hid-keyboard was 5.```

### Tips & Tricks

- Try powering off the phone and taking out the battery
- Try sending keys to your PC or laptop
- Note that the ```Device not Found``` messages are not as important as sending keys successfully.


## 💀 Known Issues

- This cannot detect when it unlocks

## 🧑🏻‍💻 Technical Details

This works from an Android phone because the USB ports are not bidirectional, unlike the ports on a laptop.

Keys are sent using `/system/xbin/hid-keyboard`.
To test this and send the key 1 you can use `echo 1 | /system/xbin/hid-keyboard dev/hidg0 keyboard`

Before each PIN, we send the escape and enter keys. This is to keep the Android responsive and dismiss any popups about the number of incorrect PIN attempts or a low battery warning. My original motivation to develop this was to unlock a Samsung S5 Android phone. It had belonged to someone who had passed away, and their family needed access to the data on it. As I didn't have a USB Rubber Ducky or any other hardware handy, I tried using a variety of methods, and eventually realised I had to develop something new.

## 🌎 Contact me  

For Queries: [My Instagram Profile](https://www.instagram.com/utsanjan/)  
[Check Out My YouTube Channel](https://www.youtube.com/DopeSatan)
