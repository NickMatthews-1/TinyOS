# Instructions

## Step 1: Creating the Initial Kernel
The first thing that you need to do to make the smallest Operating System that you can is to download the Linux Kernel which is found [here](https://www.kernel.org/)
This was built with the 6.13.1 Linux Kernel.

## Step 2: Extracting and Setting up
After you have downloaded and extracted the Linux Kernel into a place of your choosing you will need to make the configs.

To do this is actually rather simple.

Go into your terminal in the root of your newly extracted kernel and type ```make mrproper``` and then ```make tinyconfig```

You will now see an output from running ```make tinyconfig``` the output will be "configuration written to .config.

This is important as that confirms you are ready to move onto making changes to the config.

## Step 3: Making Config Changes


