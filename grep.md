# grep

## tail with grep live

```bash
tail -f file | grep --line-buffered my_pattern
```

## grep with miltiple search terms

AND

```bash
grep -E 'pattern1.*pattern2' filename
```

OR

```bash
grep -e pattern1 -e pattern2 filename
grep -E 'pattern1|pattern2' filename
```

## grep files without comments

```bash
grep -v -e '^#' -e '^$' squid.conf
```
- **e** : regex (^# : #, ^$ : empty line)
- **v** : invert match

## grep search recursive

```bash
grep -r -e "debconf"
```
- **r** : recursive

# grep for ip

```bash
ip address show wlp2s0 | grep -Eo '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' | head -n 1
```

# samples

Grep file for lines without beginning # (^#) or [ (^[) or empty line (^$)

```
cat inventory/*.inv | grep -v -e '^$' -e '^\[' -e '^#'
```
