# VALK-tool-
Bioinformatic pipeline optimized for the processing and assessment of variants at the ALK gene locus.

Specifically, the VALK tool selects fusion variants involving the ALK locus with molecular coverage >2 (INFO_MOL_COUNT) and fusion reads > 25 (INFO_READ_COUNT). The panel includes two control target genes, namely TBP and HMBS.  Both controls must have a molecular count of >2 to pass QC (ROW_TYPE= “ProcControl”; FILTER= “PASS”). In addition, the tool selects ALK gene copy-number gains or losses (ROW_TYPE= “CNV”; FILTER= “GAIN” or FILTER= “LOSS”) when CNV Ratio is >1.15 or >0.85, respectively. As recommended by the manufacturer, to make a CNV call the P-value must be >10-5 and the MAPD (Median of the Absolute values of all Pairwise Differences) must be <0.4. MAPD is a quality metric that estimates coverage variability between adjacent amplicons in CNV analyses. The higher MAPD the lower coverage uniformity, resulting in a higher probability of erroneous CNV calls.  Finally, according to our data false positives are less likely in SNPs and very likely in MNPs. For this reason, the algorithm makes a positive call as long as any of the following five conditions is met:

1. SNPs in the HotSpot file that have passed the Oncomine Variants 5.10 filter and that were detected in at least one molecular count with ≥15 reads (Rowtype= “SNP”; INFO.A.FAO ≥1; INFO.A.AO ≥15; FILTER= “PASS”; FUNC1.oncomineVariantClass= "Hotspot") 

2. SNPs that have passed the Oncomine Variants (5.10) filter and that were detected in at least two molecular counts (Rowtype= “SNP”; INFO.A.FAO ≥2; FILTER= “PASS” FUNC1.oncomineVariantClass= "Hotspot”);  

3. SNPs that have been detected in at least two molecular counts with ≥25 reads (Rowtype= “SNP”; INFO.A.FAO ≥2; INFO.A.AO ≥25)

4. Variants different from MNPs that have been detected in ≥25 molecular counts with ≥200 reads and AF ≥0.03 (Rowtype≠ “mnp”; INFO.A.FAO ≥25; INFO.A.AO ≥200; INFO.A.AF >0.03)

5. All variants that have been detected in ≥50 molecular counts with ≥200 reads and an AF ≥0.03, excluding the positions chr2: 29443609 to 29443611 in the ALK locus, which involves six consecutive guanines (G) (INFO.A.FAO ≥50; INFO.A.AO ≥200:  INFO.A.AF >0.03; POS≠ “29443609”, “29443610”, “29443611”).

All computations were performed in R v.3.6.3 using additional packages. Specifically, the Tcl/Tk package that was used to provide the end-user an intuitive graphical interface to carry out the entire filtering process. In addition, the Scales (v1.1.1) package, which contains functions that convert data values to perceptual properties, was used to transform the raw data obtained from the non-filtered-oncomine.tsv files into interpretable values for the end-user.
