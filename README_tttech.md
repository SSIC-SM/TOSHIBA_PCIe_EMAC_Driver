HOW TO GENERATE AND INSTALL THE DRIVER
--------------------------------------

+ Pre-requisites
Before building this driver...
**Kernel sources must be compiled.**
**Neutrino firmware binary must be copied in the rootfs.**

+ Driver cross-compilation
# Run:
	make all ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- KERNEL_SRC=${HOME}/<path_to_your_kernel_sources>
  File DWC_ETH_QOS.ko will be generated.

+ Driver installation
# Create a new directory in the rootfs for Neutrino and copy the kernel object file into it.
	mkdir /lib/modules/`uname -r`/kernel/drivers/neutrino/
	cp DWC_ETH_QOS.ko /lib/modules/`uname -r`/kernel/drivers/neutrino/
# Update dependencies:
	depmod -a
# Create Neutrino driver configuration file in the directory /etc/modules-load.d/:
	echo "# Load Neutrino driver at boot" >  /etc/modules-load.d/neutrino.conf
	echo "DWC_ETH_QOS"                    >> /etc/modules-load.d/neutrino.conf
# Reboot the board.

Neutrino host driver can be removed from the kernel using the following command:
	rmmod DWC_ETH_QOS

