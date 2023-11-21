A (one-off) bpftrace script to look for the top 10 userspace callers of the following:
  + `vfs_statfs`
  + Variants of `stat(2)`:
    `newstat`, `newlstat`, `newfstat`, `newfstatat`
  + `nfs4_getattr`
  + `nfs4_xdr_enc_getattr`

To use:
1. Download [stat.bt](https://raw.githubusercontent.com/ksubmsft/stat-bpftrace-demo/main/stat.bt)
2. run `bpftrace stat.bt`, and hit `Ctrl-C` after a few minutes.

Sample output:

```
$ sudo bpftrace stat.bt
Attaching 9 probes...
Counting:
  vfs_statfs  nfs4_getattr, nfs4_xdr_enc_getattr
^C
=== Top 10 callers of stat syscalls ===
@stat_syscall_count[3143, gsd-color]: 2
@stat_syscall_count[222935, bash]: 2
@stat_syscall_count[1033, irqbalance]: 4
@stat_syscall_count[210884, tmux: server]: 32
@stat_syscall_count[77010, du]: 2082


=== Top 10 callers of vfs_statfs ===
@vfs_statfs_count[77010, du]: 2
@vfs_statfs_count[739, auditd]: 3


Top 10 callers of nfs4_getattr:
@nfs4_getattr_count[nfs4_getattr, 222935, bash]: 2
@nfs4_getattr_count[nfs4_getattr, 77010, du]: 1147


Top 10 callers of nfs4_xdr_enc_getattr:
@nfs4_xdr_enc_getattr_count[nfs4_getattr, 222935, bash]: 2
@nfs4_xdr_enc_getattr_count[nfs4_getattr, 77010, du]: 1147
```
