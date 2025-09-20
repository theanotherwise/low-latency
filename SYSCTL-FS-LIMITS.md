```bash
sysctl fs.file-max
sysctl fs.nr_open
sysctl fs.inotify.max_user_instances
sysctl fs.inotify.max_user_watches
```

```bash
sysctl -w fs.file-max=1048576
sysctl -w fs.nr_open=1048576
sysctl -w fs.inotify.max_user_instances=8192
sysctl -w fs.inotify.max_user_watches=1048576
```