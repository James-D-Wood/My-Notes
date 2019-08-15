# How to start the CloudSQL Proxy and connect via the psql utility on terminal
(This is a lazy, lazy cheat sheet)

To start the proxy:
```
./cloud_sql_proxy -dir=/cloudsql \
  -instances=[instance] \
  -credential_file=[credential_file]
```

To connect via command line psql client:
```
psql "host=/cloudsql/[instance] user=[user]"
```
