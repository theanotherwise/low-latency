# SYSCTL-High PPS

```bash
# High number of TIME_WAIT
sysctl net.ipv4.tcp_max_tw_buckets
sysctl net.core.dev_weight
sysctl net.core.dev_weight_rx_bias
```

```bash
# safe
sysctl -w net.ipv4.tcp_max_tw_buckets=500000
sysctl -w net.core.dev_weight=128
sysctl -w net.core.dev_weight_rx_bias=32

# bump
sysctl -w net.ipv4.tcp_max_tw_buckets=2000000
sysctl -w net.core.dev_weight=300
sysctl -w net.core.dev_weight_rx_bias=64
```
