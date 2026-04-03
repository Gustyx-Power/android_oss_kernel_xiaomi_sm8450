# XtraAether Kernel Changelogs

## Base Configuration
- Google LTS 5.10.252
- KernelSU-Next 3.1.0
- SUSFS 2.1.0-R26

---

## Version: Mamad-Ibn-Solowie

### Scheduler Improvements
- Added BORE (Burst-Oriented Response Enhancer) Scheduler
  - Credits: WiL
  - Improves system responsiveness under load
  - Tunable via sysctl parameters

- Added ADIOS (Adaptive Deadline I/O Scheduler) v3.2.0
  - Credits: Pzqqt
  - Optimized I/O scheduling for better performance

### Power Management
- Added Bypass Charging feature
  - Kernel-side implementation with thermal-based current limiting
  - Prevents battery degradation during extended usage

### Filesystem & Storage
- Enabled CONFIG_XATTR_TMPFS=y
  - Required for Mountify modules compatibility
  - Improves tmpfs extended attributes support

---

## Version: Bahlil-D-Etanols

### Compiler Optimizations
- Polly+ ThinLTO optimization enabled
  - Improved code generation and performance
  - Reduced binary size

### Power Management
- Added POWERSUSPEND v2h
  - Adaptive hibernation support
  - Automatic sleep management
  - Better battery life during idle

### Network Stack Enhancements
- Default TCP Congestion: BBR
  - Better network throughput and latency
  - Optimized for modern networks

- Enabled CONFIG_NETFILTER_XT_MATCH_QTAGUID
  - eBPF-based network filtering
  - Improved packet processing efficiency

- Enabled CONFIG_INET_DIAG
  - Socket monitoring capabilities
  - Better network diagnostics

- Enabled CONFIG_INET_TCP_DIAG
  - TCP connection monitoring
  - Enhanced network debugging

- Enabled CONFIG_NETFILTER_NETLINK
  - Netfilter communication to userspace
  - Improved firewall management

- Enabled CONFIG_NF_CONNTRACK_MARK
  - Connection marking system
  - Better traffic classification

---

## Version: Semantic

### Memory Management
- Swappiness: Default 45
  - Balanced swap usage
  - Optimized for mobile workloads

### GPU Configuration
- GPU Power Level: Default 3
  - Balanced performance and efficiency
  - Optimized thermal management

### Display Drivers
- Fixed pp_cfg display drivers
  - Improved display stability
  - Better color accuracy

---

## Credits
- WiL: BORE Scheduler implementation
- Pzqqt: ADIOS Scheduler implementation
- Xtra Manager Software Community: Development and testing