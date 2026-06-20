# lab7-building-and-installing-first-kernel

This activity introduces Linux Kernel compilation and installation.

Clone the Linux Stable:
git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git linux-stable

Explore branches using git branch and grep:
git branch -a | grep linux-7.1

Checkout to `linux-7.1.y`:
git checkout linux-7.1.y

Copy the working kernel config (Fedora) from `/boot` directory:
cp /boot/config-$(uname -r) .config

Update the configuration:
make oldconfig

Streamlining (tailor to system specifically, optional):
lsmod > /tmp/my-lsmod
make LSMOD=/tmp/my-lsmod localmodconfig

Compile the and install Kernel:
make -j$(nproc)
sudo make modules_install install

Compile and package to RPM:
sudo dnf install dwarves perl
make binrpm-pkg -j$(nproc) 
Install using package manager

If with NVIDIA GPU (Fedora):
Install NVIDIA driver

Check kernel logs:
dmesg -t

Check secure boot status:
mokutil  --sb-state

Disable secure boot validation:
sudo mokutil --disable-validation
