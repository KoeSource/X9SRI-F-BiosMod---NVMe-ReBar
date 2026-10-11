# Supermicro X9SRI-F BIOS Mod - NVME + ReBar

Here, I'll explain how to enable ReBar and NVMe boot support on the Supermicro X9SRI-F.

Since this isn't officially supported, it's essential to follow the steps exactly!

Take a look at `/images/Mainboard_setup.jpg`.<br>
My current setup is configured exactly like this.

### Resources

https://github.com/xCuri0/ReBarUEFI<br>
https://github.com/cjtim/NVMe_support_on_old_motherboard/tree/master

If you want to mod the BIOS yourself,<br>
you'll need to get the necessary tools on your own.<br>
There are plenty of guides on how to do this.

### How to

A monitor with a VGA port is absolutely necessary.<br><br>
(Alternatively, you can use a VGA-to-HDMI adapter.<br>
However, most of them do not support DOS mode, which is required to flash the BIOS.<br>
You won't receive an error message; the monitor will simply remain black after starting MS-DOS/FreeDOS. It took me half a day to realize that the HDMI-to-VGA adapter was the problem.)

- Remove your PCIe GPU.
- Flash the modded BIOS. Do not change any graphics settings in the BIOS.
- Install the PCIe NVMe adapter.<br> 
If necessary, change the PCIe bifurcation setting in the BIOS to 4x4x4x4 for the correct slot.
- Install your OS via VGA. (Since USB 2.0 is slow, I used a SATA SSD with Ventoy.)
- Turn off the PC, then connect the PCIe graphics card.
- Start up the PC and install the graphics drivers via VGA!<br>
Check to see if the graphics drivers are installed correctly.
- Go into the BIOS. Check the boot order. Save & Exit<br>
Once UEFI is enabled, you can no longer adjust the boot order because the menu no longer displays properly.
- Go into the BIOS. Set the following options:
  - VGA Priority = offboard
  - Above 4G Encoding = ON
  - CSM -> Launch Video OptROM = UEFI
  - Boot -> Boot option Filter = UEFI
  - Save & Exit
- Go into the BIOS. CSM -> Launch CSM = OFF -> Save & Exit
- Start the PC as usual. <br>
The image should now be displayed clearly on the PCIe graphics card.
- Enable ReBar:
  - Launch RebarState.exe
  - Enter 32
  - Restart the computer

Rebar should now be enabled and working

### Disable ReBar

To disable Rebar, you must perform a CMOS reset.

### USB 3.0 VIA Controller

Getting USB 3.0 to work properly on these motherboards is a hassle. <br>
I've noticed that the Windows driver causes problems.<br>
So it's best to use the driver in the ZIP archive.

If you're still having problems, try the following:
- Disable ASPM
- Disalbe "USB Selective suspend"

In my setup, the USB 3.0 controller is located directly above the graphics card.<br>
I have a small 80mm fan pointing at it.

### Image

![Rebar Enabled on X9SRI-F](https://raw.githubusercontent.com/KoeSource/X9SRI-F-BiosMod---NVMe-ReBar/refs/heads/master/images/x9srif_rebarOn.jpg)
