# lab12-debugging-basics

This activity guides in debugging the Linux Kernel.


How to interpret OOPSes with System.map:

CONFIG_KALLSYMS must be enabled

Ex.: Crash occurs in the locations as per back trace:
PC is at add_range +0x14/0x6c

1. Do grep in the System.map file
grep  add_reange System.map

2. Replace add_range symbol name address in `add_range+0x14` = 80049f28 + 0x14 = 80049F3C

3. The result address should be same as the PC address in the backt trace.

4. Run objdump on vmlinux to get the disassembly and detail:
objdump -S -S --show-raw-insn --prefix-addresses --line-numbers vmlinux > objdump

5. Find the add_range in the vmlinux.objdump and look for PC address calculated above:
grep add_range vmlinux.objdump

6. Idetify the crash point

7. Check the fault address


Disassembling the kernel:
objdump - main utility used
gdb - useful when one get a kernel OOPS message and a stack dump


Debugging OOPS dump:

1. Run load the offending module into the GDB:
gdb oops.ko

2. Use add symbol file to the debugger. Addresses can be obtained from `/sys/module/oops/sections/.init.text1`:
add-symbol-file oops.o 0xffffffffa03e1000

3. From RIP instruction line, get the name of the offennding function and disassemble it:
disassemble my_oops_init

4. List the code of the offending function:
list *0x000000000000004a

Decode and Analyze the Panic Message:

Using decode_stacktace.sh:
scripts/decode_stackrace.sh -r <release> | <vmlinux> [base-path] [modules-path]

scripts/decode_stacktrace.sh  ./vmlinux < panic_trace.txt

Tracing directory:
/sys/kernel/tracing/

Sched wakeup format directory:
/sys/kernel/tracing/events/sched/sched_wakeup/format
