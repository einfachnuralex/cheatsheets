
# shortcuts

| shortcut | Description     |
| :------------- | :------------- |
| C-a c    | Create new screen window   |
| C-a d    | Detach   |
| C-a 0-9  | Change to window 0-9 |

# screen session

Start

```
screen
```

Error start, when logon with user per su or sudo
`Cannot open your terminal '/dev/pts/5' - please check.`

```
script /dev/null
```

Join

```
screen -x
```

# multi user

http://wiki.networksecuritytoolkit.org/index.php/HowTo_Share_A_Terminal_Session_Using_Screen

Create screen named session

```
screen -S shared
```

Mark session multiuser & add user

```
Ctrl-a :multiuser on
Ctrl-a :acladd user2
```

User2 join with

```
screen -x user1/shared
```
