# Android cheatsheet

## ADB

### list installed packages

> sudo adb shell pm list packages

### Backup app data

> sudo adb backup -f package.ba package-name

Options:

* -f: file to backup
* -apk: with apk


### Restore app data

> sudo adb restore org.fedorahosted.freeotp.ba

### App data for manual backup

com.commerzbank.photoTAN
org.fedorahosted.freeotp
at.harnisch.android.fueldb
ak.alizandro.smartaudiobookplayer
com.cerience.reader.app (Repligo Reader)
com.fsck.k9
com.blizzard.bma

## Loop Backup

for i in $(cat apps.txt); do adb backup -f $i.ba $i ; done
