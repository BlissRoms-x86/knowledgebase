# Debug Booting

There are a few ways to debug booting and we will run through a few of them here.

First is to hit "e" when the grub selection screen shows up, and try and boot by removing the "quiet" from your grub entry. 

The second option would be to boot in debug mode by adding DEBUG=1 or DEBUG=2 , both represent a lower level of logging. See Example below:

```text
menuentry 'Bliss-x86' --class android {
    search --file --no-floppy --set=root /AndroidOS/system.sfs
    linux /AndroidOS/kernel root=/dev/ram0 SRC=/AndroidOS androidboot.selinux=permissive androidboot.hardware=android_x86_64 quiet DATA= DEBUG=2
    initrd /AndroidOS/initrd.img
}
```

You will need to enter "exit" once or twice when using debug mode to procede to the following steps of the boot process. 

If the animation never starts, add "nomodeset" to the grub command to force software rendering and hardware compatibility mode. See Example below:

```text
menuentry 'Bliss-x86' --class android {
    search --file --no-floppy --set=root /AndroidOS/system.sfs
    linux /AndroidOS/kernel root=/dev/ram0 SRC=/AndroidOS androidboot.selinux=permissive androidboot.hardware=android_x86_64 quiet DATA= DEBUG=2 nomodeset
    initrd /AndroidOS/initrd.img
}
```

Once you are able to get things to boot, use the alt-f1 /f7 console or the local Terminal app and the Logcat command to log things,  
`su  
logcat > sdcard/log_name.txt`

When done, copy and paste the entire log either to Hastebin or Pastebin

**For more advanced debugging information:**

Please follow the advanced debugging procedures found on Android-x86 documentation [https://www.android-x86.org/documentation/debug.html](https://www.android-x86.org/documentation/debug.html)

