# Kali-Linux-black-screen-after-boot-menu---FIXED
After spending few days on how-tos and debugging the black screen issue on boot after installing Kali Linux, I was finally able to find a solution to that problem. 


* Here is a simple and short fix that will allow to boot and configure the system from a graphical user interface (In Linux Mint will be Gnome).
* On the grub menu, select Kali Linux and press <b>[Tab] or [e]</b> to edit the grub settings.
* Now search for the line that starts with <b>‘linux‘</b> and ends with <b>-‘quiet splash’ or ‘splash’</b>.
* Add one of the following 'xxxx.modeset=0' parameter at the end of the long grub command line as is (type one space before). Use the parameter related to the brand or chipset of your video card. 

pe.: 
use nouveau  or nvidia for nvidia based cards (proprietary driver, just nv in some linux distributions, nouveau driver is the default in Mint) ), 
use radeon for amd/ati cards, i915 for intel based motherboards...  These are the most common examples:
* nvidia.modeset=0
* nouveau.modeset=0
* radeon.modeset=0
* i915.modeset=0 
* r128.modeset=0  (for very old ati rage 128 cards...)
* If you don't know the brand you may use just one word:   nomodeset
* Your will find the full range of drivers and more info at Xorg.org wiki

* Press [Ctrl]+[X] or F10 to boot with this added parameter. This parameter will not be saved, just used in this single boot and nothing is damaged. To cancel without changes press [Esc].

Therefore, if you do not want to go through this procedure every time, after you enter your Kali Linux system, do the follow:
* open terminal and verify you have hybrid graphics with command: lspci | grep -E "VGA|3D" 

I worked on VmWare ESXI so when I insert command, the output is: 00:0f.0 VGA compatible controller: VMware SVGA II Adapter

In that case, you need to edit the GRUB config so that you don't have to manually enter the nomodeset option on each boot. (NOTE: This will leave you with particularly small resolution options for the VM)

You can do this as follows:
* sudo nano /etc/default/grub
and then add nomodeset to GRUB_CMDLINE_LINUX_DEFAULT:

<b>GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nomodeset"</b>

And then save by hitting Ctrl+O, then exit nano with Ctrl+X, then simply run:
* sudo update-grub

For other graphics card manufacturers, find the commands yourself :) 



