```bash
sysctl net.ipv4.tcp_fin_timeout
sysctl net.ipv4.tcp_tw_reuse
sysctl net.ipv4.tcp_timestamps
sysctl net.ipv4.tcp_sack
sysctl net.ipv4.tcp_window_scaling
sysctl net.ipv4.tcp_syn_retries
sysctl net.ipv4.tcp_retries2
sysctl net.ipv4.tcp_keepalive_time
sysctl net.ipv4.tcp_keepalive_intvl
sysctl net.ipv4.tcp_keepalive_probes
```

```bash
sysctl -w net.ipv4.tcp_fin_timeout=5
sysctl -w net.ipv4.tcp_tw_reuse=1
sysctl -w net.ipv4.tcp_timestamps=1
sysctl -w net.ipv4.tcp_sack=1
sysctl -w net.ipv4.tcp_window_scaling=1
sysctl -w net.ipv4.tcp_syn_retries=5
sysctl -w net.ipv4.tcp_retries2=8
sysctl -w net.ipv4.tcp_keepalive_time=300
sysctl -w net.ipv4.tcp_keepalive_intvl=60
sysctl -w net.ipv4.tcp_keepalive_probes=5
```