# lab10-kernel-and-driver-building-loading-and-dependencies

This activity guides in building, loading, and dependencies of kernel and drivers.

Using make to compile a single source file:
make <path>/<filename>.o

Using make to compile files inside a directory:
make <path>

Using make to compile a path as module:
make M=<path>

Before successfully building a module, all of its dependencies must be enabled.
`Kconfig` file contains this information.

Kernel configuration menu:
make menuconfig

Check if module was loaded:
lsmod | grep <module-name>

To load and unload a module:
modprobe vimc

To remove a module:
rmmod <module>
