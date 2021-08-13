# Linux kernel

## Running

This folder has a Linux 4.10.6 bzImage already compiled, allowing to just run it with QEMU. The [run.sh](./run.sh) script
provides an easy executable for it.

### Dependencies

TODO

### KVM problem

If for some reason your machine does not support KVM, remove `-enable-kvm \` from [run.sh](./run.sh). It will make it veeeery
slow, but should work.

## .config

[config](./config) is the .config file that specifies the options that will be enabled and disabled in the kernel.

This file was created using (from inside the kernel tree):

```terminal
make defconfig
make kvmconfig
```

Then appending some debug options to it:

```text
# Coverage collection.
CONFIG_KCOV=y

# Debug info for symbolization.
CONFIG_DEBUG_INFO=y

# Memory bug detector
CONFIG_KASAN=y
CONFIG_KASAN_INLINE=y

# Required for Debian Stretch
CONFIG_CONFIGFS_FS=y
CONFIG_SECURITYFS=y
```

And finally running `make olddefconfig`.

[Take a look here](https://vccolombo.github.io/cybersecurity/linux-kernel-qemu-setup/) for more information.

## create-image.sh

File taken from [google/syzkaller](https://github.com/google/syzkaller).