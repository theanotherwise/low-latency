```bash
sysctl net.core.rmem_max
sysctl net.core.wmem_max
sysctl net.core.rmem_default
sysctl net.core.wmem_default
sysctl net.ipv4.tcp_rmem
sysctl net.ipv4.tcp_wmem

sysctl net.ipv4.udp_rmem_min
sysctl net.ipv4.udp_wmem_min
sysctl net.ipv4.udp_mem
```

```bash
sysctl -w net.core.rmem_max=16777216
sysctl -w net.core.wmem_max=16777216
sysctl -w net.core.rmem_default=524288
sysctl -w net.core.wmem_default=524288
sysctl -w net.ipv4.tcp_rmem="4096 524288 16777216"
sysctl -w net.ipv4.tcp_wmem="4096 524288 16777216"

sysctl -w net.ipv4.udp_rmem_min=16384
sysctl -w net.ipv4.udp_wmem_min=16384
sysctl -w net.ipv4.udp_mem="762282 1016380 1524564"
```