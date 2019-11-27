# FunFams

Provide FunFams and structural clusters for the following CATH superfamilies:

  * PH (2.30.29.30)
  * PI3K_C2 (2.60.40.150)
  * C2 (2.60.40.150)
  * C1 (3.30.60.20)
  * PX (3.30.1520.10)
  * FYVE (3.30.40.10)
  * BAR (1.20.1270.60)
  * ENTH (1.25.40.90)
  * SH2 (3.30.505.10)
  * CRAL_TRIO (3.40.525.10)


Create tarball of FunFam and Structural Cluster alignments for each superfamily:

```
$ cat sfam_ids.txt | awk '{print $1}' | \
    xargs -I XXX sh -c 'find /cath/data/v4_2_0/funfam/families/XXX "(" -name "*.sto" -or "(" -name "*FF_SSG9*" -and -type f ")" ")" -printf "%f\\0" | tar -zcf data/XXX.sto.tgz -C /cath/data/v4_2_0/funfam/families/XXX --null -T -'
```

More information on FunFam and Structural Clusters files can be found [here](https://github.com/sillitoe/cath-structural-cluster-example)
