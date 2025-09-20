# low-latency

## TCP Buffers

### Check

```bash
sysctl net.core.rmem_max
sysctl net.core.wmem_max
sysctl net.core.rmem_default
sysctl net.core.wmem_default
sysctl net.ipv4.tcp_rmem
sysctl net.ipv4.tcp_wmem
```

### Set

```bash
sysctl -w net.core.rmem_max=16777216
sysctl -w net.core.wmem_max=16777216
sysctl -w net.core.rmem_default=524288
sysctl -w net.core.wmem_default=524288
sysctl -w net.ipv4.tcp_rmem="4096 524288 16777216"
sysctl -w net.ipv4.tcp_wmem="4096 524288 16777216"
```

## Devices / Sockets

### Check

```bash
sysctl vm.max_map_count
sysctl net.core.somaxconn
sysctl net.ipv4.tcp_max_syn_backlog
sysctl net.core.optmem_max
sysctl net.core.netdev_max_backlog
```

### Set

```
sysctl -w vm.max_map_count=1048576
sysctl -w net.core.somaxconn=65535
sysctl -w net.ipv4.tcp_max_syn_backlog=65535
sysctl -w net.core.optmem_max=65536
sysctl -w net.core.netdev_max_backlog=250000
```
