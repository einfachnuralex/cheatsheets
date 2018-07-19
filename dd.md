
# dd

sample

```
dd if=2017-11-29-raspbian-stretch-lite.img of=/dev/mmcblk0 bs=4M conv=fsync status=progress
```

progress copy or dd | dd cheat

```bash
dd if=/dev/urandom of=/dev/null status=progress bs=1G count=1 oflag=direct
dd if=/dev/urandom | pv | dd of=/dev/null
```
- **bs** : sets the if and of sizes to bytes; block size (base 10 integer, 1G=1024×1024×1024 bytes = 1.073 GB);
- **count** : number of blocks (1 means that 1 block of 1G is copied);
- **oflag=direct** : uses direct I/O data, avoiding the buffer cache; it speeds up the process
