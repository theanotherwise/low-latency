# Devices / Sockets

```bash
sysctl vm.max_map_count
sysctl net.core.somaxconn
sysctl net.ipv4.tcp_max_syn_backlog
sysctl net.core.optmem_max
sysctl net.core.netdev_max_backlog
```

```
sysctl -w vm.max_map_count=1048576
sysctl -w net.core.somaxconn=65535
sysctl -w net.ipv4.tcp_max_syn_backlog=65535
sysctl -w net.core.optmem_max=65536
sysctl -w net.core.netdev_max_backlog=250000
```
