# code

## 00-DNA Sequencing Alignment
- [00.01-DNA-sequence-processing.md](00.01-DNA-sequence-processing.md): Markdown file with code used corresponding toe "DNA Sequence Processing" section in Methods. From raw data to calling of methlyation state at all loci.
- [00.02-C1-alignment.sh](https://github.com/hputnam/Meth_Compare/blob/master/code/00.02-C1-alignment.sh)
- [00.03-lambda-alignment.sh](https://github.com/hputnam/Meth_Compare/blob/master/code/00.03-lambda-alignment.sh)
- [00.04-MethCompare_MultiQC.ipynb](https://github.com/hputnam/Meth_Compare/blob/master/code/00.04-MethCompare_MultiQC.ipynb): Script used to run MultiQC on trimmed and aligned BS reads that generates the input files for 00.05-FormatMultiQC.Rmd.
- [00.05-FormatMultiQC.Rmd](https://github.com/hputnam/Meth_Compare/blob/master/code/00.05-FormatMultiQC.Rmd): This script produces **Figure 1** and **Supplementary Tables 1-3** from MultiQC output files. It also calculates lambda conversion efficiency based on the ratio of the sum of all unmethylated cytosines in CHG and CHH context to the sum of methylated and unmethylated cytosines in CHG and CHH and generates an intermediate file lamda_alignments_descriptive_stats.csv that is the input file for 00.06-CompareConversionEfficiency.Rmd.
- [00.06-CompareConversionEfficiency.Rmd](https://github.com/hputnam/Meth_Compare/blob/master/code/00.06-CompareConversionEfficiency.Rmd): This script generates **Supplementary Tables 4-5** and **Supplementary Figure 1** boxplots of conversion efficiency estimates. These include lamda alignments descriptive stats, conversion efficiency based on lambda alignments, estimated conversion efficiency based on coral alignments for each sample, and ANOVA statistics comparing conversion efficiency calculation methods across library preparation methods.

## 01-CpG Coverage

- [01.01-qualimap2.sh](https://github.com/hputnam/Meth_Compare/blob/master/code/01.01-qualimap2.sh):  This script runs Qualimap bamqc and multi-bamQC on deduplicated WBGS and MDBBS and non-deduplicated RRBS sorted bam files for each species, and produces both individual sample Qualimap reports and multi-sample BAM QC reports (which include PCAs for each species).
- [01.02-Qualimap\_MultiBamQC\_PCA.Rmd](https://github.com/hputnam/Meth_Compare/blob/master/code/01.02-Qualimap_MultiBamQC_PCA.Rmd):  This script takes in the sample summary tables reported in the multi-sample BAM QC reports, runs PCA, and generates **Supplementary Figure 2** score plots for each species.
- [01.03-Mcap\_CpG\_coverageXdepth.ipynb](https://github.com/hputnam/Meth_Compare/blob/master/code/01.03-Mcap_CpG_coverageXdepth.ipynb):  This script totals CpGs at different levels of coverage for individual _M. capitata_ samples and for pooled _M. capitata_ samples based on method and downsampled to different sequencing depths.
- [01.04-Pact\_CpG\_coverageXdepth.ipynb](https://github.com/hputnam/Meth_Compare/blob/master/code/01.04-Pact_CpG_coverageXdepth.ipynb):  This script totals CpGs at different levels of coverage for individual _P. acuta_ samples and for pooled _P. acuta_ samples based on method and downsampled to different sequencing depths.

#### Downsampling analysis
- [01.05-SubsampleFQsPact.sh](https://github.com/hputnam/Meth_Compare/blob/master/code/01.05-SubsampleFQsPact.sh):  This script pools trimmed reads by method for P. acuta samples and randomly downsamples read pairs at 50M, 100M, 150M, and 200M.
- [01.06-SubsampleFQsMcap.sh](https://github.com/hputnam/Meth_Compare/blob/master/code/01.05-SubsampleFQsMcap.sh):  This script pools trimmed reads by method for M. capitata samples and randomly downsamples read pairs at 50M, 100M, 150M, and 200M.
- [01.07-SubsampleBmrkPact.sh](https://github.com/hputnam/Meth_Compare/blob/master/code/01.07-SubsampleBmrkPact.sh):  This script performs Bismark alignment of P. acuta downsampled reads, methylation extraction, deduplicates WGBS and MBDBS downsampled reads, generates cytosine reports, generates sorted bam files, and generates 5x coverage files.
- [01.08-SubsampleBmrkMcap.sh](https://github.com/hputnam/Meth_Compare/blob/master/code/01.08-SubsampleBmrkMcap.sh):  This script performs Bismark alignment of M. capitata downsampled reads, methylation extraction, deduplicates WGBS and MBDBS downsampled reads, generates cytosine reports, generates sorted bam files, and generates 5x coverage files.

#### Coverage plots and sequencing saturation estimation
- [01.09-Genome\_CpG\_coverage\_analysis.Rmd](https://github.com/hputnam/Meth_Compare/blob/master/code/01.09-Genome_CpG_coverage_analysis.Rmd):  This script generates **Figure 2** CpG coverage plots from CpG_coverageXdepth script outputs for individual samples and downsampling analysis output. It also perform sequencing saturation estimation based on a Michaelis-Menten model and generates **Supplementary Figure 3**.

#### Generate union bedgraphs for CpGs with 5x coverage
- [01.10-Mcap-Canonical-Coverage-Track.ipynb](https://github.com/hputnam/Meth_Compare/blob/master/code/01.10-Mcap-Canonical-Coverage-Track.ipynb)
- [01.11-Pact-Canonical-Coverage-Track.ipynb](https://github.com/hputnam/Meth_Compare/blob/master/code/01.11-Pact-Canonical-Coverage-Track.ipynb)

#### Upset plots
- [01.12-Generate\_UpsetPlot\_input.ipynb](https://github.com/hputnam/Meth_Compare/blob/master/code/01.12-Generate_UpsetPlot_input.ipynb):  This script sorts and merges by method sample bedgraphs of CpG loci with 5x coverage for each species. It then generates a union bed file for each species from merged begraphs, and genome CpG bedgraph (contains all CpG loci in the genome).
- [01.13-GenerateUpsetPlot.Rmd](https://github.com/hputnam/Meth_Compare/blob/master/code/01.13-GenerateUpsetPlot.Rmd):  This script generates **Figure 3** upset plot from the output of 01.12-Generate\_UpsetPlot\_input.ipynb for each species.

## 02-Methylation characterization
- [02.01-5xUnionBedCpGs_PCA.Rmd](https://github.com/hputnam/Meth_Compare/blob/master/code/02.01-5xUnionBedCpGs_PCA.Rmd): This script performs PCA on CpG methylation data from union bedgraphs from 01.10-Mcap-Canonical-Coverage-Track.ipynb and 01.11-Pact-Canonical-Coverage-Track.ipynb, and generates **Supplementary Figure 4**.
- [Generating-Genome-Feature-Tracks.ipynb](https://github.com/hputnam/Meth_Compare/blob/master/scripts/Generating-Genome-Feature-Tracks.ipynb): Create gene, CDS, intron, flanking region, and intergenic feature tracks for *M. capitata* and *P. acuta* genomes
- [Characterizing-CpG-Methylation-5x.ipynb](https://github.com/hputnam/Meth_Compare/blob/master/scripts/Characterizing-CpG-Methylation-5x.ipynb): Characterize methylation status and genomic locations of CpGs in individual sample data for both species using `bedtools`
- [Characterizing-CpG-Methylation-5x-Union.ipynb](https://github.com/hputnam/Meth_Compare/blob/master/scripts/Characterizing-CpG-Methylation-5x-Union.ipynb): Characterize methylation status and genomic locations of CpGs from 5x union bedgraphs for both species using `bedtools`
- [Characterizing-CpG-Methylation-5x-Union-Summary-Plots.Rmd](https://github.com/hputnam/Meth_Compare/blob/master/scripts/Characterizing-CpG-Methylation-5x-Union-Summary-Plots.Rmd): Create summary tables and stacked barplots to understand methylation status and genomic locations of 5x union CpGs in both species
- [Identifying-Genomic-Locations.ipynb](https://github.com/hputnam/Meth_Compare/blob/master/scripts/Identifying-Genomic-Locations.ipynb): Characterize genomic locations of CpGs in upset plots and method-associated DMC using `bedtools`
- [Identifying-Genome-Features-Summary.Rmd](https://github.com/hputnam/Meth_Compare/blob/master/scripts/Identifying-Genome-Features-Summary.Rmd): Create summary tables for upset plot data and various method-associated DMC categories

## 03-Genomic Location of Methylation


## 04-Correlation of Percent Methylation of Shared CpG Loci 


## 05-Proportion of Detected CpGs for Orthologs
