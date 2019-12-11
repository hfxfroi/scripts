# scripts
Collection of scripts- mostly for manipulating, filtering, and format-conversion of DNA sequence files. Feel free to use.

### How to use
Most scripts are written to accept the <-h> argument to display a help menu which should describe the function of the scripts as well as any optional or mandatory inputs.

Example:
The Perl program "alleles2taghap.pl" takes the ".alleles" output from the RADseq assembly program pyRAD and creates the ".taghap" format for the program fineRADstructure. To display the help menu, call the program like so:

    ./alleles2taghap.pl -h

Which will display:

    tkchafin@acamel-linux1:~/scripts$ ./alleles2taghap.pl -h

    alleles2taghap.pl by Tyler Chafin

    This script converts from the .alleles file output by pyRAD to create the input for fineRADstructure

    NOTE:
	- All samples are assumed to be diploid.
	- Sample names CANNOT contain underscores.
	- Columns containing Ns or gaps will be deleted from final output
	- Popmap file should be tab-delimited, like so: SampleName [tab] PopID
	- If populations to include/exclude are not given, all samples in popmap are used.
	- You can specify multiple popIDs as: ID1+ID2+ID3, as long as these match IDs in popmap
	- For the -s filter, singletons are evaluated within the selected subset of individuals

    Options:
	-a	: Path to input file (.alleles)
	-p	: Path to popmap file (tab-delimited)
	-o	: Output file prefix. [Default = out, i.e. out.taghap]
	-c	: Min number of samples for which data must be present per locus [Default = 1]
	-n	: Minumum proportion of loci an individual must be present at to be retained [def = 0.2]
	-i	: PopIDs to include in output file (e.g. -i pop1+pop4)
	-x	: PopIDs to exclude (e.g. -x catenatus or -x sistrTX+sistrIN)
	-m	: Maximum number of SNPs per locus. Loci exceeding are deleted [default:10]
	-s	: Skip SNPs that are singletons [Boolean; Default = false]
	-h	: Displays this help message

    Program killed: Help menu called.

### Contents
Here is a (probably) complete list of the scripts contained here, and generally what they do. All scripts written in Python require Python3.
```
alleles2taghap.pl	: Converts from pyRAD .alleles format to input for fineRadStructure
averageFastStructure.pl	: Combines multiple replicate runs of FastStructure
batchBUCKY.pl		: Pipeline for running BUCKy. Old and probably broken.
collapse_baits.py	: For filtering baits by SNP count from BaitsTools output
collapseHaps.pl		: Collapse sequences to redundant consensus sequences
compare2seqs.pl		: This was a learning exercise. Just compares sequences.
concatFasta.py		: Script to concatenate fastas (No help menu- use argv)
concatenateNexus.py	: Concatenate Nexus alignments and calculate partitions block
condenseAlleles.pl	: Creates a consensus of alleles (input as FASTA) per individual
count_residues.pl	: Counts residues in an amino acid alignment
fast2distruct.pl	: Tries to parse FastStructure ouputs to create DISTRUCT input
fasta2length.pl		: Calculate non-gap character length of sequences
fasta2nexus.pl		: Converts FASTA to NEXUS format
fasta2phylip.py		: Converts from FASTA to PHYLIP and PHYLIP to FASTA, nothing fancy
findBreaksVCF.py	: Breaks contigs in VCF to chunks of X parsimony-informative SNPs, for running MDL
fill_quartets.py	: Sorts through TICR output to find missed quartets (for debugging only) (no help menu - use argv)
filter_loci.pl		: Parses a directory of FASTA alignments, and blacklists those with too low alignment coverage
filterLoci.py		: Filters a pyRAD .loci file on individual coverage and number of parsimony-informative sites
fixedSNP.pl		: Parses PHYLIP file to find differentially fixed SNPs between two given populations
genesFromGFF.pl		: Extracts elements from a FASTA file, given a GFF file of annotations
liftoverCoords.py	: Converts coordinates between assemblies (e.g. CanFam2 to CanFam3) and makes MareyMap inputs
makeHyde.py		: Makes inputs for HyDe- Hybrid Detection program
makePopArt.py		: Python program to make inputs for PopArt (haplotype network program) from FASTA
makeSAMOVA.pl		: Makes inputs for SAMOVA given FASTA and coordinates, with automatic clustering by distance
newhybs2distruct.py	: Takes posterior probs (PofZ.txt) from NewHybrids and makes inputs to run DISTRUCT
newhybs2props.py	: Calculates geneological assignment proportions from NewHybrids, outputs table and files to spoof DISTRUCT
nremover.pl		: My version of Steve Mussmann's nremover script, for filtering DNA alignments
parallelMB.pl		: For running batches of MrBayes on a cluster, in parallel per locus
phylip2bgc.pl		: Converts PHYLIP alignment to inputs for BGC (inference of Bayesian Genomic CLines)
phylip2biNumNex.py	: Converts PHYLIP to bi-allelic numerically coded NEXUS for PhyloNet's MLE_BiMarkers
phylip2ecoevolity.pl	: Converts PHYLIP to the NEXUS format needed for ecoevolity.
phylip2introgress.pl	: Converts PHYLIP to inputs for R package INTROGRESS (introgession analyses)
phylip2newhybrids.pl	: Creates inputs for NewHybrids, with missing data filters built in
phylip2nexus.pl		: Converts PHYLIP to NEXUS
phylip2structure.pl	: Converts PHYLIP alignment of SNPs to inputs for STRUCTURE
phylipFilterPops.pl	: Filters SNPs for creating PoMo-IQTREE inputs
process_ecoevolity.sh	: Runs the post-processing for ecoevolity outputs
pseudoHaploidize.py	: Script to haploidize FASTA-formatted sequences by randomly sampling alleles at heterozygous sites
pyrad2fasta.pl		: Extracts genewise alignments from pyRAD .loci format, and writes FASTA for each
seq2structure.pl	: I assume somehow different than phylip2structure, I don't remember honestly
short2fullPopmap.pl	: Does a very specific thing to my tab-delimited popmap files
slidingWindowGC.pl	: Calculates GC content along a sliding window down a sequence
snps2phy.sh		: Shell script to convert pyRAD .snp output to PHYLIP format
splitFASTA.pl		: Breaks a FASTA file into a user-defined number of chunks. For helping parse a large genome
splitFastaPops.py	: Pulls subsets from FASTA file to new FASTA file, given tab-delimited table of population IDs
splitStackedFasta.pl	: Splits FASTA of specifically-formatted collapsed read clusters
stacks2fasta.pl		: Fromats output of STACKS to a new FASTA for variable loci, but querying cstacks catalog
structure2newhy.pl	: Converts STRUCTURE file to input for NewHybrids
subsetPhy.py		: Quickly written and shitty script to subset taxa from a PHYLIP alignment
subsetSnps.py		: Given a list of desired columns, subsets SNPs from a STRUCTURE file
sumls.sh		: A bash alias for doing something with ls
summaryGFF.pl		: Something old and incomplete.
treeExpansion.py	: Converts a Newick tree of clade names, expanded to all taxa in given tab-delimited file
trimFastq.pl		: Perl script for end-trimming FASTQ reads
utm2latlong.py		: Converts UTM to and from latitude and longitudes
vcf2phylip.py		: VCF to PHYLIP
```
