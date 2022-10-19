---
layout: post
title: "Configure Cloud init images on proxmox"
date: 2022-10-19 09:00:00 -0000
categories: proxmox
tags: homelab proxmox cloud-init
---

## How to download and create a cloud init image on proxmox 

You will need to create a new VM in proxmox, in this scenario the vmid is set to `999` it is important to remember when creating this vm to configure it without a disk drive initially

Copy link from cloud-images.ubuntu.com
```bash
wget https://cloud-images.ubuntu.com/minimal/releases/jammy/release/ubuntu-22.04-minimal-cloudimg-amd64.img
```

Create a serial interface on the VM, this enables consoles to work on the VM
```bash
qm set 999 --serial0 socket --vga serial0
```

rename the file and modify the extension to .qcow2
```bash
mv ubuntu-22.04-minimal-cloudimg-amd64.img ubuntu-22.04-minimal.qcow2
```

resize the image file as appropriate
```bash
qemu-img resize ubuntu-22.04-minimal.qcow2 32G
```

imprort the disk to the machine
```bash
qm importdisk 999 ubuntu-22.04-minimal.qcow2 local-lvm
```