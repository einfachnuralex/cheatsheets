
# cron

https://unix.stackexchange.com/questions/296347/crontab-never-running-while-in-etc-cron-d

* Files in /etc/cron.d need to also list the user that the job is to be run under.
* You should also ensure the permissions and owner:group are set correctly (-rw-r--r-- and owned by root:root
* it seems that also the filename has a role. In my case I had added to etc/cron.d a file with a dot in the middle of the name and the job was never executed until I renamed it
* same problem here, dashes - in filename, changing them to underscores _ solved the problem, jobs ran immediately
