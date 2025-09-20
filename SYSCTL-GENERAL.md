## Ports

```bash
sysctl net.ipv4.ip_local_port_range
```

```bash
sysctl -w net.ipv4.ip_local_port_range="1024 65535"
```

## Memory Overcommit

```bash
sysctl vm.overcommit_memory
```

```bash
grep -E 'CommitLimit|Committed_AS|MemTotal|SwapTotal' /proc/meminfo
```

### Test / Dev Environments

```bash
sysctl -w vm.overcommit_memory=1
```

### DB / Kafka

```bash
sysctl -w vm.overcommit_memory=2
sysctl -w vm.overcommit_ratio=80
```