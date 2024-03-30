# Payload2Super :shipit:

```
OPTION 1: pay2sup.sh [-rw|--read-write] [-r|--resize] payload.bin|super.img|rom.zip|/dev/block/by-name/super
OPTION 2: pay2sup.sh [-rw|--read-write] [-r|--resize] [-c|--continue]

-rw  | --read-write          = Grants write access to all the partitions.

-r   | --resize	             = Resizes partitions based on user input. User input will be asked during the program.

-dfe | --disable-encryption  = Disables Android's file encryption. This parameter requires read&write partitions.

-d   | --debloat             = Debloats partition images with a given debloat list. If list file isn't provided or doesn't exist, it will default to debloat.txt in project directory. If that doesn't exist either, it will skip debloating. 

-t   | --thread	             = Certain parts of the program are multitaskable. If you wish to make the program faster, you can specify a number here.

-c   | --continue            = Continues the process if the program had to quit early. Do not specify a payload file with this option. NOTE: This option could be risky depending on which part of the process the program exited. Use only if you know what you're doing.

-h   | --help	             = Prints out this help message.

Note that --continue or payload.zip|.bin flag has to come after all other flags otherwise other flags will be ignored. You should not use payload.zip|.bin and --continue flags mixed with together. They are mutually exclusive.

```
This tool is aimed to support multiple devices, however it requires testers, which I have none. You are free to test it on your device and give feedbacks.

It basically converts any payload flashable ROMs into super flashables to make flashing easier and faster. You can also repack super flashables to grant them read&write access and increase/decrease partition sizes or disable Android's file encryption.

ROOT ACCESS REQUIRED 

## FEATURES
 - Can convert payload flashables to super flashables
 - Can repack super flashables from zips or /dev/block/by-name/super partition
 - Can grant partitions read and write access
 - Can increase/shrink partitions
 - Can disable Android's file encryption
 - Can use multi-threads to make process faster
 - Can continue if the program has exited in the middle of a process.
 - Can debloat partition images in case of exceeding super partition size

# FAQ
 - I get an error while repacking super, or resizing partitions, saying partition sizes exceed the super block size, what do I do?

This happens more often because the ROM you're converting is EROFS and while converting to EXT4, it has to get bigger because of the filesystems' compression rates. If the source ROM is too big, this error can happen. To work around it, you have to debloat the partition images. Tool has a debloat feature that you can use.


If you wish to go back to EROFS to make partition images fit the super block, you can do that too. The tool will ask you during runtime.

- My Device has different partitions in super.img

You can add it by yourself by adding partitions in partition.txt

>[!WARNING]
>__ONLY ADD PARTITION TO THE FIRST LINE OF THE TEXT FILE__
>
>__THE SCRIPT BY DEFAULT ALREADY INCLUDES "SYSTEM" , "SYSTEM_EXT" , "PRODUCT" AND "VENDOR" PARTITION SO DO NOT ADD THESE STATED PARTITION TO THE THE TEXT FILE__
>
>__IF YOU WANT TO REMOVE ANY DEFAULT PARTITIONS YOU NEED TO EDIT THE PAY2SUP.SH__
>
>__BEFORE__
>
>![Screenshot 2024-01-28 155320](https://github.com/rosemaryuser/Payload2Super/assets/126266679/5cf1ce5b-1ce7-444a-93d6-29f99d288b13)
>
>__AFTER__
>
>![Screenshot 2024-01-28 155320](https://github.com/rosemaryuser/Payload2Super/assets/126266679/ae4417b1-ae27-4b7b-b2bf-7ba452f12282)
>
>__IN THIS EXAMPLE I REMOVED VENDOR PARTITION__
>
>__I ADVICE TO NOT REMOVE DEFAULT PARTITIONS UNLESS U REALLY KNOW WHAT YOU ARE DOING__




>[!IMPORTANT]
>
>EXAMPLE:
>
>__SINGLE PARTITION__
>
>![Capture1](https://github.com/rosemaryuser/Payload2Super/assets/126266679/9d54466e-ba2c-4f6b-8b9f-9a4f666278a3)
>
>__MULTIPLE PARTITIONS__
>
>![Capture](https://github.com/rosemaryuser/Payload2Super/assets/126266679/f647de64-6edb-40a2-9f73-4cde96f45a2b)
>
>When adding a __NEW SINGLE__ partition just type it in the first line
>
>When adding __MULTIPLE__ partitions make sure to put a "|" also know as "pipe" before typing the next partition as shown in the example image
>
>__Only partitions in this list will be affected by the flags applied__ 

# To get this tool
```
git clone https://github.com/elfametesar/Payload2Super
su
cd Payload2Super
```
# Example Usage

```
sh pay2sup.sh -rw -r -dfe -t $(nproc --all) <path-to-your-rom-file>
```

This is a multi-platform tool, meaning it can work on both x64 Linux distros and ARM64 Android devices. You can use this tool without needing ADB access, by manually adding super block size and slot suffix.

Warning: Some shells may not be compatible, so make sure to use it on BASH, ZSH or KSH. BASH is recommended.


# Usage for dummies
Start by typing in
```
sh pay2sup.sh 
```
And add your optional parameters, for read&write access:
```
sh pay2sup.sh -rw
```
For resizing partition images:
```
sh pay2sup.sh -rw -r
```
For disabling encryption:
```
sh pay2sup.sh -rw -r -dfe
```
For using multiple cores to make the program faster:
```
sh pay2sup.sh -rw -r -dfe -t <corenumber>
```
And finally in the end, specify your ROM path:
```
sh pay2sup.sh -rw -r -dfe -t <corenumber> <path-to-ROM>
```

>[!NOTE]
>Contact me on telegram http://t.me/techgeekyboy

# Tested On
- Motorola G20
- POCO F3
- Redmi Note 10 (Mojito)
- Oneplus 8T
- Redmi Note 10s (Rosemary)
