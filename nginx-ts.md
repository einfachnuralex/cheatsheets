
nginx troubleshooting too many open files

# get pid
ps aux | grep nginx

# see limits
cat /proc/pid/limits

# see open files
ls -l /proc/pid/fd/*
