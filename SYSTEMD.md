# SystemD

```bash
[Service]
LimitCORE=infinity
LimitSTACK=infinity
LimitFSIZE=infinity
LimitMEMLOCK=infinity
LimitNOFILE=infinity
LimitNPROC=infinity
```

## Scheduling

```bash
CPUSchedulingPolicy=rr
CPUSchedulingPriority=99
IOSchedulingClass=realtime
IOSchedulingPriority=0
#CPUAffinity=0-1

# Baremetal
#NUMAPolicy=preferred
```
