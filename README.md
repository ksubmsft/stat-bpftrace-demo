A (one-off) bpftrace script to look for the top 10 userspace callers of the following:
  + `vfs_statfs`
  + Variants of `stat(2)`:
    `newstat`, `newlstat`, `newfstat`, `newfstatat`
  + `nfs4_getattr`
  + `nfs4_xdr_enc_getattr`

To use:
1. Download [stat.bt](https://raw.githubusercontent.com/ksubmsft/stat-bpftrace-demo/main/stat.bt)
2. Run `bpftrace stat.bt|tee stat_out.txt`, and hit `Ctrl-C` after a few minutes.
3. `stat_out.txt` can later be processed to get the statistics we need.
