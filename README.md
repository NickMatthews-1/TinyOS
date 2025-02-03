# This is a TinyOS


So howdy there. I have created a new OS that I am calling TinyOS. At the moment all it contains only Lua and can boot.
Thats pretty much it. It can boot with QEMU at the moment using the following command.

```
qemu-system-x86_64 -cdrom image.iso
```

With this operating system it currently does absolutely nothing other then just use Lua by doing ```/Lua```

With that you can do things with Lua but not much else. The only way to exit Lua is by doing ```os.exit()```


This operating system was made with the 6.13.1 Linux Kernel and can be found at

https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.13.1.tar.xz


## Instructions!

I made a special instructions file for this [here](instructions.md) that can be used to learn how to make your own TinyOS!



> [!CAUTION]
> the person that made this is slightly stupid
