# scBSTools
single cell BS-seq toolkits
##iBSTools
&emsp;&emsp;scBStools(single-cell Bisulfite Sequencing Tools) is an integrated tools for comprehensive analysis of single cell bisulfite sequencing(scWGBS) reads.
&emsp;&emsp;Due to the low coverage and large variation of single-cell WGBS profiles, the previous tools could not be directly used to identify the DNA methylation patterns from single-cell WGBS data. We developed a comprehensive suite (scBStools) to perform a wide variety of single-cell WGBS analysis. scBStools comprised of a serial of tools of bisulfite sequencing reads mapping and quality control, methylation ratio assessment and statistics at single-base resolution, but new advanced tools for DNA methylation patterns (under-methylated, inter-methylated and variably methylated regions) identification, annotation and heterogeneity assessment, as well as identification and clustering group analysis of DMRs for a population of single cell samples. The manuscript has been prepared.

&emsp;&emsp;scBSTools has four modules:
* **towig** - methylation level file to Wiggle format
* **sc_pattern** - identification of methylation patterns  of genomic reigons for single cell
* **sc_dmr** - identification of differentially methylated regions among cells
* **heter_assess** - assess heterogeneity between cells

![workflow](https://github.com/methylation/scBSTools/blob/master/imgs/scBSTools.png "foo")

--
###Install
scBSTools can be used directly after decompressing. 
```
unzip scBSTools-master.zip
```

--
###Manual

* These are simple examples, more details please read the [scBSTools wiki]()

__Usage:__ Convert "H1_sc_bt2.bismark.cov" into "wig" format. Methy counts is in col 5,unmethy counts is in col 6.
```shell
towig -t bismark -n H1 -r hg19.fa -i H1_sc_bt2.bismark.cov -o H1_wig
```
__Usage:__ Identify methylation patterns from "H1_wig/".
```shell
sc_pattern -i H1_sc_wig/ -o H1_sc_pattern/ -n H1_sc
```

__Usage:__ Identify differentially methylated regions for a specific genomic regions between single cell methylomes.
```shell
sc_dmr -r reference.bed -rh 1 -w cell_wig_list.txt -o diff
```
__Usage:__ Identify reference methylation patterns regions from mutiple methylomes in "wig_list.txt".
```shell
heter_assess -path ./software/scBSTools_v1.1.0/ -w wig_list.txt -o heter_assess
```
--
###Using Tips

1. If you use PBS(Portable Batch System) in your cluster server, **avoid to appoint relative path** for `-o,--outdir` and other parameters which need to assign path because workspace will be changed when pbs file is submitted. 

2. wiggle format
More detail information in [UCSC Genome Browser: Wiggle Track Format (WIG)](http://genome.ucsc.edu/goldenPath/help/wiggle.html).

3. construction information
scBSTools is contructed in `R3.1.3` and `perl v5.16.3`. 
and scBSTools is tested in R2.x and perl v5.10.x... 
iBSTools just employs basic funtions in `R` and `perl`. So almost all of versions of R and perl is available.

4. dependence relationship
towig is independent. Input could come from `BSMAP`,`Bismark` or ENCODE, Roadmap, TCGA.
sc_pattern is independent. 
sc_dmr requires sc_pattern. 
