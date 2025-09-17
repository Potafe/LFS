- There are several other partitions that are not required, but should be considered when designing a disk layout. The following list is not comprehensive, but is meant as a guide.

    * /boot – Highly recommended. Use this partition to store kernels and other booting information. To minimize potential boot problems with larger disks, make this the first physical partition on your first disk drive. A partition size of 200 megabytes is adequate.

    * /boot/efi – The EFI System Partition, which is needed for booting the system with UEFI. Read the BLFS page for details.

    * /home – Highly recommended. Share your home directory and user customization across multiple distributions or LFS builds. The size is generally fairly large and depends on available disk space.

    * /usr – In LFS, /bin, /lib, and /sbin are symlinks to their counterparts in /usr. So /usr contains all the binaries needed for the system to run. For LFS a separate partition for /usr is normally not needed. If you create it anyway, you should make a partition large enough to fit all the programs and libraries in the system. The root partition can be very small (maybe just one gigabyte) in this configuration, so it's suitable for a thin client or diskless workstation (where /usr is mounted from a remote server). However, you should be aware that an initramfs (not covered by LFS) will be needed to boot a system with a separate /usr partition.

    * /opt – This directory is most useful for BLFS, where multiple large packages like KDE or Texlive can be installed without embedding the files in the /usr hierarchy. If used, 5 to 10 gigabytes is generally adequate.

    * /tmp – A separate /tmp partition is rare, but useful if configuring a thin client. This partition, if used, will usually not need to exceed a couple of gigabytes. If you have enough RAM, you can mount a tmpfs on /tmp to make access to temporary files faster.

    * /usr/src – This partition is very useful for providing a location to store BLFS source files and share them across LFS builds. It can also be used as a location for building BLFS packages. A reasonably large partition of 30-50 gigabytes provides plenty of room.

