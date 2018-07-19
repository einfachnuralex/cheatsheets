
# SSH keys

## Ubuntu/Debian: re-generate ssh keys

```
rm -v /etc/ssh/ssh_host_*
dpkg-reconfigure openssh-server
```

## User ssh key

```
ssh-keygen -b 4096 -t rsa -f .ssh/id_rsa -q -N ""
```

# Config

```
Host test-xenial
  Hostname 192.168.2.33
  User ubuntu
  IdentityFile ~/.ssh/alex.pem
  LocalForward 4444 192.168.10.254:4444
```

> ssh -i Downloads/alex.pem -L 4444:192.168.10.254:4444 ubuntu@192.168.2.33

# Commands

```
ESCAPE CHARACTERS
     When a pseudo-terminal has been requested, ssh supports a number of
     functions through the use of an escape character.

     A single tilde character can be sent as ~~ or by following the tilde by
     a character other than those described below.  The escape character
     must always follow a newline to be interpreted as special.  The escape
     character can be changed in configuration files using the EscapeChar
     configuration directive or on the command line by the -e option.

     The supported escapes (assuming the default ‘~’) are:

     ~.      Disconnect.

     ~^Z     Background ssh.

     ~#      List forwarded connections.

     ~&      Background ssh at logout when waiting for forwarded connection
             / X11 sessions to terminate.

     ~?      Display a list of escape characters.

     ~B      Send a BREAK to the remote system (only useful if the peer sup‐
             ports it).

     ~C      Open command line.  Currently this allows the addition of port
             forwardings using the -L, -R and -D options (see above).  It
             also allows the cancellation of existing port-forwardings with
             -KL[bind_address:]port for local, -KR[bind_address:]port for
             remote and -KD[bind_address:]port for dynamic port-forwardings.
             !command allows the user to execute a local command if the
             PermitLocalCommand option is enabled in ssh_config(5).  Basic
             help is available, using the -h option.

     ~R      Request rekeying of the connection (only useful if the peer
             supports it).

     ~V      Decrease the verbosity (LogLevel) when errors are being written
             to stderr.

     ~v      Increase the verbosity (LogLevel) when errors are being written
             to stderr.
```
