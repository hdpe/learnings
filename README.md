# learnings

## nginx Optimisation

max concurrent requests:

```
events {
  worker_connections x;
}
```

must exceed file descriptor limit (*3? File required for each client, each proxy_pass, each local port); can set with:

```
worker_rlimit_nofile 8192;
```

Note this lives in *main (top-level) context* (can't define in nginx/conf.d/... files).

SE Linux boolean reqd to support `worker_rlimit_nofile`:

```
setsebool -P httpd_setrlimit 1
```
