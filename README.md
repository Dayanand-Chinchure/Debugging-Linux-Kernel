#Debugging-Linux-KernelTo debug the kernel using qemu and gdb.	

Instructions:
	1) Read all the instructions and steps before performing any action.
	2) Make sure you have installed OR downloaded prerequisite mentions below.
	3) qemu and gdb must be installed.
	4) Go through the "*Note" to understand steps bit more.
	5) In case of any doubts and suggestions mail to "d.chinchure@gmail.com"
 
Prerequisite :
        1) Qemu [no kvm]
        2) gdb
        3) openvpn
        4) bridge-utils
        5) kernel source code (eg. linux-2.6.32.67.tar.xz)	
	
Steps:

1) Make sure you have qemu and gdb installed and in working state.

2) Download kernel source code linux-2.6.32.67.tar.xz from kernel.org. Extract the source code. 

3) Copy the ".config" file from files.tar.gz and put it into extracted source code directory
   *Note : ".config" file is been copied from another machine with all neccessary options enable.
	 
4) Compile the kernel with option "make oldconfig"
   *Note : This will create ".config" file with old configuration settings and name a .config file as .config.old

5) After the step 4 only do "make -jx" (Replace the x with {No. of Cores - 1})
   *Note : This will create a "linux-2.6.32.67/arch/x86/boot/bzImage" file by which we have to boot with qemu. 
           No need to perform the furthur compilation steps.

5) Run command "sudo sh qemu-up" to create a bridge connection.
   *Note : We want Host machine and qemu guest to communicate with each other for that we have created a bridge 
	   connection between Host machine and qemu quest.

6) Run command "sh run linux-2.6.32.67/arch/x86/boot/bzImage" 
  *Note : Now qemu guest is up.

7) As you are in qemu guest run command "ifconfig eth0 10.10.10.100 netmask 255.255.255.0"
  *Note : after this host machine can ping to qemu quest and we will know that host machine and qemu guest 
          can communicate.	
	
8) Run command "gdb vmlinux" 
  *Note : Make sure you are in compiled kernel directory before running command.			 	

8) run command in gdb prompt "target remote :1234"
	
9) Now you can debug the kernel using qemu and gdb 	
