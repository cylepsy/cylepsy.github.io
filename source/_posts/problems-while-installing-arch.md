---
title: Problems While Installing Arch Linux on VM
date: 2019-12-02 16:36:14
tags:
  - Linux
	- Arch Linux
	- Virtual Machine
---

I'm learning Arch Linux recently, and tried to install it in a virtual machine with VirtualBox.
However there are still some problems that I ran into.

I referenced [Luke_Smith](https://www.youtube.com/watch?v=4PBqpX0_UOc&t=2598s)'s and [DistroTube](https://www.youtube.com/watch?v=HpskN_jKyhc&t=1998s)'s videos for installing Arch Linux.
Latter also used a virtual machine.

## Grub 2 Doesn't Load Linux Kernel

The first issue I ran into is with the bootloader, Grub 2 in this case.
The step of installing bootloader was not clarified in the [Arch_Installation_Guide](https://wiki.archlinux.org/index.php/Installation_guide), but was cited to another page.

After installing Grub 2 via Pacman, run this command to install Grub to the whole disk:

```bash
grub-install /dev/sda #sda is your main drive
```

Then run this command to generate the grub config file in `/boot` directory:

```bash
grub-mkconfig grub-mkconfig -o /boot/grub/grub.cfg
```

These are the expected prompts:

```bash
Found linux image /boot/vmlinuz/-linx
Found initrt image ...
...
done
```

However I only got one line of `done` and nothing else, which indicates the linux kernel couldn't be loaded by Grub.
After couple of minutes of Googling, I realized that the linux firmware **wasn't actually installed** on the disk. I had no idea how Arch worked without kernel, but rerunning the `pacstrap` command with `linux-kernel` argument really fixed the problem.

```bash
pacstrap /mnt base linux linux-firmware
```

## Internet with VM

The second issue is access of internet. While installing on a VM, you should already be able to access to the internet when using the minimal OS on the installation drive. To setup internet for the actual OS that we're installing, simply enable a service after `arch-chroot` to the actual OS.

```bash
systemctl enable dhcpcd
```

If you're prompted with text like `Created symlink ...`, then you're good to go. If you're prompted with something like `dhcpcd.service does not exist` like me, then you need to install some packages.
Boot back to the minimal OS on the installation drive, and install dhcpcd via pacman:

```bash
pacman -S dhcpcd
```

Then boot back to the actual OS, you should be able to enable the network service.
