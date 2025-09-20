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