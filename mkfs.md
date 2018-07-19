# Format disk in Linux

### format in ext4

mkfs.ext4 /dev/sda1

### Get ext4 with more inodes

mkfs.ext4 -Tsmall /dev/sda1

See /etc/mke2fs.conf


#### Links

http://stackoverflow.com/questions/21397110/how-to-store-one-billion-files-on-ext4
