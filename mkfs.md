# Format disk in Linux

### format in ext4

standard:
mkfs.ext4 /dev/sda1

with reserved inodes and 0% for superuser:
mkfs.ext4 -E resize=2T -L $NAME -m 0 /dev/vgfoo/lvbar
(-E resize => Reserve  enough  space  so  that the block group descriptor table can grow to support a filesystem that has max-online-resize blocks.)

### Get ext4 with more inodes

mkfs.ext4 -Tsmall /dev/sda1

See /etc/mke2fs.conf


#### Links

http://stackoverflow.com/questions/21397110/how-to-store-one-billion-files-on-ext4
