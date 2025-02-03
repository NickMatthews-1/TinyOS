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

## Step 4: Making Inital Kernel

Congrats you can now make the initial kernel. To do this it is as simple as

``` make -jX ```

The X is in place of the amount of processors your CPU has.


## Step 5: Testing

After making the initial kernel I advise that you test this kernel by trying to run it. This can be done with QEMU from the commandline,
with the following command

``` qemu-system-x86_64 -kernel arch/x86/boot/bzImage ```

This will open up a QEMU window and start the booting process for the new kernel. However, at this point in time the OS will just panic.
This is an expected outcome. This is due to the fact that there is no init and the kernel panics. Do not worry. This is what we want.

## Step 6: Making Init

Firstly you will need to take the shell.c (file)[shell.c] found in this repo and compiling it with gcc. This is done with the following command.

```gcc -c shell.c```
This will output "shell.o" as the output.

Now take the sys.S (file)[sys.S] from this repo and compile that with as. This is done with the following command

```as sys.S```
This will output "a.out" as the output.


You now need to link these two together using the LD Linker. This is done with the following command.

```ld -o shell shell.o a.out --entry main -z noexecstack```

This will now link these two together into one file.
