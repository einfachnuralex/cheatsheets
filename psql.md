
# Connect to postgres (local)

```
sudo -u postgres psql
```

# Connect to postgres (remote)

```
psql -h 10.16.38.24 -U postgres -W
```

# Change passwd

```
ALTER USER postgres WITH PASSWORD 'secret';
```

# List all users

```
SELECT * FROM pg_user;
or
\du
```
