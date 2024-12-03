# Arch install
## Load keyboard layout
- `loadkeys uk`
## Test networking
- `ping xkcd.com`
## Partitions
- `cfdisk`: new 4G (swap), new fill disk (root).
- `mkfs.ext4 <root>`
- `mkswap <swap>`
- `mount <root> /mnt`
- `mkdir -p mnt/boot/efi`
- `mount <efi> /mnt/boot/efi`
- `swapon <swap>`
- `lsblk` (check)
## Base packages
- `pacstrap /mnt base linux linux-firmware sof-firmware base-devel grub efibootmgr dosfstools mtools vim networkmanager intel-ucode man-db man-pages texinfo iw git`
## File system table
- `genfstab /mnt > /mnt/etc/fstab`
## Change root
- `arch-chroot /mnt`
## Time zone and locale
- `ln -sf /usr/share/zoneinfo/Europe/London /etc/localtime`
- `hwclock --systohc`
- `vim /etc/locale.conf`, add `LANG=en_GB.UTF8`
- ` vim /etc/vconsole.conf`, add `KEYMAP=uk`
## Users
- `vim /etc/hostname`, add hostname chosen.
- `passwd`, type root password chosen.
- `useradd -m -G wheel -s /bin/bash <username>`
- `passwd <username>`, type user password chosen.
- `visudo`, uncomment line beginning `%wheel`.
## Networking
- `systemctl enable --now NetworkManager`
- `nmcli device wifi list`
- `nmcli device wifi connect <network> password <password>`
## Grub
- `vim /etc/default/grub`, uncomment/add `GRUB_DISABLE_OS_PROBER=false`
- `pacman -S os-prober`
- `grub-install --target x86_64-efi --bootloader-id=grub_uefi --recheck`
- `grub-mkconfig -o /boot/grub/grub.cfg`
## Exit
- `exit`
- `umount -a`
- `reboot`
## Install yay
- `git clone https://aur.archlinux.org/yay.git`
- `cd yay && makepkg -si`
- `yay -Syu`
