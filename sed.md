
## intro sed

Replace **cat** with **dog**

```bash
sed 's/cat/dog/' old_file > new_file #First
sed 's/cat/dog/5' old_file > new_file #5 times
sed 's/cat/dog/g' old_file > new_file #All
sed '/dragon/s/cat/dog/g' old_file > new_file #Only lines with dragon
sed '/dragon/!s/cat/dog/g'old_file > new_file #All, except lines with dragon
```
## sed with environment variables

```
sed 's/foo/$BAR/g'
sed "s/foo/$BAR/g"
```

## replace in file

```
sed -i -e 's/few/asd/g' hello.txt
```

## delete line in file

```
sed -i '76d' ~/.ssh/known_hosts
```

## replace line

```
sed -i 's/search.*/search psynet.lan tast.lan/g' /etc/resolv.conf
```

## Remove blank lines
```bash
sed '/^$/d' old_file > new_file
```

## Converting between UNIX and Windows
```bash
sed 's/.$//' dos_file > unix_file
sed 's/$'"/`echo \\\r`/" unix_file > dos_file #bash
sed 's/$/\r/' unix_file > dos_file # gsed 3.02.80 or higher
```
