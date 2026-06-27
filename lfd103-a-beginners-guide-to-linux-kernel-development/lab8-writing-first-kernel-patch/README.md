# lab8-writing-first-kernel-patch

This activity guides in writing a Linux patch.

Configure `.gitconfig` file.

Drivers can be configured to be installed or disabled: disabled, vmlinux, module (modprobe)

Check new config variables:
make listnewconfig

Git operations like remote, checkout, and branch.

Check loaded modules on system:
lsmod

Finding source and header files using git grep (ex. uvcvideo):
git grep uvcvideo -- '*Makefile'

Set the value of `CONFIG_USB_VIDEO_CLASS` to configure as module in .config:
CONFIG_USB_VIDEO_CLASS=m

Recompile, install, and load the module:
sudo modprobe uvcvideo

Check the message and the module:
dmesg | less
lsmod | grep uvcvideo

Unload the module:
sudo rmmod uvcvideo

Set the value of `CONFIG_USB_VIDEO_CLASS` to configure as built-in in .config:
CONFIG_USB_VIDEO_CLASS=y

Check git local repository status:
git status

Using checkpatch.pl to check the code change if it follows the Linux Kernel style guide:
git diff | ./scripts/checkpatch.pl

Patch workflow:
- Make code changes and compile
- Run checkpatch.pl to the code changes
- Fix errors and warnings

Commit all modified files at once:
git commit -a

Generate patch file:
git format-patch -1 <commit-id>
