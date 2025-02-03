# This is a TinyOS


So howdy there. I have created a new OS that I am calling TinyOS. At the moment all it contains only Lua and can boot.
Thats pretty much it. It can boot with QEMU at the moment using the following command.

```
qemu-system-x86_64 -cdrom image.iso
```

With this operating system it currently does absolutely nothing other then just use Lua by doing ```/Lua```

With that you can do things with Lua but not much else. The only way to exit Lua is by doing ```os.exit()```


<!-- This part is for the dumbass that made this OS -->
<!-- make isoimage FDARGS="initrd=/init.cpio" FDINITRD=../fun/init.cpio -->
<!-- ld -o shell shell.o a.out --entry main -z noexecstack  -->
<!-- gcc -static shell.c -o shell -->
<!-- cat files | cpio -H newc -o > init.cpio -->
<!-- echo init >> files -->
<!-- echo lua >> files -->
<!-- make isoimage FDARGS="initrd=/init.cpio" FDINITRD=~/fun/init.cpio -->
