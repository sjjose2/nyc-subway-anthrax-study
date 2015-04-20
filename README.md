# Searching for anthrax in the New York City subway metagenome.

By Robert Petit III, Matthew Ezewudo, Sandeep J. Joseph and *Timothy D. Read,
Emory University School of Medicine, Atlanta, Georgia
\cite{Boyle-Vavra2015-ba}
##Introduction
In January 2015 Chris Mason and his team [published](http://www.sciencedirect.com/science/article/pii/S2405471215000022) 
an in-depth analysis of metagenomic data [(environmental shotgun DNA sequence)](http://en.wikipedia.org/wiki/Metagenomics) from samples isolated from public surfaces 
in the New York City (NYC) subway system. Along with a ton of really interesting findings, the authors claimed 
to have detected DNA from the bacterial biothreat pathogens *Bacillus anthracis* (which causes anthrax) and 
*Yersinia pestis* (causes plague) in some of the samples. This predictably led to a press firestorm and skepticism from
scientists on social media.  The authors followed up with an 
[re-analysis](http://microbe.net/2015/02/17/the-long-road-from-data-to-wisdom-and-from-dna-to-pathogen/) 
of the data on microbe.net, where they admitted that they overreached on the anthrax and plague claims based on the tools that they were using for detection.

*B. anthracis* is a Gram-positive bacterium that forms tough spores as part of its lifecycle.  The 5.2 M basepair (Mb) main chromosome is very similar to those of other bacteria in species informally called the '[*Bacillus cereus* group](http://genome.cshlp.org/content/22/8/1512)' (including *B. cereus*, *B. thuringiensis* and *B. mycoides*).  *Bacillus cereus* group strains in general are commonly found in soil but *B. anthracis* itself is very rare and generally associated with livestock grazing sites with a past history of anthrax.
What sets *B. anthracis* apart from close relatives is the presence of two plasmids: pXO1 (181kb), which carries the lethal toxin genes and pXO2 (94kb), which includes genes for a protective capsule.  Without one of these plasmids, *B. anthracis* is considered attenuated in virulence and unable to cause classic anthrax.  Other *B. cereus* group bacteria can have plasmids very similar to pXO1 and pXO2 but missing the important virulence genes.  Rarely, other *B. cereus* group carry pXO1 and appear to cause anthrax-like disease.  Its a confusing situation, not helped by the current overly-narrow species definitions.  This [recent review](http://www.annualreviews.org/doi/abs/10.1146/annurev.micro.091208.073255) gives more information.

The NYC subway metagenome study rasied very timely questions about using unbiased DNA sequencing for pathogen detection.  We were interested in this dataset as soon as the publication appeared and started looking deeper into why the anlysis software gave false positive results and indeed what exactly was found in the subway samples.  We decided to wrap up the results of our preliminary analysis and put it on this site.   This report focuses on the results for *B. anthracis* but we also did some preliminary work on  *Y.pestis* and may follow up on this later.  



##Methods Overview
The results are organized in 4 sections:  

1.  **Accessing metagenome data and controls:**  Where we obtained the data and how we constructed artificial controls by mixing recent whole genome shotgun data from pathogens and near-neighbors with NYC subway metagenome data.  
2.  **Mapping metagenome data to plasmids (and chromosomes):**    Looking at the patterns of sequence coverage over the key virulence associated plasmids, pXO1 , pXO2 (and pMT of *Y. pestis*) in metagenome samples and controls.  
3.  **Species identification with Kraken :** [Kraken](http://genomebiology.com/2014/15/3/R46) is a popular k-mer based software for read identification.  We showed that Kraken was a sensitive way to find *B. anthracis* when it was present in low abundance but the method also produced a small number of false positive reads on near-neighbor *B. cereus* sequence control data.  
4.  **Custom [SNP (single nucleotide polymorphism)](http://en.wikipedia.org/wiki/Single-nucleotide_polymorphism) assays for *B. anthracis* core genome:** We identified 31-mer words that corresponded to SNPs in the core genome of *B. anthracis* that were not found in close relatives. This gave a rapid specific test for *B. anthracis*.  However, we still detected two potential positive SNPs in one of the NYC subway samples.

##Summary of results

Our control experiments showed that direct mapping of sequences reads from the metagenome was a sensitive way to detect plasmids,  Plasmid reads were present when as little as 0.01x *B. anthracis* genome equivalents were added.  However, some *B. cereus* reads mapped to pXO2 because the strain we used probably contained a closely related mobile element.  What differentiated *B. anthracis* from the control was that coverage was evenly distributed across the plasmids.  We found that the NYC samples had evidence of quite deep coverage of *B. cereus*-like chromosome and plasmids, which was not an unexpected result.  The pattern of coverage of the plasmids qualitatively resembled *B. cereus* rather than *B. anthracis* although there were some reads in sample SRR1748708 that mapped across the part of the plasmid containing the lethal toxin gene cluster.  

We showed that Kraken was a sensitive tool for detection of *B. anthracis* down to at least 0.01X genome coverage.  However, the *B. cereus* control also gave us false positive *B. anthracis* reads, albeit at a lower incidence than the true positive.  On the NYC subway samples we obtained a reasonably large number of *B. anthracis* specific calls but this could be explained by the fact that the sample contained up to 50x chromosomal coverage of *B. cereus* group organisms.  

Our novel assay of 1,793 31-mers specific to the  *B. anthracis* core genome was sensitive at 0.01X *B. anthracis* genome coverage and did not give false positives on the *B. cereus* control at up to 5x coverage.  Surprisingly, we obtained 2 positive hits on on of the NYC subway samples. There are a number of possible reasons for this:

1.	*B. anthracis* is truly present in this sample at about 0.01x genome coverage along with a much greater number of *B. cereus* group organisms.  At this level of coverage we would expect to see some hits to the lethal toxin gene in pXO1, which we did. However, the reads that mapped inside the lethal toxin gene were found by BLASTN to be false positives.  It is possible that the 0.01x genome coverage the *B. anthracis* pXO1 reads stochastically missed the toxin gene and we were seeing false positive hits from the other *B. cereus* group strains present. Alternatively, we detected a *B. anthracis* variant that had lost its plasmids.  
2.	The SNPs are present in a *B. cereus* strain, very closely related to *B. anthracis* that has not been sequenced (if its sequence were available in a public database, it would have resulted in the SNPs being filtered out of consideration).  
3.	The SNPs were present in a *B. cereus* strain whose ancestor had at some point undergone homologous recombination in this area of the chromosome with an ancestor of *B. anthracis*.  
4.	The sequences were introduced through laboratory cross-contamination.  
5.	The SNPs were an artifact of random sequencing error.


At the present time, we believe the most likely explanation for the results is option 2.  There is no direct evidence for the lethal toxin.  The B. cereus close to *B. anthracis* lkely represents a small fraction of a mixture of *B. cereus* strains present.  

Deeper sequence coverage of this sample preferably combined with culture and PCR-based analysis would be helpful here.

##Perspective

We believe that one of the biggest messages to take from this investigation is that there is no one-size-fits-all approach to bacterial species indentification in metagenome samples.  There are several reasons for this.  Perhaps most importantly, there is no consistently applied definition for the boundary that divides bacterial species based on DNA sequence identity.  The main chromsomes of some bacteria from different species (like *B. cereus* and *B. anthracis*) can be >99% similar to each other in terms of DNA sequence identity.  Secondly, some species distinctions rely on the presence or absence of mobile elements like plasmids and phages(again *B. cereus* and *B. anthracis* are a great example), which are hard to model using a uniform approach like Kraken or Metaphlan. These genetic elements are often modular in structure with very similar 'backbones' but with key genes replaced.  Finally, the generalist species indentification programs rely on databases of sequenced genomes, which are not uniform in their coverage of different species, or different lineages within species.

Individual species will have their own unique features that can be used to extract information from metagenomic sequence. In this case, if you were to have an organism-specific detection algorthim for *B. cereus* you would need to account for the presence of the plasmids with at least 2 times the coverage of the chromsome.  You would also expect even coverage across all the sites in the plasmid.

Even if you have developed a sophisticated algorithm you will still need to use judgement in interpreting results.  In the case of the *B. cereus* group, we dont know what proportion of the cells were spores and what proportion were the in the more fragile vegative state. There is also still much that we dont know about bacteria in the environment, especialy the conditions under which they exchange DNA.  Can we say that its not natural to find evidence of a small number of "anthracis specific" SNPs on a *B. cereus* chromsome?  This could be becasue thsi strain has not been sequenced, or because of recombination, or convergent evolution. Judgement is especially important where the amount of data supporting a putative pathogen is small.  Obviously orthologous validation (culture, PCR etc) is really useful.

Finally, the negative result is subject to a lot of nuances.  The limit of detection will be affected by the amount of sequence generated and the complexity of the microbial community.

****

## 1. Accessing metagenome data and controls   
On February 10th 2015, we used *prefetch*, from [SRA Toolkit (v 2.4.4)](http://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.4.4/), 
to download each of the 1,572 runs associated with SRA study 
[SRP051511](http://trace.ncbi.nlm.nih.gov/Traces/study/?acc=SRP051511). 
We then converted each run from SRA format to FASTQ format using *fastq-dump*, again from SRA Toolkit (v 2.4.4). 
Each FASTQ file was also converted to FASTA format using *fastq_to_fasta* from 
[FASTX Toolkit (v 0.0.13.2)](http://hannonlab.cshl.edu/fastx_toolkit/download.html). For each SRA run we used the 
information contained in [SRP051511_info.txt](/data/methods/01-accessing-data-and-controls/nyc-supplementary-data/SRP051511_info.txt), acquired from SRP051511's RunInfo Table, to associate sample names used in the study with
their corresponding SRA run accessions.

We created the python script, 
[extract_pathogens.py](/data/methods/01-accessing-data-and-controls/extract-pathogens.py), 
to parse [DataTable5-metaphlan-metadata_v19.txt](//data/methods/01-accessing-data-and-controls/nyc-supplementary-data/DataTable5-metaphlan-metadata_v19.txt). 
From this we were able to determine which NYC samples contained reads associated with *Bacillus antracis* and 
the *Yersinia* genus. We then used another python script, 
[map-pathogens.py](/data/methods/01-accessing-data-and-controls/map-pathogens.py) 
in order to associate the NYC sample names with their corresponding SRA run accession.

The following runs were identified as containing reads associated with *Bacillus antracis* and the *Yersinia* genus:

#####*Bacillus anthracis*
| NYC Sample Name | SRA Run Accession      |
|-----------------|------------------------|
| P00134          | SRR1748707, SRR1748708 |
| P00497          | SRR1749083             |

#####Yersinia genus
| NYC Sample Name | SRA Run Accession |
|-----------------|-------------------|
| P00064          | SRR1748611        |
| P00070          | SRR1748618        |
| P00073          | SRR1748620        |
| P00102          | SRR1748663        |
| P00111          | SRR1748670        |
| P00164          | SRR1748743        |
| P00193          | SRR1748789        |
| P00208          | SRR1748804        |
| P00214          | SRR1748810        |
| P00230          | SRR1748826        |
| P00235          | SRR1748831        |
| P00239          | SRR1748835        |
| P00242          | SRR1748838        |
| P00243          | SRR1748839        |
| P00275          | SRR1748865        |
| P00279          | SRR1748869        |
| P00286          | SRR1748876        |
| P00294          | SRR1748884        |
| P00302          | SRR1748892        |
| P00303          | SRR1748893        |
| P00306          | SRR1748896        |
| P00321          | SRR1748911        |
| P00338          | SRR1748928        |
| P00347          | SRR1748936        |
| P00379          | SRR1748967        |
| P00382          | SRR1748970        |
| P00391          | SRR1748979        |
| P00392          | SRR1748980        |
| P00406          | SRR1748994        |
| P00416          | SRR1749003        |
| P00435          | SRR1749021        |
| P00475          | SRR1749061        |
| P00476          | SRR1749062        |
| P00494          | SRR1749080        |
| P00506          | SRR1749092        |
| P00604          | SRR1749188        |
| P00629          | SRR1749213        |
| P00653          | SRR1749237        |
| P00655          | SRR1749239        |
| P00660          | SRR1749244        |
| P00665          | SRR1749249        |
| P00707          | SRR1749291        |
| P00710          | SRR1749294        |
| P00718          | SRR1749302        |
| P00725          | SRR1749309        |
| P00767          | SRR1749350        |
| P00771          | SRR1749354        |
| P00779          | SRR1749362        |
| P00783          | SRR1749366        |
| P00803          | SRR1749386        |
| P00818          | SRR1749401        |
| P00916          | SRR1749496        |
| P00992          | SRR1749571        |
| P00993          | SRR1749572        |
| P00997          | SRR1749576        |
| P01002          | SRR1749581        |
| P01017          | SRR1749596        |
| P01020          | SRR1749599        |
| P01022          | SRR1749601        |
| P01036          | SRR1749615        |
| P01048          | SRR1749627        |
| P01052          | SRR1749631        |
| P01056          | SRR1749635        |
| P01063          | SRR1749642        |
| P01079          | SRR1749651        |
| P01093          | SRR1749665        |
| P01245          | SRR1749817        |
| P01270          | SRR1749835        |
| P01316          | SRR1749873        |
| P01337          | SRR1749894        |
| P01376          | SRR1749933        |
| P01606          | SRR1750038        |

### Creating metagenomic controls for *B. anthracis* and a close relative, *B. cereus*
As a control for these analysis we randomly selected NYC sample SRR1749070 which is *B anthracis* free and added 
different amounts of known *B. anthracis* or *B. cereus* sequences to it. Using these controls we produced
results we would expect to see if *B. anthracis* was present in the metagenomic sequences. We used *B. anthracis*
([DRR014739](http://trace.ncbi.nlm.nih.gov/Traces/sra/?run=DRR014739)) (strain H29: isolated in Zambia, unpublished data from Division of Infection and Immunity, Research Center for Zoonosis Control, Hokkaido Univerisity) and *B. cereus* 
([SRR642775](http://trace.ncbi.nlm.nih.gov/Traces/sra/?run=SRR642775)) (strain VD143, unpublished data from the Broad Institute) sequencing projects as our controls. The reads from the *B. anthracis* project were trimmed from 300bp (Illumina MiSeq) down to the first 100bp using *fastq_trimmer (v0.0.13.2)*
from FASTX Toolkit. This was necessary to make the reads more similar to the NYC sample, SRR1749070, which was 100bp 
Illumina HiSeq 2000 reads. This step was not necessary for the *B. cereus* control because it too was 100bp Illumina 
HiSeq 2000 reads. 

Each control was then randomly subsampled using *seqtk (commit 43ff625a3211b51f301cb356a34fb8d1e593d50a)* to 
0.1x, 0.25x, 0.5x, 1x, and 5x coverage. *B. anthracis* was additionally subsampled to 0.01x, 0.05x and 0.10x coverage. 
Coverage was estimated using the total size of the *B. anthracis* genome, the 
pXO1 plasmid and the pXO2 plasmids. For *B. cereus* we used only the total size of the *B. cereus* 
genome. These subsampled coverages were then added to the sequences of the *B. anthracis* free NYC sample SRR1749070. 
This produced multiple samples for each control, one with no control sequences and those with the different levels 
of coverage. These samples were then subjected to the same mapping pipeline as the *B. anthracis* positive 
samples menthion above. This process of downloading and preparing the controls for analysis was automated 
using the following scripts [get-anthracis-control.sh](/data/methods/01-accessing-data-and-controls/get-anthracis-control.sh) (*B. anthracis*) and
[get-cereus-control.sh](/data/methods/01-accessing-data-and-controls/get-cereus-control.sh) (*B. cereus*).

****

## 2. Mapping metagenome data to plasmids (and chromosomes)

### Mapping against pXO1 and pXO2 using BWA
We used *BWA (v 0.7.5a-r405)* to map reads from each of the NYC and control samples against reference 
pXO1 and pXO2 plasmids as well as reference *B. anthracis* and *B. cereus* completed genomes. We used the following 
references: pXO1 reference [CP009540](http://www.ncbi.nlm.nih.gov/nuccore/CP009540.1), pXO2 reference
[NC_007323](http://www.ncbi.nlm.nih.gov/nuccore/50163691), *B. anthracis* reference 
[CP009541](http://www.ncbi.nlm.nih.gov/nuccore/CP009541), and *B. cereus* reference
[NC_003909](http://www.ncbi.nlm.nih.gov/nuccore/NC_003909). The aligned reads in SAM format were then
converted to sorted BAM and indexed using *samtools (v 1.1)*. The per base coverage was extracted using 
*genomeCoverageBed* from *bedtools (v2.16.2)*. Coverage across the plasmids and chromosomes were plotted for mulitple
sliding windows by the Rscript *[plot-coverage.R](/data/methods/02-mapping/plot-coverage.R)*. Mapped reads
were extracted and saved in both FASTQ and FASTA format using *bam2fastq (v1.1.0)* and *fastq_to_fasta* 
from *FASTX Toolkit v 0.0.13.2*.

For pXO1, we focused on coverage of the virulence genes (*cya*, *lef*, *pagA* and *pagR*). To
visualize this, an alternate plot was created which included subplots of coverage of these genes using the RScript
*[plot-pxo1-anthrax-toxin-coverage.R](/data/methods/02-mapping/plot-pxo1-anthrax-toxin-coverage.R)*. The reads that mapped 
to each gene were also extracted and blasted (*blastn v2.2.30+)* against the NT database (built on Feb 9, 2015). For 
each gene, a count of the organism names of which the top five hits of each read belonged to was recorded. 

The analysis of the plasmids was automated using the following scripts 
*[map-anthracis-plasmids.sh](/data/methods/02-mapping/map-anthracis-plasmids.sh)*
(NYC samples) and *[map-anthracis-controls.sh](/data/methods/02-mapping/map-anthracis-controls.sh)* (control samples).
Analysis of the completed chromosomes was automated using the scripts 
*[map-bacilli-nyc.sh](/data/methods/02-mapping/map-bacilli-nyc.sh)* (NYC samples) and 
*[map-bacilli-controls.sh](/data/methods/02-mapping/map-bacilli-controls.sh)* (control samples).
Summaries of the results of mapping samples against pXO1, pXO2 and chromosomes were generated using the following scripts:
*[mapping-coverage-summary.py](/data/methods/02-mapping/mapping-coverage-summary.py)*, 
*[mapping-gene-summary.py](/data/methods/02-mapping/mapping-gene-summary.py)* and 
*[mapping-top-blast-hits-summary.py](/data/methods/02-mapping/mapping-top-blast-hits-summary.py)*

### pXO1 Results
For each sample we calculated the summary statistics of coverage across the complete pXO1 plasmid.
NYC sample SRR174708 has the best average coverage (2x), but each of the NYC samples have a median coverage of 
0x. These results are nearly the opposite of the *B. anthracis* control. Even at an estimated coverage of 0.25x, 
the mean coverage of pXO1 is 1.23x (median 1x). The mean coverage only improves as the estimated coverage of 
*B. anthracis* reads increases. The *B. cereus* control includes low levels of pXO1 overage.

####  Summary statistics of per base coverage against pXO1 for NYC samples and controls.
###### *NYC Subway System*
| Study      | Min. | 1st Qu. | Median | Mean   | 3rd Qu. | Max | Coverage Plots |
|------------|------|---------|--------|--------|---------|-----|----------------|
| SRR1749083 | 0    | 0.0000  | 0.0000 | 0.4652 | 0.0000  | 44  |[pXO1](/data/results/02-mapping/anthracis/SRR1749083/pXO1/coverage/SRR1749083-coverage.pdf), [Toxin](/data/results/02-mapping/anthracis/SRR1749083/pXO1/coverage/SRR1749083-anthrax-toxin.pdf)|
| SRR1748708 | 0    | 0.0000  | 0.0000 | 2.0766 | 4.0000  | 100 |[pXO1](/data/results/02-mapping/anthracis/SRR1748708/pXO1/coverage/SRR1748708-coverage.pdf), [Toxin](/data/results/02-mapping/anthracis/SRR1748708/pXO1/coverage/SRR1748708-anthrax-toxin.pdf)|
| SRR1748707 | 0    | 0.0000  | 0.0000 | 0.2506 | 0.0000  | 44  |[pXO1](/data/results/02-mapping/anthracis/SRR1748707/pXO1/coverage/SRR1748707-coverage.pdf), [Toxin](/data/results/02-mapping/anthracis/SRR1748707/pXO1/coverage/SRR1748707-anthrax-toxin.pdf)|
###### *B. anthracis* control
| Study            | Min. | 1st Qu. | Median  | Mean    | 3rd Qu. | Max | Coverage Plots |
|------------------|------|---------|---------|---------|---------|-----|----------------|
| SRR1749070-0x    | 0    | 0.0000  | 0.0000  | 0.0103  | 0.0000  | 2  |[pXO1](/data/results/02-mapping/anthracis-control/SRR1749070-0x/pXO1/coverage/SRR1749070-0x-coverage.pdf), [Toxin](/data/results/02-mapping/anthracis-control/SRR1749070-0x/pXO1/coverage/SRR1749070-0x-anthrax-toxin.pdf)|
|SRR1749070-0.01x  | 0	   | 0.0000	 | 0.0000	 | 0.0467  |	0.0000	 | 3   |[pXO1](/data/results/02-mapping/anthracis-control/SRR1749070-0.01x/pXO1/coverage/SRR1749070-0.01x-coverage.pdf), [Toxin](/data/results/02-mapping/anthracis-control/SRR1749070-0.01x/pXO1/coverage/SRR1749070-0.01x-anthrax-toxin.pdf)|
| SRR1749070-0.05x	| 0	   | 0.0000	 | 0.0000	 | 0.2169	 | 0.0000	 | 4   |[pXO1](/data/results/02-mapping/anthracis-control/SRR1749070-0.05x/pXO1/coverage/SRR1749070-0.05x-coverage.pdf), [Toxin](/data/results/02-mapping/anthracis-control/SRR1749070-0.05x/pXO1/coverage/SRR1749070-0.05x-anthrax-toxin.pdf)|
| SRR1749070-0.10x	| 0	   | 0.0000	 | 0.0000	 | 0.4877	 | 1.0000	 | 8   |[pXO1](/data/results/02-mapping/anthracis-control/SRR1749070-0.10x/pXO1/coverage/SRR1749070-0.10x-coverage.pdf), [Toxin](/data/results/02-mapping/anthracis-control/SRR1749070-0.10x/pXO1/coverage/SRR1749070-0.10x-anthrax-toxin.pdf)|
| SRR1749070-0.25x | 0    | 0.0000  | 1.0000  | 1.2305  | 2.0000  | 13  |[pXO1](/data/results/02-mapping/anthracis-control/SRR1749070-0.25x/pXO1/coverage/SRR1749070-0.25x-coverage.pdf), [Toxin](/data/results/02-mapping/anthracis-control/SRR1749070-0.25x/pXO1/coverage/SRR1749070-0.25x-anthrax-toxin.pdf)|
| SRR1749070-0.5x  | 0    | 1.0000  | 2.0000  | 2.4250  | 3.0000  | 20  |[pXO1](/data/results/02-mapping/anthracis-control/SRR1749070-0.5x/pXO1/coverage/SRR1749070-0.5x-coverage.pdf), [Toxin](/data/results/02-mapping/anthracis-control/SRR1749070-0.5x/pXO1/coverage/SRR1749070-0.5x-anthrax-toxin.pdf)|
| SRR1749070-1x    | 0    | 3.0000  | 4.0000  | 4.8863  | 6.0000  | 36  |[pXO1](/data/results/02-mapping/anthracis-control/SRR1749070-1x/pXO1/coverage/SRR1749070-1x-coverage.pdf), [Toxin](/data/results/02-mapping/anthracis-control/SRR1749070-1x/pXO1/coverage/SRR1749070-1x-anthrax-toxin.pdf)|
| SRR1749070-5x    | 0    | 19.0000 | 23.0000 | 24.3656 | 28.0000 | 175 |[pXO1](/data/results/02-mapping/anthracis-control/SRR1749070-5x/pXO1/coverage/SRR1749070-5x-coverage.pdf), [Toxin](/data/results/02-mapping/anthracis-control/SRR1749070-5x/pXO1/coverage/SRR1749070-5x-anthrax-toxin.pdf)|
###### *B. cereus* control
| Study            | Min. | 1st Qu. | Median | Mean   | 3rd Qu. | Max | Coverage Plots |
|------------------|------|---------|--------|--------|---------|-----|----------------|
| SRR1749070-0x    | 0    | 0.0000  | 0.0000 | 0.0103 | 0.0000  | 2    |[pXO1](/data/results/02-mapping/cereus-control/SRR1749070-0x/pXO1/coverage/SRR1749070-0x-coverage.pdf), [Toxin](/data/results/02-mapping/cereus-control/SRR1749070-0x/pXO1/coverage/SRR1749070-0x-anthrax-toxin.pdf)|
| SRR1749070-0.25x | 0    | 0.0000  | 0.0000 | 0.0368 | 0.0000  | 7   |[pXO1](/data/results/02-mapping/cereus-control/SRR1749070-0.25x/pXO1/coverage/SRR1749070-0.25x-coverage.pdf), [Toxin](/data/results/02-mapping/cereus-control/SRR1749070-0.25x/pXO1/coverage/SRR1749070-0.25x-anthrax-toxin.pdf)|
| SRR1749070-0.5x  | 0    | 0.0000  | 0.0000 | 0.0522 | 0.0000  | 9   |[pXO1](/data/results/02-mapping/cereus-control/SRR1749070-0.5x/pXO1/coverage/SRR1749070-0.5x-coverage.pdf), [Toxin](/data/results/02-mapping/cereus-control/SRR1749070-0.5x/pXO1/coverage/SRR1749070-0.5x-anthrax-toxin.pdf)|
| SRR1749070-1x    | 0    | 0.0000  | 0.0000 | 0.0912 | 0.0000  | 16  |[pXO1](/data/results/02-mapping/cereus-control/SRR1749070-1x/pXO1/coverage/SRR1749070-1x-coverage.pdf), [Toxin](/data/results/02-mapping/cereus-control/SRR1749070-1x/pXO1/coverage/SRR1749070-1x-anthrax-toxin.pdf)|
| SRR1749070-5x    | 0    | 0.0000  | 0.0000 | 0.4261 | 0.0000  | 53  |[pXO1](/data/results/02-mapping/cereus-control/SRR1749070-5x/pXO1/coverage/SRR1749070-5x-coverage.pdf), [Toxin](/data/results/02-mapping/cereus-control/SRR1749070-5x/pXO1/coverage/SRR1749070-5x-anthrax-toxin.pdf)|

To give an idea of the difference in coverages, below was coverage across the pXO1 plasmid at 1000bp
sliding windows with a 500bp overlap for three samples. SRR1748708 was selected because it has the greatest
mean coverage of the NYC samples. 
 
###### *NYC sample SRR1748708*
![SRR1748708](/data/results/02-mapping/anthracis/SRR1748708/pXO1/coverage/SRR1748708-coverage-1000bp.png "SRR1748708")
###### *B. anthracis* control 0.5x coverage
![B. anthracis control 0.5x coverage](/data/results/02-mapping/anthracis-control/SRR1749070-0.5x/pXO1/coverage/SRR1749070-0.5x-coverage-1000bp.png "B. anthracis control 0.5x coverage")
###### *B. cereus* control 5x coverage
![B. cereus control 5x coverage](/data/results/02-mapping/cereus-control/SRR1749070-5x/pXO1/coverage/SRR1749070-5x-coverage-1000bp.png "B. cereus control 5x coverage")

These three plots depict very different stories. In the *B. cereus* control, although there were few reads 
that mapped, there are regions of pXO1 that are similar to *B. anthracis*. However, SRR1748708 **did** have 
significant coverage accross the pXO1 plasmid. Comparing SRR1748708 and the *B. anthracis* control, the similar mean
coverages are very different from one another. SRR1748708 has regions of high coverage and regions of low coverage.
The *B. anthracis* control, on the other hand, has a very similar coverage across the complete pXO1 plasmid. This 
suggests SRR1748708 may contain a plasmid backbone that is shared among *Bacillus* species.

The pXO1 plasmid has a mean coverage of 2x in SRR1748708; were the genes associated with the 
anthrax toxin covered? Below are visualizations of SRR1748708 and the *B. anthracis* 0.5x and 5x controls that 
depict subplots of reads mapped to the *cya*, *lef*, *pagA* and *pagR* genes. For each of the plots below the 
top plot is coverage across the whole pXO1 plasmid. The coverage is based on 1,000bp sliding windows with an overlap 
of 500bp. Each subplot against the genes *pagA*, *pagR*, *lef* and *cya* was the actual coverage in that region.

###### *NYC sample SRR1748708*
![SRR1748708](/data/results/02-mapping/anthracis/SRR1748708/pXO1/coverage/SRR1748708-anthrax-toxin.png "SRR1748708")
###### *B. anthracis* control 0.5x coverage
![B. anthracis control 0.5x coverage](/data/results/02-mapping/anthracis-control/SRR1749070-0.5x/pXO1/coverage/SRR1749070-0.5x-anthrax-toxin.png "B. anthracis control 0.5x coverage")
###### *B. anthracis* control 5x coverage
![B. anthracis control 5x coverage](/data/results/02-mapping/anthracis-control/SRR1749070-5x/pXO1/coverage/SRR1749070-5x-anthrax-toxin.png "B. anthracis control 5x coverage")

The *B. anthracis* controls clearly showed a number of reads mapping to each of the genes. The total number of 
reads mapped to each gene for each sample was extracted (below). At 0.5x a total of 197 reads mapped to these 
genes. At 5x the coverage the total number of reads mapped jumped to 1,817. clearly evident. Looking at 
SRR1748708, the genes are essentially devoid of mapped reads but reads are mapped to these genes. Although only 72 
reads mapped to these genes it is necessary to investigate these reads further. 

####  Number of reads mapped to genes (*cya*, *lef*, *pagA* and *pagR*) related to the anthrax toxin.
###### *NYC Subway System*
| Sample     | *cya* | *lef* | *pagA* | *pagR* |
|------------|-------|-------|--------|--------|
| SRR1748707 | 8     | 2     | 2      | 0      |
| SRR1748708 | 30    | 22    | 18     | 2      |
| SRR1749083 | 4     | 10    | 2      | 0      |
###### *B. anthracis* control
| Sample           | *cya* | *lef* | *pagA* | *pagR* |
|------------------|-------|-------|--------|--------|
| SRR1749070-0x    | 0     | 0     | 0      | 0      |
| SRR1749070-0.01x | 0     | 0     | 4      | 0      |
| SRR1749070-0.05x | 8     | 2     | 11     | 1      |
| SRR1749070-0.10x | 14    | 7     | 11     | 1      |
| SRR1749070-0.25x | 29    | 28    | 24     | 2      |
| SRR1749070-0.5x  | 57    | 76    | 55     | 9      |
| SRR1749070-1x    | 107   | 148   | 108    | 16     |
| SRR1749070-5x    | 544   | 644   | 532    | 97     |
###### *B. cereus* control
| Sample           | *cya* | *lef* | *pagA* | *pagR* |
|------------------|-------|-------|--------|--------|
| SRR1749070-0x    | 0     | 0     | 0      | 0      |
| SRR1749070-0.25x | 0     | 0     | 0      | 0      |
| SRR1749070-0.5x  | 0     | 0     | 0      | 0      |
| SRR1749070-1x    | 0     | 0     | 0      | 0      |
| SRR1749070-5x    | 0     | 0     | 0      | 0      |

The next step was to determine the likely origin of the mapped reads in the each of the genes. In order to do so, 
we extracted these reads and saved them in FASTA format. We then BLASTed those reads against a local NT database 
(described above). We chose to only retain the top five hits for each read. Our goal was not to determine the 
exact organism of origin, but instead to get an idea of what these reads are mapping to (below). There was a 
clear difference between the results of the NYC sample SRR1748708 and the *B. anthracis* control. The reads from 
the *B. anthracis* controls most often return *B. anthracis* (~85%) as the top hit followed by *B. cereus* (~14.6%). 
The NYC samples did not have a top hit to *B. anthracis*. The most common was *B. thuringiensis* followed by various organisms including humans and other *Bacillus* species. It is important to state that in this case the 
total hit counts are not important. What is important is the difference between the NYC
samples and the control *B. anthracis*.

#### Organism names for each of the top NT blast hits of reads mapped to the anthrax toxin genes.
###### *NYC samples SRR1748707, SRR1748708, and SRR1749083*
| Organism                     |  Hit Count   |
|------------------------------|--------------|
| Bacillus thuringiensis       | 189          |
| Homo sapiens                 | 62           |
| Triticum aestivum            | 45           |
| Bacillus cereus              | 41           |
| Bacillus bombysepticus       | 22           |
| Pan troglodytes              | 17           |
| Cyprinus carpio              | 13           |
| Human DNA                    | 10           |
| Bacillus weihenstephanensis  | 7            |
| Bacillus toyonensis          | 7            |
| Staphylococcus xylosus       | 6            |
| Chlorocebus aethiops         | 4            |
| Nippostrongylus brasiliensis | 3            |
| Haemonchus placei            | 2            |
| Pongo abelii                 | 2            |
| TPA_exp: Homo                | 2            |
| Strongyloides stercoralis    | 1            |
| Diphyllobothrium latum       | 1            |
| Strongyloides papillosus     | 1            |
| Echinostoma caproni          | 1            |
###### *B. anthracis* controls (0.01x, 0.05x, 0.10x, 0.25x, 0.5x, 1x, and 5x)
| Organism            | Hit Count |
|---------------------|-----------|
| Bacillus anthracis  | 10736     |
| Bacillus cereus     | 1856      |
| Synthetic construct | 35        |
| Cyprinus carpio     | 2         |

### pXO2 Results
Similar to pXO1, we calculated the summary statistics of coverage across the complete pXO2 plasmid for
each sample . We observed similar patterns of coverage. Again NYC sample SRR174708 
has the best mean coverage (4.5x), but each of the NYC samples again have a median coverage of 0x. 
The *B. anthracis* 0.5x control has a mean coverage of 1.34x (median 1x). Again the mean coverage improves 
as the estimated coverage of *B. anthracis* reads increases. Finally, as before, the *B. cereus* control 
contained low levels of pXO2 coverage.

#### Summary statistics of per base coverage against pXO2 for NYC samples and controls.
###### *NYC Subway System*
| Study      | Min. | 1st Qu. | Median | Mean   | 3rd Qu. | Max  | Coverage Plots |
|------------|------|---------|--------|--------|---------|------|----------------|
| SRR1749083 | 0    | 0.0000  | 0.0000 | 2.1786 | 0.0000  | 3706 |[pXO2](/data/results/02-mapping/anthracis/SRR1749083/pXO2/coverage/SRR1749083-coverage.pdf)|
| SRR1748708 | 0    | 0.0000  | 0.0000 | 4.4961 | 0.0000  | 9863 |[pXO2](/data/results/02-mapping/anthracis/SRR1748708/pXO2/coverage/SRR1748708-coverage.pdf)|
| SRR1748707 | 0    | 0.0000  | 0.0000 | 0.3622 | 0.0000  | 707  |[pXO2](/data/results/02-mapping/anthracis/SRR1748707/pXO2/coverage/SRR1748707-coverage.pdf)|
###### *B. anthracis* control
| Study            | Min. | 1st Qu. | Median  | Mean    | 3rd Qu. | Max | Coverage Plots |
|------------------|------|---------|---------|---------|---------|-----|----------------|
| SRR1749070-0x    | 0    | 0.0000  | 0.0000  | 0.2483  | 0.0000  | 662 |[pXO2](/data/results/02-mapping/anthracis-control/SRR1749070-0x/pXO2/coverage/SRR1749070-0x-coverage.pdf)|
| SRR1749070-0.01x	| 0    |	0.0000  |	0.0000	 | 0.2772  |	0.0000	 | 667 |[pXO2](/data/results/02-mapping/anthracis-control/SRR1749070-0.01x/pXO2/coverage/SRR1749070-0.01x-coverage.pdf)|
| SRR1749070-0.05x	| 0    |	0.0000  |	0.0000	 | 0.3784  |	0.0000	 | 667 |[pXO2](/data/results/02-mapping/anthracis-control/SRR1749070-0.05x/pXO2/coverage/SRR1749070-0.05x-coverage.pdf)|
| SRR1749070-0.10x	| 0    |	0.0000  |	0.0000  |	0.4731  |	0.0000	 | 667 |[pXO2](/data/results/02-mapping/anthracis-control/SRR1749070-0.10x/pXO2/coverage/SRR1749070-0.10x-coverage.pdf)|
| SRR1749070-0.25x | 0    | 0.0000  | 0.0000  | 0.7916  | 1.0000  | 667 |[pXO2](/data/results/02-mapping/anthracis-control/SRR1749070-0.25x/pXO2/coverage/SRR1749070-0.25x-coverage.pdf)|
| SRR1749070-0.5x  | 0    | 0.0000  | 1.0000  | 1.3448  | 2.0000  | 667 |[pXO2](/data/results/02-mapping/anthracis-control/SRR1749070-0.5x/pXO2/coverage/SRR1749070-0.5x-coverage.pdf)|
| SRR1749070-1x    | 0    | 1.0000  | 2.0000  | 2.4348  | 3.0000  | 667 |[pXO2](/data/results/02-mapping/anthracis-control/SRR1749070-1x/pXO2/coverage/SRR1749070-1x-coverage.pdf)|
| SRR1749070-5x    | 0    | 8.0000  | 10.0000 | 11.4254 | 13.0000 | 670 |[pXO2](/data/results/02-mapping/anthracis-control/SRR1749070-5x/pXO2/coverage/SRR1749070-5x-coverage.pdf)|
###### *B. cereus* control
| Study            | Min. | 1st Qu. | Median | Mean   | 3rd Qu. | Max | Coverage Plots |
|------------------|------|---------|--------|--------|---------|-----|----------------|
| SRR1749070-0x    | 0    | 0.0000  | 0.0000 | 0.2483 | 0.0000  | 662 |[pXO2](/data/results/02-mapping/cereus-control/SRR1749070-0x/pXO2/coverage/SRR1749070-0x-coverage.pdf)|
| SRR1749070-0.25x | 0    | 0.0000  | 0.0000 | 0.2969 | 0.0000  | 667 |[pXO2](/data/results/02-mapping/cereus-control/SRR1749070-0.25x/pXO2/coverage/SRR1749070-0.25x-coverage.pdf)|
| SRR1749070-0.5x  | 0    | 0.0000  | 0.0000 | 0.3577 | 0.0000  | 676 |[pXO2](/data/results/02-mapping/cereus-control/SRR1749070-0.5x/pXO2/coverage/SRR1749070-0.5x-coverage.pdf)|
| SRR1749070-1x    | 0    | 0.0000  | 0.0000 | 0.4805 | 0.0000  | 688 |[pXO2](/data/results/02-mapping/cereus-control/SRR1749070-1x/pXO2/coverage/SRR1749070-1x-coverage.pdf)|
| SRR1749070-5x    | 0    | 0.0000  | 0.0000 | 1.3704 | 0.0000  | 782 |[pXO2](/data/results/02-mapping/cereus-control/SRR1749070-5x/pXO2/coverage/SRR1749070-5x-coverage.pdf)|

The coverage across the pXO2 plasmid at 1000bp sliding windows with a 500bp overlap for three 
samples is depicted below. SRR1748708 was selected because it has the greatest
mean coverage of the NYC samples. 


###### *NYC sample SRR1748708*
![SRR1748708](/data/results/02-mapping/anthracis/SRR1748708/pXO2/coverage/SRR1748708-coverage-1000bp.png "SRR1748708")
###### *B. anthracis* control 1x coverage
![B. anthracis control 1x coverage](/data/results/02-mapping/anthracis-control/SRR1749070-1x/pXO2/coverage/SRR1749070-1x-coverage-1000bp.png "B. anthracis control 1x coverage")
###### *B. cereus* control 5x coverage
![B. cereus control 5x coverage](/data/results/02-mapping/cereus-control/SRR1749070-5x/pXO2/coverage/SRR1749070-5x-coverage-1000bp.png "B. cereus control 5x coverage")

There was clearly a peak in each of the plots above, which is likely a repeat region within the 
*Bacillus* species. SRR1748708 mostly maps to this region. As with pXO1, the *B. anthracis* control 
maintains similar coverage accross the complete pXO2 plasmid. Unlike pXO1, there seems to be a number of 
regions in pXO2 that are very similar to *B. cereus* as depicted by the plot of the *B. cereus* control.

### Completed *B. anthracis* and *B. cereus* Chromosome Results
In order to demonstrate how similar the chromosomes of *B. anthracis* and *B. cereus* are to one another, we
also mapped reads to completed chromosomes. Summary statistics of mapped reads can be found below. Unlike the pXO1
and pXO2 plasmids each of the NYC samples have a mean coverage greater than 1x for both *B. anthracis* and *B. cereus*. 
The difference in the mean coverage between *B. anthracis* and *B. cereus* for each NYC sample is negligble
(SRR1748707:0.0555, SRR1749083:0.1124, and SRR1748708:0.5252). Again focusing on SRR1748708, because it has the 
greatest mean coverage against both *B. anthracis* and *B. cereus*, we can visualize the coverage accross each chromosome.

###### Coverage across *B. anthracis* for sample SRR1748708 
![SRR1748708](/data/results/02-mapping/bacilli-nyc/SRR1748708/anthracis/coverage/SRR1748708-coverage-10000bp.png "SRR1748708 against B. anthracis")

###### Coverage across *B. cereus* for sample SRR1748708 
![SRR1748708](/data/results/02-mapping/bacilli-nyc/SRR1748708/cereus/coverage/SRR1748708-coverage-10000bp.png "SRR1748708 against B. cereus")

Using 10kb sliding windows (5kb overlap), the two plots above show consistent coverage across both the *B. anthracis* 
and *B. cereus* chromosomes. The discrepency in peaks of coverage can be explained by the location of the origin 
of replication in each of the references. The other two samples, SRR1748707 and SRR1749083, show similar patterns 
of consistent coverage.  At first glance, these plots could be mistakenly taken as evidence for the presence of 
both *B. anthracis* and *B. cereus* in the NYC samples. Recall, the genomes of organisms within the *B. cereus group* 
are very similar to one another. Just how similar? Below are cross mappings of reads from *B. anthracis* and *B. cereus*
to one another.

###### Coverage across *B. anthracis* for *B. cereus* control at 5x coverage
![B. cereus control](/data/results/02-mapping/bacilli-controls/cereus-control/SRR1749070-5x/anthracis/coverage/SRR1749070-5x-coverage-10000bp.png "B. cereus control against B. anthracis")

###### Coverage across *B. cereus*  for *B. anthracis* control at 5x coverage
![B. anthracis control](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-5x/cereus/coverage/SRR1749070-5x-coverage-10000bp.png "B. anthracis control against B. cereus")

These two plots show *B. cereus* reads consistenly mapping to the *B. anthracis* chromosome and likewise *B. anthracis* 
reads consistenly mapping to the *B. cereus* chromosome. The similarity between the two chromosomes would likely cause 
difficulties distiguishing between the two organisms based on sequence homology alone.

#### Summary statistics of per base coverage against *B. anthracis* for NYC samples and controls.
###### *NYC Subway System*
| Study      | Min. | 1st Qu. | Median  | Mean    | 3rd Qu. | Max  | Coverage Plots |
|------------|------|---------|---------|---------|---------|------|----------------|
| SRR1748707 | 0    | 0.0000  | 1.0000  | 1.8449  | 3.0000  | 584  | *[B. anthracis](/data/results/02-mapping/bacilli-nyc/SRR1748707/anthracis/coverage/SRR1748707-coverage.pdf)* |
| SRR1748708 | 0    | 8.0000  | 16.0000 | 16.1112 | 23.0000 | 1346 | *[B. anthracis](/data/results/02-mapping/bacilli-nyc/SRR1748708/anthracis/coverage/SRR1748708-coverage.pdf)* |
| SRR1749083 | 0    | 2.0000  | 5.0000  | 5.6239  | 8.0000  | 186  | *[B. anthracis](/data/results/02-mapping/bacilli-nyc/SRR1749083/anthracis/coverage/SRR1749083-coverage.pdf)* |
###### *B. anthracis* control
| Study            | Min. | 1st Qu. | Median | Mean   | 3rd Qu. | Max | Coverage Plots |
|------------------|------|---------|--------|--------|---------|-----|----------------|
| SRR1749070-0x    | 0    | 0.0000  | 0.0000 | 0.3307 | 0.0000  | 524 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0x/anthracis/coverage/SRR1749070-0x-coverage.pdf)* |
| SRR1749070-0.01x | 0    | 0.0000  | 0.0000 | 0.3382 | 0.0000  | 524 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0.01x/anthracis/coverage/SRR1749070-0.01x-coverage.pdf)* |
| SRR1749070-0.05x | 0    | 0.0000  | 0.0000 | 0.3685 | 0.0000  | 524 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0.05x/anthracis/coverage/SRR1749070-0.05x-coverage.pdf)* |
| SRR1749070-0.10x | 0    | 0.0000  | 0.0000 | 0.4054 | 0.0000  | 524 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0.10x/anthracis/coverage/SRR1749070-0.10x-coverage.pdf)* |
| SRR1749070-0.25x | 0    | 0.0000  | 0.0000 | 0.5182 | 0.0000  | 524 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0.25x/anthracis/coverage/SRR1749070-0.25x-coverage.pdf)* |
| SRR1749070-0.5x  | 0    | 0.0000  | 0.0000 | 0.7062 | 1.0000  | 524 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0.5x/anthracis/coverage/SRR1749070-0.5x-coverage.pdf)* |
| SRR1749070-1x    | 0    | 0.0000  | 1.0000 | 1.0793 | 1.0000  | 524 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-1x/anthracis/coverage/SRR1749070-1x-coverage.pdf)* |
| SRR1749070-5x    | 0    | 2.0000  | 3.0000 | 4.0712 | 5.0000  | 529 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-5x/anthracis/coverage/SRR1749070-5x-coverage.pdf)* |
###### *B. cereus* control
| Study            | Min. | 1st Qu. | Median | Mean   | 3rd Qu. | Max | Coverage Plots |
|------------------|------|---------|--------|--------|---------|-----|----------------|
| SRR1749070-0x    | 0    | 0.0000  | 0.0000 | 0.3307 | 0.0000  | 524 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/cereus-control/SRR1749070-0x/anthracis/coverage/SRR1749070-0x-coverage.pdf)* |
| SRR1749070-0.25x | 0    | 0.0000  | 0.0000 | 0.4954 | 0.0000  | 525 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/cereus-control/SRR1749070-0.25x/anthracis/coverage/SRR1749070-0.25x-coverage.pdf)* |
| SRR1749070-0.5x  | 0    | 0.0000  | 0.0000 | 0.6688 | 1.0000  | 525 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/cereus-control/SRR1749070-0.5x/anthracis/coverage/SRR1749070-0.5x-coverage.pdf)* |
| SRR1749070-1x    | 0    | 0.0000  | 0.0000 | 1.0151 | 1.0000  | 525 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/cereus-control/SRR1749070-1x/anthracis/coverage/SRR1749070-1x-coverage.pdf)* |
| SRR1749070-5x    | 0    | 0.0000  | 3.0000 | 3.7523 | 6.0000  | 528 | *[B. anthracis](/data/results/02-mapping/bacilli-controls/cereus-control/SRR1749070-5x/anthracis/coverage/SRR1749070-5x-coverage.pdf)* |

#### Summary statistics of per base coverage against *B. cereus* for NYC samples and controls.
###### *NYC Subway System*
| Study      | Min. | 1st Qu. | Median  | Mean    | 3rd Qu. | Max | Coverage Plots |
|------------|------|---------|---------|---------|---------|-----|----------------|
| SRR1748707 | 0    | 0.0000  | 1.0000  | 1.7894  | 3.0000  | 350 | *[B. cereus](/data/results/02-mapping/bacilli-nyc/SRR1748707/cereus/coverage/SRR1748707-coverage.pdf)* |
| SRR1748708 | 0    | 7.0000  | 16.0000 | 15.5860 | 23.0000 | 455 | *[B. cereus](/data/results/02-mapping/bacilli-nyc/SRR1748708/cereus/coverage/SRR1748708-coverage.pdf)* |
| SRR1749083 | 0    | 2.0000  | 5.0000  | 5.5115  | 8.0000  | 146 | *[B. cereus](/data/results/02-mapping/bacilli-nyc/SRR1749083/cereus/coverage/SRR1749083-coverage.pdf)* |
###### *B. anthracis* control
| Study            | Min. | 1st Qu. | Median | Mean   | 3rd Qu. | Max | Coverage Plots |
|------------------|------|---------|--------|--------|---------|-----|----------------|
| SRR1749070-0x    | 0    | 0.0000  | 0.0000 | 0.3284 | 0.0000  | 521 | *[B. cereus](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0x/cereus/coverage/SRR1749070-0x-coverage.pdf)* |
| SRR1749070-0.01x | 0    | 0.0000  | 0.0000 | 0.3344 | 0.0000  | 521 | *[B. cereus](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0.01x/cereus/coverage/SRR1749070-0.01x-coverage.pdf)* |
| SRR1749070-0.05x | 0    | 0.0000  | 0.0000 | 0.3587 | 0.0000  | 521 | *[B. cereus](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0.05x/cereus/coverage/SRR1749070-0.05x-coverage.pdf)* |
| SRR1749070-0.10x | 0    | 0.0000  | 0.0000 | 0.3881 | 0.0000  | 521 | *[B. cereus](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0.10x/cereus/coverage/SRR1749070-0.10x-coverage.pdf)* |
| SRR1749070-0.25x | 0    | 0.0000  | 0.0000 | 0.4781 | 0.0000  | 521 | *[B. cereus](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0.25x/cereus/coverage/SRR1749070-0.25x-coverage.pdf)* |
| SRR1749070-0.5x  | 0    | 0.0000  | 0.0000 | 0.6293 | 1.0000  | 521 | *[B. cereus](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-0.5x/cereus/coverage/SRR1749070-0.5x-coverage.pdf)* |
| SRR1749070-1x    | 0    | 0.0000  | 0.0000 | 0.9291 | 1.0000  | 523 | *[B. cereus](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-1x/cereus/coverage/SRR1749070-1x-coverage.pdf)* |
| SRR1749070-5x    | 0    | 1.0000  | 3.0000 | 3.3184 | 5.0000  | 528 | *[B. cereus](/data/results/02-mapping/bacilli-controls/anthracis-control/SRR1749070-5x/cereus/coverage/SRR1749070-5x-coverage.pdf)* |
###### *B. cereus* control
| Study            | Min. | 1st Qu. | Median | Mean   | 3rd Qu. | Max | Coverage Plots |
|------------------|------|---------|--------|--------|---------|-----|----------------|
| SRR1749070-0x    | 0    | 0.0000  | 0.0000 | 0.3284 | 0.0000  | 521 | *[B. cereus](/data/results/02-mapping/bacilli-controls/cereus-control/SRR1749070-0x/cereus/coverage/SRR1749070-0x-coverage.pdf)* |
| SRR1749070-0.25x | 0    | 0.0000  | 0.0000 | 0.4956 | 0.0000  | 522 | *[B. cereus](/data/results/02-mapping/bacilli-controls/cereus-control/SRR1749070-0.25x/cereus/coverage/SRR1749070-0.25x-coverage.pdf)* |
| SRR1749070-0.5x  | 0    | 0.0000  | 0.0000 | 0.6714 | 1.0000  | 522 | *[B. cereus](/data/results/02-mapping/bacilli-controls/cereus-control/SRR1749070-0.5x/cereus/coverage/SRR1749070-0.5x-coverage.pdf)* |
| SRR1749070-1x    | 0    | 0.0000  | 0.0000 | 1.0226 | 1.0000  | 522 | *[B. cereus](/data/results/02-mapping/bacilli-controls/cereus-control/SRR1749070-1x/cereus/coverage/SRR1749070-1x-coverage.pdf)* |
| SRR1749070-5x    | 0    | 0.0000  | 3.0000 | 3.8064 | 6.0000  | 522 | *[B. cereus](/data/results/02-mapping/bacilli-controls/cereus-control/SRR1749070-5x/cereus/coverage/SRR1749070-5x-coverage.pdf)* |


****

## 3. Species identification with Kraken  

We used *Kraken (v. 0.10.4-beta)* and its pre-built Bacteria database to identify *B. anthracis* reads within the B. anthracis* positive NYC sampels and our controls (described above). We also used *B. anthracis*, *B cereus* and *B. thurigiensis* sequencing projects as controls. We used python script [parse_kraken.py](/data/methods/03-kraken/parse_kraken.py) to extract the propotion of reads covered by *B.anthracis*, *B. cereus* group and other bacteria species respectively in the different samples.  

*B. anthracis* reads were detected by Kraken within each of the NYC samples. The results from Kraken [Control Results](/data/results/03-kraken/anthracis-control) suggests that using Kracken we could detect the presence of minute amounts of sequence reads from the organism.

The results from our *B. anthracis*, *B cereus* and *B. thurigiensis* sequencing project controls can be found at the following link: [Anthrax WGS search](https://www.dropbox.com/sh/fwfi75ft4ny1qkk/AADF16diPK-cgV-CmRHzLjWTa?dl=0).  
 
###### *B.cereus* FASTQ species distribution*
 ![B. cereus](/data/results/03-kraken/anthracis-control/cereus.png "B.cereus")

###### *B.anthracis* FASTQ  reads, species distribution*
 ![B. anthracis](/data/results/03-kraken/anthracis-control/anthracis.png "B. anthracis")
 
######  SRR1749070-0.01x *B. anthracis* control
 ![0x coverage](/data/results/03-kraken/anthracis-control/0x_.png "anthracis 0x coverage")

######  SRR1749070-0.01x *B. anthracis* control
 ![0.01x coverage](/data/results/03-kraken/anthracis-control/0.01x_.png "anthracis 0.01x coverage")
 
######  SRR1749070-0.05x *B. anthracis* control
 ![0.05x coverage](/data/results/03-kraken/anthracis-control/0.05x_.png "anthracis 0.05x coverage")
 
######  SRR1749070-0.10x *B. anthracis* control
 ![0.10x coverage](/data/results/03-kraken/anthracis-control/0.10x_.png "anthracis 0.10x coverage")
 
######  SRR1749070-0.25x *B. anthracis* control
 ![0.25x coverage](/data/results/03-kraken/anthracis-control/0.25x_.png "anthracis 0.25x coverage")
 
###### SRR1749070-5.0x *B. cereus* control
 ![5.0x coverage](/data/results/03-kraken/anthracis-control/B.cereus5x.png "cereus 5.0x coverage") 

###### SRR1748707 species distribution*
 ![SRR1749083](/data/results/03-kraken/anthracis-control/P00134_1.png )
 
###### SRR1748708 species distribution* 
 ![SRR1748707](/data/results/03-kraken/anthracis-control/P00134_2.png )
 
###### SRR1749083 species distribution*  
 ![SRR1748708](/data/results/03-kraken/anthracis-control/P00497.png )
 
###### Kraken runs summary
|Run name | Description | *B. anthracis* reads | other *Bacillus* reads | other species reads|
|---------|-------------|----------------------|------------------------|--------------------|
| 0x_     |0X *B anthracis* control| 1          | 3348                 | 11463073           |
| 0.01x_  |0.01X *B anthracis* control| 62      | 3860                 | 11464150           |
| 0.05x_  |0.05X *B anthracis* control| 318     | 5891                 | 11468444           |
| 0.10x_  |0.1X *B anthracis* control| 652     | 8469                 | 11473841           |
| 0.5x_   |0.5X *B anthracis* control | 3446    | 29091                | 11517005           |
| 0.25x_  |0.25X *B anthracis* control | 1732   | 16219                | 11490012           |
| 1x_     |1x_ *B anthracis* control | 6969     | 54694                | 11571054           |
| 5x_     |5x_ *B anthracis* control | 35233    | 259841               | 12002947           |
| B.cereus0.25x_|0.25X *B cereus* control | 6   | 28495                | 11489686           |
| B.cereus0.5x_|0.5X *B cereus* control| 12     | 54058                | 11516632           |
| B.cereus1x_   |1X *B cereus* control | 23    | 105023               | 11570399           |
| B.cereus5x_   |5X *B cereus* control | 126   | 511557               | 11998576           |
| SRR1748707  |NYC subway      | 110   | 29013                | 365541             |
| SRR1748708  |NYC subway     | 1528  | 390672               | 3333666            |
| SRR1749083     |NYC subway    | 251   | 597131               | 5033455            |
| cereus     |*B. cereus* FASTQ file        | 4405  | 8260273              | 98861              |
| anthracis  |*B. antracis* FASTQ file     | 917036| 597131               | 5033455            |

****
 
## 4. Custom SNP assay for the *B. anthracis* core genome  

As a first pass, we made a list of SNPs specific to only the *B. anthracis* core genome. These SNPs were not not found in other *B. cereus*. We then extracted SNPs and flanking regions as 31-mers, with the SNP based occupying 16th position.  

#### Identifying *B. anthracis* specific SNPs from the whole genome alignment*

ProgressiveMAUVE was used to perform whole genome alignment of 10 *B. cereus* group genomes that were selected based on previously published whole genome phylogeny in order to capture the maximum diversity. ProgressiveMAUVE was performed using script [progressiveMAUVE.sh](/data/methods/04-custom-snp-assay/progressiveMAUVE.sh). The *B. cereus* strain ATCC 10987 was used as the reference genome for SNP calling (see below). The 10 genomes and the progressiveMAUVE output can be accessed [here](/data/methods/04-custom-snp-assay/mauve-input).
    
#### Genome sequences of *B. cereus* group species used for ProgressiveMAUVE. 
| Strain name   | Species                | File name    | RefSeq/SRA  | [Clade](http://genome.cshlp.org/content/22/8/1512) |
|---------------|------------------------|--------------|-------------|-------|
| ATCC 10987     | Bacillus cereus        | BCE.fasta    | NC_003909   | 1     |
| m1293         | Bacillus cereus        | bce1_.fasta  | SRX096996   | 1     |
| Ames ancestor | Bacillus anthracis     | GBAA_.fasta  | NC_007530   | 1     |
| Rock3-44      | Bacillus cereus        | bce22_.fasta | SRX098720   | 3     |
| AH603         | Bacillus cereus        | bce26_.fasta | SRX098634   | 3     |
| ATCC 10876    | Bacillus cereus        | bce2_.fasta  | SRX096081   | 2     |
| MM3           | Bacillus cereus        | bce6_.fasta  | SRX098606   | 1     |
| ATCC 1479     | Bacillus cereus        | BC.fasta     | NC_004721-2 | 2     |
| E33L          | Bacillus cereus        | BCZK.fasta   | NC_006274   | 1     |
| BGSC 4BD1     | Bacillus thuringiensis | bth11_.fasta | SRX098635   | 2     |

The MAUVE alignment was loaded into MAUVE Version 2.4.0 inorder to visualize the alignment and to export the SNPs using the "export SNP" option. The nucleotide positions of the reference genome (BCE.fasta, ATCC 10987) as well as the corresponding SNP position on the *B. anthracis* genome, along with the 10 nucleotide pattern at the position were extracted. In this nucleotide pattern, the first nuleotide will be from the reference genome and the 3rd nucleotide will be from the B. anthracis genome. Anthrax-specific SNPs (i.e SNP nucloetide positions found in only the Anthrax genome) were identified using the script [GenerateSNPpattern.sh](/data/methods/04-custom-snp-assay/GenerateSNPpattern.sh), where a number (corresponding to the position of the nucleotide variant) were assigned. Finally, those nucleotide positions that have only the number 3 assigned (position of the *B. anthracis genome* on the alignment) were extracted along with the corresponding nucleotide positions at the reference genome as well as at the *B. anthracis* genome [Anthrax_specific-SNPPattern.txt](/data/results/04-custom-snp-assay/Anthrax_Specific_SNP_31-mers_9538.txt). In total, 9,538 Anthrax-specific SNPs were identified.

#### Generating all the B. cereus 31-mers to downselect against the 9538 Anthrax-specific SNPs*

Next, using the query:  

>[txid86661\[Organism:exp\] NOT txid1392\[Organism:exp\] AND (biomol_genomic\[PROP\] AND refseq\[filter\])](http://www.ncbi.nlm.nih.gov/nuccore/?term=txid86661%5BOrganism%3Aexp%5D+NOT+txid1392%5BOrganism%3Aexp%5D+AND+(biomol_genomic%5BPROP%5D+AND+refseq%5Bfilter%5D))

we downloaded 6,948 *[B. cereus group](http://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?id=86661)* 
(excluding *[Bacillus anthracis](http://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?mode=Info&id=1392)*) 
sequences in FASTA format from NCBI Refseq to downselect against the 9,538 Anthrax-specific SNPs identified in the first pass. 

First, we extracted all the 31-mers in and around all the [9538 Anthrax-specific SNP positions](/data/results/04-custom-snp-assay/Anthrax_Specific_SNP_31-mers_9538.txt) from the *B. anthracis* Ames ancestor genome so that the 16th nucleotide in the 31-mer is the SNP at that specific position. This was done using the script [extractKmers.sh](/data/methods/04-custom-snp-assay/extractKmers.sh).

We then generated all the 31-mers present in all the 6,948  *[B. cereus group](http://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?id=86661)* 
(excluding *[Bacillus anthracis](http://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?mode=Info&id=1392)*) using *[JELLYFISH](http://www.cbcb.umd.edu/software/jellyfish/)* by the script [generate-31-mers-BCereusGroup.sh](/data/methods/04-custom-snp-assay/generate-31-mers-BCereusGroup.sh). The resultant JELLYFISH database of all the B. cereus 31-mers were queried by the 9,538 Anthrax-specific 31-mers using the script [QueryBcereusGroup.sh](/data/methods/04-custom-snp-assay/QueryBcereusGroup.sh). All the 31-mers with zero-counts against the *B. cereus* database were outputed. A total of 1,793 31-mers that had zero-counts were retained and used in all the further downstream analysis.

#### Querying for *B. anthracis* specific 31-mers in the *B. anthracis* and *B. cereus* control groups, and NYC Subway  B. anthracis positive samples.

Here we used the same control samples previously described for B. anthracis and B. cereus in this analysis. All the 31-mers were generated using the script [Getting_KmerCounts.sh](/data/methods/04-custom-snp-assay/Getting_KmerCounts.sh). The *B. anthracis* specific 1,793 31-mers were queried against the 31-mer database of all the control and real samples using [QueryAnthraxSNPs.sh](/data/methods/04-custom-snp-assay/QueryAnthraxSNPs.sh) and the 31-mers that matched the B. anthracis-specific 1,793 31-mers were extracted along with their counts in each sample.  The table lists the total number of 31-mers found (ie each individual SNP multiplyed by the number of occurences).

#### Summary of the number of matched 31-mers from each of *B. anthracis* control samples with the 1,793 Anthrax-specific 31-mers. 
|        Study       | Number of matched 31-mers with Anthrax-specific 31-mers |
|:------------------:|:--------------------------------:|
|   SRR1749070-0x    |                 0                |
| SRR1749070-0.01x   |                 4                |
| SRR1749070-0.05x   |                42                |
|  SRR1749070-0.1x   |                72                |
| SRR1749070-0.25x   |                202               |
|  SRR1749070-0.5x   |                403               |
|  SRR1749070-1.0x   |                729               |
|  SRR1749070-5.0x   |               2311               |

For those control samples that did not have any *B. anthracis* reads (0x coverage), none of the Anthrax-specific 31-mers were matched, as expected.  From these data, there should be at least 0.01x coverage of *B. anthracis* reads in the sample, which can be considered as the minimum threshold for detection using 31-mers. Even at 5x coverage only 65% of the Anthrax-specific 31-mers were matched.

#### Summary of the number of matched 31-mers from each of B. cereus control samples with the 1793 Anthrax-specific 31-mers.

|        Study       | Number of matched 31-mers with Anthrax-specific 31-mers  |
|:------------------:|:--------------------------------:|
|   SRR1749070-0x    |                 0                |
| SRR1749070-0.01x   |                 0                |
| SRR1749070-0.05x   |                 0                |
|  SRR1749070-0.1x   |                 0                |
| SRR1749070-0.25x   |                 0                |
|  SRR1749070-0.5x   |                 0                |
|  SRR1749070-1.0x   |                 0                |
|  SRR1749070-5.0x   |                 0                |


As expected, none of the 31-mers from the samples in the *B. cereus* controls matched to the 31-mer set. This showed that the 1,793 31-mers were specific for *B. anthracis*.

#### Summary of the number of matched 31-mers from each of the 3 NY Subway sytem Anthrax positve samples with the 1793 Anthrax-specific 31-mers.
|    Study   |Number of matched 31-mers with Anthrax-specific 31-mers |
|:----------:|:--------------------------------:|
| SRR1749083 |                 0                |
| SRR1748708 |                 2                |
| SRR1748707 |                 0                |

Only sample SRR1748708 contained *B. anthracis* -specific 31-mers with a frequency count of 2 for each of the 2 31-mers. This indicated, a potential positive result with *B. anthracis* present at ~ 0.01X coverage. 

#### Anthrax-specific K-mers identified from the NYC subway system SRR1748708 sample

| SNP position on the *B. anthracis* Ames ancestor genome | 31-mer sequence | Number of matches | Annotation |
|:-------------------------------------------------------------------------------:|:---------------------------------------------------:|:-------------------------------------------------------:|:---------------------------------:|
|                                     4083672                                     |           TGTGCCCCATCCTGAGCATACAACTTTATAA           |                            2                            |       nucleotidyltransferase [GBAA_4491](http://www.ncbi.nlm.nih.gov/nucleotide/50082967?report=gbwithparts&from=4082774&to=4085128&RID=HYA30CNN013)      |
|                                     4136672                                     |           ACATAGAACAAGTGACATTCTATCAAACGGT           |                            2                            |          intergenic region  between spore protease  [GBAA_4546](http://www.ncbi.nlm.nih.gov/nucleotide/50082967?report=gbwithparts&from=4135441&to=4136547&RID=HYBY805Z01R) and S20 ribosomas protein [GBAA_4547](http://www.ncbi.nlm.nih.gov/nucleotide/50082967?report=gbwithparts&from=4136720&to=4136986&RID=HYBY805Z01R)      |
****

## Appendix: Project Data Structure

    Public
        data
            - Supplementary information from study and information about the study on SRA
        references
            - Reference genomes and plasmids used for mapping
        results
            - Mapping results of the B. anthracis and Yersinia samples against references
        scripts
            - All custom scripts used in these analyses
    
    In House
        bin
            - Symbolic links to programs built in src folder
        logs
            - Logged output from scripts
        sra-fastq
            - Each of the 1572 samples in FASTQ and FASTA format
        sra-pathogens
            - Symbolic links to FASTQ of samples containing B. anthracis and Yersinia
        sra-runs
            - Each of the 1572 samples in SRA format
        src
            - Programs downloaded and built for this project
