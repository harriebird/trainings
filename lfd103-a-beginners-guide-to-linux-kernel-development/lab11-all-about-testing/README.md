# lab11-all-about-testing

This activity guides in testing the Linux Kernel.

New patches can be applied using the command:
patch -p1 < file.patch
git apply --index file.patch 

To remove untracked directories and files:
git clean -dfx

View Kernel logs example command:
dmesg -t -l emerg

View kernel logs with no timestamp:
dmesg -t -k

To do kernel build stress test:
time make all

Enable configurations to test kernel changes:
CONFIG_KASAN
CONFIG_KMSAN
CONFIG_UBSAN
CONFIG_LOCKDEP
CONFIG_PROVE_LOCKING
CONFIG_LOCKUP_DETECTOR
