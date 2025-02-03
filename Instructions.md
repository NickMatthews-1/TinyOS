# Instructions

## Step 1: Creating the Initial Kernel
The first thing that you need to do to make the smallest Operating System that you can is to download the Linux Kernel which is found [here](https://www.kernel.org/)
This was built with the 6.13.1 Linux Kernel.

## Step 2: Extracting and Setting up
After you have downloaded and extracted the Linux Kernel into a place of your choosing you will need to make the configs.

To do this is actually rather simple.

Go into your terminal in the root of your newly extracted kernel and type ```make mrproper``` and then ```make tinyconfig```

You will now see an output from running ```make tinyconfig``` the output will be "configuration written to .config"

This is important as that confirms you are ready to move onto making changes to the config.

## Step 3: Making Config Changes

You now need to make the some changes to the Linux Kernel in the menuconfig. You can enter the menuconfig by doing

```make menuconfig```

Upon doing that you will be greeted by the Kernel Configuration screen. Here is the list of the following things that you will need to change.

- Enable the 64 Bit Kernel
- Enter General Setup and Enable Initial RAM filesystem and RAM disk (initramfs/initrd) support
- Disable all of the compression methods for initial ramdisk/ramfs (these appear after selecting initramfs)
- Ensure "Configure Standard Kernel Features (Expert Users)" is enabled
- Enter Standard Kernel Features and enable "Enable Support for PrintK"
- Go back to the main mennu of the Kernel Configuration and go to Device Drivers
- In Device Drivers go to Character Devices and then enable TTY inside of Character Devices
- Go back to the main menu of Kernel Configuration
- Now go to Executable File Formats in the main menu
- In Executable File Formats enable Kernel Support for ELF binaries
- You can now exit the Kernel Configuration menu. It will ask if you want to save the config. The answer is yes.

