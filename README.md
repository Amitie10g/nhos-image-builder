# NiceHash OS image downloader

This tool is intended to download and prepare a [NiceHash OS](https://www.nicehash.com/blog/post/nicehash-os-flash-tool-user-guide) to be used in the cloud.

## What does this tool do?
* Downloads the latest NiceHash OS (RAW) disk image
* Shrinks the image to 702545408 bytes (670 MB minus 512 bytes, see below why)
* Fixes the GPT structure (using [sgdisk](https://linux.die.net/man/8/sgdisk))
* Converts the image to VHD (using [qemu-img](https://linux.die.net/man/1/qemu-img))
* If loop device is available
  * Attaches the VHD image as loop device (using [losetup](https://linux.die.net/man/8/losetup) from [util-linux](https://pkgs.alpinelinux.org/package/edge/main/x86_64/util-linux))
  * Mounts the second partition
  * Updates the NiceHas OS configuration file
* Otherwise, you must mount the image and edit the configuration file yourself

Loop devices are exposed by running the container as privileged
