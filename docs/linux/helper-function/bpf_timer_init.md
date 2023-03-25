# Helper function `bpf_timer_init`

<!-- [FEATURE_TAG](bpf_timer_init) -->
[:octicons-tag-24: v5.15](https://github.com/torvalds/linux/commit/b00628b1c7d595ae5b544e059c27b1f5828314b4)
<!-- [/FEATURE_TAG] -->

This helper initializes a [timer](../ebpf-concepts/timers.md).

## Definition

<!-- [HELPER_FUNC_DEF] -->
Initialize the timer.
First 4 bits of `flags` specify clockid.
Only CLOCK_MONOTONIC, CLOCK_REALTIME, CLOCK_BOOTTIME are allowed.
All other bits of `flags` are reserved.
The verifier will reject the program if `timer` is not from
the same `map`.


**Returns**
0 on success.
`-EBUSY` if `timer` is already initialized.
`-EINVAL` if invalid `flags` are passed.
`-EPERM` if `timer` is in a map that doesn't have any user references.
The user space should either hold a file descriptor to a map with timers
or pin such map in bpffs. When map is unpinned or file descriptor is
closed all timers in the map will be cancelled and freed.

`#!c static long (*bpf_timer_init)(struct bpf_timer *timer, void *map, __u64 flags) = (void *) 169;`
<!-- [/HELPER_FUNC_DEF] -->

## Usage

### Program types

This helper call can be used in the following program types:

<!-- TODO use generated list as soon as we can exclude functions from inherited groups -->
<!-- verifier.c excludes tracing programs from using timers -->
 * [BPF_PROG_TYPE_CGROUP_DEVICE](../program-type/BPF_PROG_TYPE_CGROUP_DEVICE.md)
 * [BPF_PROG_TYPE_CGROUP_SKB](../program-type/BPF_PROG_TYPE_CGROUP_SKB.md)
 * [BPF_PROG_TYPE_CGROUP_SOCK](../program-type/BPF_PROG_TYPE_CGROUP_SOCK.md)
 * [BPF_PROG_TYPE_CGROUP_SOCKOPT](../program-type/BPF_PROG_TYPE_CGROUP_SOCKOPT.md)
 * [BPF_PROG_TYPE_CGROUP_SOCK_ADDR](../program-type/BPF_PROG_TYPE_CGROUP_SOCK_ADDR.md)
 * [BPF_PROG_TYPE_CGROUP_SYSCTL](../program-type/BPF_PROG_TYPE_CGROUP_SYSCTL.md)
 * [BPF_PROG_TYPE_FLOW_DISSECTOR](../program-type/BPF_PROG_TYPE_FLOW_DISSECTOR.md)
 * [BPF_PROG_TYPE_LSM](../program-type/BPF_PROG_TYPE_LSM.md)
 * [BPF_PROG_TYPE_LWT_IN](../program-type/BPF_PROG_TYPE_LWT_IN.md)
 * [BPF_PROG_TYPE_LWT_OUT](../program-type/BPF_PROG_TYPE_LWT_OUT.md)
 * [BPF_PROG_TYPE_LWT_SEG6LOCAL](../program-type/BPF_PROG_TYPE_LWT_SEG6LOCAL.md)
 * [BPF_PROG_TYPE_LWT_XMIT](../program-type/BPF_PROG_TYPE_LWT_XMIT.md)
 * [BPF_PROG_TYPE_SCHED_ACT](../program-type/BPF_PROG_TYPE_SCHED_ACT.md)
 * [BPF_PROG_TYPE_SCHED_CLS](../program-type/BPF_PROG_TYPE_SCHED_CLS.md)
 * [BPF_PROG_TYPE_SK_LOOKUP](../program-type/BPF_PROG_TYPE_SK_LOOKUP.md)
 * [BPF_PROG_TYPE_SK_MSG](../program-type/BPF_PROG_TYPE_SK_MSG.md)
 * [BPF_PROG_TYPE_SK_REUSEPORT](../program-type/BPF_PROG_TYPE_SK_REUSEPORT.md)
 * [BPF_PROG_TYPE_SK_SKB](../program-type/BPF_PROG_TYPE_SK_SKB.md)
 * [BPF_PROG_TYPE_SOCKET_FILTER](../program-type/BPF_PROG_TYPE_SOCKET_FILTER.md)
 * [BPF_PROG_TYPE_SOCK_OPS](../program-type/BPF_PROG_TYPE_SOCK_OPS.md)
 * [BPF_PROG_TYPE_SYSCALL](../program-type/BPF_PROG_TYPE_SYSCALL.md)
 * [BPF_PROG_TYPE_TRACING](../program-type/BPF_PROG_TYPE_TRACING.md)
 * [BPF_PROG_TYPE_XDP](../program-type/BPF_PROG_TYPE_XDP.md)

### Example