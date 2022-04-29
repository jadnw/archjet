# Arch Installtion Guide (BTRFS, ZRAM, Timeshift AutoSnap,...)

- mkfs.fat -F32 /dev/sda1
- mkfs.btrfs /dev/sda2
- mount /dev/sda2 /mnt
- btrfs subvolume create /mnt/@
- btrfs subvolume create /mnt/@home
- umount /mnt
- mount -o noatime,space_cache=v2,compress=zstd,ssd,discard=async,subvol=@ /dev/sda2 /mnt
- mkdir /mnt/{boot,home}
- mount -o noatime,space_cache=v2,compress=zstd,ssd,discard=async,subvol=@home /dev/sda2 /mnt/home
- mount /dev/sda1 /mnt/boot
- pacstrap /mnt base linux linux-firmware neovim git fish amd-ucode
- genfstab -U /mnt >> /mnt/etc/fstab
- arch-chroot /mnt
- git clone https://github.com/z4yw0o/archfly.git
- cd archfly
- chmod +x arch-install
- ./arch-install
- EDITOR=nvim visudo
- nvim /etc/mkinitcpio.conf
- mkinitcpio -p linux
- umount -R /mnt
- reboot
