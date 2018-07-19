# DKMS

dkms add -m vboxhost -v 5.0.4 -k 4.1.0-pf1
dkms install -m vboxhost -v 5.0.4 -k 4.1.0-pf1
dkms build -m vboxhost -v 5.0.4 -k 4.1.0-pf1 
dkms build -m vboxhost -v 5.0.4 -k 3.16.0-4-amd64
dkms install -m vboxhost -v 5.0.4 -k 3.16.0-4-amd64
