The Linux kernel authors have provided a very nice feature of issuing low-level commands to the kernel directly, regardless of the state the system is in. This is called the "Magic SysRq Key", because these commands are issued by pressing the <kbd>SysRq</kbd> key on the keyboard (if you can't find it, typically, it shares the same physical key as the <kbd>Print Screen</kbd> key, but on some laptops it can be elsewhere). 

A common use is to reboot when the computer freezes and becomes unresponsive due to some software or hardware exception, without having to push the hardware reset button or to cut power to the computer, which runs the risk of corrupting the filesystem and does not give the chance to processes which are still responsive to terminate gracefully. The magic SysRq key lets us do this elegantly and safely.

On EndeavourOS, like on vanilla Arch, this functionality is disabled by default, because it is a potential security concern (however, since it requires physical access to the keyboard, it's not a big security concern). This is how you enable it:

* Run this command in the terminal: 
* 
  `echo 'kernel.sysrq=1' | sudo tee /etc/sysctl.d/99-reisub.conf`
  
  This will create the file `/etc/sysctl.d/99-reisub.conf`, containing the single line `kernel.sysrq=1` (it does not have to be named `99-reisub.conf`, but the name is good because you'll know what it does, it is the location of the file and its contents that are important). Alternatively, you can create this file using a terminal-based text editor, like `vim` or `nano` with `sudo`.
    
* Reboot for the change to take place.
* If you want to disable this functionality, just remove the file created in the first step (`sudo rm /etc/sysctl.d/99-reisub.conf`)

Now, when you want to hard-reboot the computer, perform the following key combination:
press and hold the <kbd>Alt</kbd> key the entire time. Now, one after another, with about a second in between, press (tap) the following keys: <kbd>SysRq</kbd>, <kbd>R</kbd>, <kbd>E</kbd>, <kbd>I</kbd>, <kbd>S</kbd>, <kbd>U</kbd>, <kbd>B</kbd>. Your computer should reboot if everything was done correctly (you can let go of the <kbd>Alt</kbd> key now ;) ).

This sequence issues the following low-level commands to the kernel:
 * <kbd>R</kbd> = Switch the keyboard from raw mode to XLATE mode
 * <kbd>E</kbd> = Send the signal `SIGTERM` to gracefully terminate all processes (except `PID 1`)
 * <kbd>I</kbd> = Send the signal `SIGKILL` to kill all processes that didn't terminate gracefully
 * <kbd>S</kbd> = Sync data to disk (flush)
 * <kbd>U</kbd> = Unmount the filesystem (and remount as read-only)
 * <kbd>B</kbd> = Reboot

Just remember that the letters spell REISUB (a good mnemonic is "Reboot Even If System Utterly Broken").

For more info, see: 
https://wiki.archlinux.org/index.php/Keyboard_shortcuts#Kernel

https://www.kernel.org/doc/html/latest/admin-guide/sysrq.html

In consultation with the Holy Frog Congress humbly created by 

https://forum.endeavouros.com/u/kresimir/summary
