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

Firstly you will need to take the shell.c [file](shell.c) found in this repo and compiling it with gcc. This is done with the following command.

```gcc -c shell.c```
This will output "shell.o" as the output.

Now take the sys.S [file](sys.S) from this repo and compile that with as. This is done with the following command

```as sys.S```
This will output "a.out" as the output.


You now need to link these two together using the LD Linker. This is done with the following command.

```ld -o shell shell.o a.out --entry main -z noexecstack```

This will now link these two together into one file. This is now in a usable state.

If you make any changes to either the [shell.c](shell.c) or the [sys.S](sys.S) file at any time you will need to recompile them and relink using this section.

After that is done just rename the file from shell to init by doing ```mv shell init```

We now need to make an archive with the init file we have just made. This is done by doing the following

```echo init | cpio -H newc -o > init.cpio```

You will now have the outputted archive as a result of the command you just ran.


## Step 7 Making the ISO Image

In this section you will be making a bootable image of this operating system.

You will need to re-enter the Linux Kernel directory that you previously made. In here you will need to specify some of the arguements for,
the compliation of the image that you will be making. This is done with the following

```make isoimage FDARGS="initrd=/init.cpio" FDINITRD=../TinyOS/init.cpio```

This will now make a new image that will be ready for boot and place it in arch/x86/boot/ and it will be called image.iso This will be
inside the Linux directory you are currently working out of.

To test it, it's as simple as doing

```qemu-system-x86_64 -cdrom arch/x86/boot/image.iso```

This will now open a QEMU window similar to earlier and take you to a working shell.

## Completion

You have now made a new operating system and are now free to do with it as you wish. Currently you can do NOTHING at all with it as it
has no functionality to it other then the basic shell that you added earlier. I will cover how to add functionality to it in another guide.
