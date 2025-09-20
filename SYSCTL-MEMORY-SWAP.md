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
