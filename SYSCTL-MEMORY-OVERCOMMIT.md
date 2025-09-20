```bash
sysctl vm.overcommit_memory

grep -E 'CommitLimit|Committed_AS|MemTotal|SwapTotal' /proc/meminfo
```

```bash
# Test / Dev Environments
sysctl -w vm.overcommit_memory=1

# DB / Kafka
sysctl -w vm.overcommit_memory=2
sysctl -w vm.overcommit_ratio=80

# Stateless
sysctl -w vm.overcommit_memory=0
```
