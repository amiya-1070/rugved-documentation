[***https\://docs.nvidia.com/jetson/archives/r34.1/DeveloperGuide/index.html***](https://docs.nvidia.com/jetson/archives/r34.1/DeveloperGuide/index.html)

### **always tell your LLM the complete specifications of your jetson. or better, don’t use LLMs at all.**

ssh ramesh@192.168.50.2  
orin pw: 1234

ssh rugvedxavier@192.168.60.2  
xavier pw: Rugved@123\#

(current; update as needed)

### **safety**

the jetson is a rather fragile device and does not have the hundreds of guardrails in your personal laptops. treat it as if it would break any time. be very, very careful during storms. if the power goes off, there’s a chance it could corrupt the binaries if they were in the process of being written (re: from experience.) so keep important files backed up in hard disk, because you will probably need to reflash the jetson many times.

### **flashing**

[https\://wiki.seeedstudio.com/reComputer\_J4012\_Flash\_Jetpack/](https://wiki.seeedstudio.com/reComputer_J4012_Flash_Jetpack/) (for the Orin NX 16GB)

### **packages**

[https\://pypi.jetson-ai-lab.io/](https://pypi.jetson-ai-lab.io/) (has all cuda-dependent packages)  
[https\://developer.download.nvidia.com/compute/cusparselt/redist/libcusparse\_lt/linux-aarch64/](https://developer.download.nvidia.com/compute/cusparselt/redist/libcusparse_lt/linux-aarch64/)  
btw, inside /usr/local/bin there’s cuda and cuda-\<ver\>. former is the symlink for latter  
(many more occurrences like this across the system)

### **nvidia-l4t-\***

nvidia-l4t-\* packages cause huge problems because our orin nx uses Seeed board, and the packages aren’t able to recognize it since Seeed board doesn’t use Nvidia reference carrier design.

device tree differences:  
different carrier board, USB topology, power rails, GPIO mapping, different PCIe layout so they might have been overridden during flashing

seeed does not have the A/B OTA layout \</3 

board name isn’t usually recognized by the package, and hence the scripts tend to fail

so be careful running sudo apt-upgrade

seeed board has:

- has custom flashing layout  
- bootloader configuration different  
- custom boot/partition config  
- carrier board specific patches

### **bootloader**

the wrong kernels/dtbs can be installed if you’re not careful, make sure they’re compatible with Seeed. in doing so, the boot config will be edited and look for wrong/non-existent DTB (device tree blob), it will fail to initialize hardware, system drops  
ctrl+alt+f2 (to go into the CLI of ubuntu server on USB)

never leave packages half-updated or unpacked.

### **snap**

[https\://forums.developer.nvidia.com/t/chromium-other-browsers-not-working-after-flashing-or-updating-heres-why-and-quick-fix/338891](https://forums.developer.nvidia.com/t/chromium-other-browsers-not-working-after-flashing-or-updating-heres-why-and-quick-fix/338891)  
there are often compatibility issues between linux and jetsons specifically, and it’s usually some packages making a fuss. do one of 3 things: revert it to an older version, manually download a compatible version, or disable it if it is not needed.

### **opencv**

if u get a numpy.multicore.array error then make numpy=1.26.4

### **torch**

[https\://medium.com/@surentharm/setting-up-pytorch-on-nvidia-jetson-nano-the-complete-2025-guide-294a7cf62766](https://medium.com/@surentharm/setting-up-pytorch-on-nvidia-jetson-nano-the-complete-2025-guide-294a7cf62766)

[https\://forums.developer.nvidia.com/t/pytorch-for-jetson/72048](https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048) (only has old ver.)

