# Proposal: Next Low‑Latency Tuning Topics

This repo already covers: SYSCTL (General, Network, Sockdev, TCP mem, Mem overcommit, High PPS, THP) and SYSTEMD (General). Below are complementary, high‑impact additions worth adding next.

## CPU and Scheduling

- CPU isolation for critical workloads
  - Boot: `isolcpus=managed_nohz,2-5 nohz_full=2-5 rcu_nocbs=2-5`
  - Pin workload threads: `taskset`, `cset`, or `systemd` `CPUAffinity=`
- Performance governor and C‑states
  - `cpupower frequency-set -g performance`
  - Optional boot (measure): `intel_pstate=disable intel_idle.max_cstate=0 processor.max_cstate=1 idle=poll`
- Real‑time scheduling for latency‑critical services
  - `SCHED_FIFO`/`SCHED_RR` with `CPUSchedulingPolicy=` and `CPUSchedulingPriority=`
- NUMA locality
  - `numactl -N 0 -m 0 <cmd>`; keep IRQs, NIC queues and workers on the same NUMA node
- IRQ affinity (pair NIC queues with CPUs)
  - `/proc/irq/*/smp_affinity_list`, `irqbalance --banirq` or disable and set manually

## Network Stack (sysfs, ethtool, sysctl)

- RPS/RFS/XPS placement
  - `/sys/class/net/ethX/queues/rx-*/rps_cpus`, `/queues/tx-*/xps_cpus`, and `rfs_table_size`
- NIC offloads and coalescing
  - `ethtool -K ethX gro off lro off tso off gso off rxvlan off txvlan off` (validate per workload)
  - `ethtool -C ethX rx-usecs 0 rx-frames 1 tx-usecs 0 tx-frames 1` for minimal coalescing
- RX/TX ring sizing
  - `ethtool -G ethX rx 4096 tx 4096` (match NIC capability and PPS)
- Busy polling
  - `sysctl -w net.core.busy_read=50 net.core.busy_poll=50` and per‑socket `SO_BUSY_POLL`
- Backlogs and softirq budgets
  - `net.core.netdev_max_backlog`, `net.core.netdev_budget`, `net.core.netdev_budget_usecs`, `net.core.dev_weight`
- Queue length and conntrack (if NAT/firewall present)
  - `ip link set ethX txqueuelen 10000`, `net.netfilter.nf_conntrack_max=…`

## TCP/UDP specifics

- Congestion control and pacing: `net.ipv4.tcp_congestion_control=bbr` (or `bbr2` where available)
- Buffers: `net.core.{rmem,wmem}_max`, `net.ipv4.tcp_{rmem,wmem}`
- Fast Open and low‑latency path: `net.ipv4.tcp_fastopen=3`, `net.ipv4.tcp_low_latency=1`
- Path MTU, initial windows and GRO/GSO strategy (validate with traffic patterns)

## VM and Memory (beyond THP/overcommit)

- Swappiness and dirty path: `vm.swappiness=1`, `vm.dirty_ratio=10`, `vm.dirty_background_ratio=5` (starting points)
- HugeTLB (1G/2M) pages for pinned memory
  - Boot reserve example: `hugepagesz=1G hugepages=8`; bind with `numactl`
- Map count and watermarks: `vm.max_map_count`, `vm.min_free_kbytes`

## I/O and Filesystems

- Block I/O scheduler
  - Boot: `scsi_mod.use_blk_mq=1`; per‑device scheduler `none`/`mq-deadline` for NVMe/SAS
- Filesystem mount options: `noatime,nodiratime` for read‑heavy paths
- NVMe specifics: tune queue depth and IRQ affinity per queue

## SYSTEMD: service hardening + latency

- Keep existing limits; additionally consider `TasksMax=infinity`, `Delegate=yes` (containers)
- Use `CPUAffinity=`, `NUMAPolicy=preferred`/`NUMAMask=` to keep locality
- Only apply `MemoryHigh=`, `IOWeight=`, `CPUQuota=` if intentional throttling is desired

## Kernel boot parameters (opt‑in, measure impact)

- `mitigations=off` (security trade‑off; benchmark before/after)
- `nosmt` (or prefer targeted CPU isolation instead)
- `nosoftlockup nowatchdog`
- `iommu=pt` or `iommu=off` for trusted NIC paths

## Measurement & Methodology (add a guide)

- Traffic/latency tools: `pktgen`, `MoonGen`, `TRex`; report latency via HdrHistogram/CDFs
- Observability: `perf`, `bcc`/`bpftrace`, `ethtool -S`, `nstat`, `ss -tinp`, `sar`, `pidstat`
- Ship baseline apply/revert scripts per area to ensure repeatability

## Suggested new docs (file stubs)

- `RPS-XPS.md` — sizing/placement for RPS/RFS/XPS and IRQ affinity
- `ETHTOOL.md` — offloads, coalescing, rings, what to measure in `-S`
- `BUSY-POLL.md` — kernel sysctls and per‑socket options
- `KERNEL-BOOT.md` — latency‑oriented boot parameters
- `CPU-ISOLATION.md` — isolcpus/nohz_full/rcu_nocbs + NUMA strategies
- `IO-SCHEDULER.md` — NVMe/block scheduler and FS options
- `MEASUREMENT.md` — methodology and tooling

> All values above are starting points. Validate on your hardware, kernel, NIC, and workload before rolling out broadly.
