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

### Stateless Prod

```bash
sysctl -w vm.overcommit_memory=0
```

## SWAP Memory

```bash
sysctl vm.swappiness
sysctl vm.dirty_background_ratio
sysctl vm.dirty_ratio=
```

```bash
sysctl -w vm.swappiness=1
sysctl -w vm.dirty_background_ratio=5
sysctl -w vm.dirty_ratio=10
```
