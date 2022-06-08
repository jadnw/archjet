# Arch Installtion Guide (BTRFS, ZRAM, Timeshift AutoSnap,...)

- mkfs.fat -F32 /dev/sda5
- mkfs.btrfs /dev/sda6
- mount /dev/sda6 /mnt
- btrfs subvolume create /mnt/@
- btrfs subvolume create /mnt/@home
- umount /mnt
- mount -o noatime,space_cache=v2,compress=zstd,ssd,discard=async,subvol=@ /dev/sda6 /mnt
- mkdir /mnt/{boot,home}
- mount -o noatime,space_cache=v2,compress=zstd,ssd,discard=async,subvol=@home /dev/sda6 /mnt/home
- mount /dev/sda5 /mnt/boot
- pacstrap /mnt base linux linux-firmware neovim git fish amd-ucode
- genfstab -U /mnt >> /mnt/etc/fstab
- arch-chroot /mnt
- git clone https://github.com/jadnw/archjet.git
- cd archfly
- chmod +x install
- ./install
- EDITOR=nvim visudo
- nvim /etc/mkinitcpio.conf
- mkinitcpio -p linux
- exit
- umount -R /mnt
- reboot
