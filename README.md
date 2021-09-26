# ftdi-usb-spi Driver

To build against the running Linux kernel:
```
make M=`pwd` modules
```

To cross-compile build against another kernel
```
(
  export PATH=/path-to/cross-compiler/example/gcc-arm-8.3-2019.03-x86_64-arm-linux-gnueabihf/bin:$PATH
  export KDIR=/path-to/linux-src-path
  make -C $KDIR M=`pwd` ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- KDIR=$KDIR modules
)
```

Deploy the driver and udev rule to auto-load the module:
```
# Copy the driver to the currently running kernel modules folder
sudo cp spi-ft232h.ko /lib/modules/$(uname -r)/kernel/drivers/misc/
# run depmod so module can be auto-loaded (modprobe)
sudo depmod -a

sudo cp conf/99-ftdi-usb-spi.rules /lib/udev/rules.d/
# reload the udev rule
sudo udevadm control --reload
```

