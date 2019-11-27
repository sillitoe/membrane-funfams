# CATH FunFams / Membrane Interactions

Use CATH Functional Families (FunFams) to investigate conservation patterns of residues involved in membrane interactions.

## Dataset

Create FunFams and structural clusters for the following CATH superfamilies:

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

## Files

Create tarball of FunFam and Structural Cluster alignments for each superfamily:

```
$ cat sfam_ids.txt | awk '{print $1}' | \
    xargs -I XXX sh -c 'find /cath/data/v4_2_0/funfam/families/XXX "(" -name "*.sto" -or "(" -name "*FF_SSG9*" -and -type f ")" ")" -printf "%f\\0" | tar -zcf data/XXX.sto.tgz -C /cath/data/v4_2_0/funfam/families/XXX --null -T -'
```

These files have been included in the `data/` directory of this repo.

### Sequence Diversity (DOPS)

When looking for highly conserved residues, it is important to only consider alignments with significant amount of sequence diversity (otherwise all positions look highly conserved). The DOPS score is a measure of sequence diversity within the alignment - for functional site studies we usually only process alignments with a DOPS score >= 70.

DOPS can be found in the STOCKHOLM alignment format, along with lots of other meta data:

```sh
$ grep -C5 'DOPS' 2.30.29.30-ff-9309.reduced.sto
#=GF ID 2.30.29.30/FF/9309
#=GF DE Uncharacterized protein
#=GF AC 2.30.29.30/FF/9309
#=GF TP FunFam
#=GF DR CATH: 4.2
#=GF DR DOPS: 2.976
#=GS A0A1D8PD25/553-664  AC A0A1D8PD25
#=GS A0A1D8PD25/553-664  OS Candida albicans SC5314
#=GS A0A1D8PD25/553-664  DE Age1p
#=GS A0A1D8PD25/553-664  DR GENE3D; 66899cd80a8e40edbd99d416420e03fc/553-664;
#=GS A0A1D8PD25/553-664  DR ORG; Eukaryota; Fungi; Dikarya; Ascomycota; Saccharomycotina; Saccharomycetes; Saccharomycetales; Debaryomycetaceae; Candida; Candida albicans;
```

### Structural Clusters

Structural clusters essentially glue FunFam alignments together by identifying structurally equivalent residues between the FunFams.

For each superfamily:

* perform all-against-all structure comparison between structural representatives within FunFams (ie one representative CATH domain per FunFam)
* generate structural clusters for these representatives (9A)
* create multiple structural alignment within structural clusters (CORA)
* use structurally equivalent positions within the alignment to glue original FunFam sequence alignments together

### See also

FunFam and Structural Clusters files:

[https://github.com/sillitoe/cath-structural-cluster-example](https://github.com/sillitoe/cath-structural-cluster-example)

Useful CATH API endpoints:

[https://github.com/UCLOrengoGroup/cath-api-docs#functional-families-funfams](https://github.com/UCLOrengoGroup/cath-api-docs#functional-families-funfams)

Code to glue alignments together:

[https://github.com/UCL/cathpy](https://github.com/UCL/cathpy)

