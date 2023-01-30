
## **Illumina sequencing**

bridge PCR (bPCR) amplification: 
Bridge amplification takes place in a flow cell, aiming to generating clusters of DNA strands for further sequencing and analysis. The flow cell is coated with two types of oligos, complementary to the two adapters on the fragment strand, respectively. Once the fragment strand is added to the flow cell, it hybridizes to one of the oligos on the cell surface. A polymerase then moves along the strand, creating its complementary DNA strand, i.e. the reverse strand. The double-stranded DNA is denatured and the original strand (forward strand) is washed away. The remaining reverse strand then folds over and its adapter region hybridizes to the second type of oligo on the flow cell. Polymerase attaches to the reverse strand and generates the complementary strand that is identical to the forward strand, forming a double-stranded bridge. This bridge is then denatured, resulting in two single-stranded copies of the DNA, forward and reverse strand, anchored to the flow cell. By repeating this denaturation and extension process, millions of fragments are amplified, forming localized clusters on the flow cell.

original paper:  https://www.nature.com/articles/nature07517

-   http://dors.weizmann.ac.il/course/course2019-20/Noa_IlluminaPrimaryAnalysisPipeline.pdf
-   https://biomedicalhub.github.io/genomics/01-part1-introduction.html
-   https://apollo-institute.org/bridge-amplification-sequencing/
-   https://hbctraining.github.io/Training-modules/planning_successful_rnaseq/slides/sequencing_technologies_mm.pdf
-   https://www.youtube.com/watch?v=fCd6B5HRaZ8
-   https://www.youtube.com/watch?v=womKfikWlxM



isothermal amplification: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3761594/

Currently available sequencing technologies utilize surface amplification to form clusters of amplified nucleic acid on a solid support. The most common approaches include bridge amplification and isothermal amplification can be performed using kinetic exclusion amplification (KEA), also referred to as exclusion amplification (ExAmp). Both of these amplification methodologies utilize 2 different surface primers, forward and reverse, immobilized on a solid support. However, both bridge and ExAmp cluster amplification processes make inefficient use of the 2 surface primers. Current estimates are that <10% of the surface primers are converted into template strands after amplification. 
source: https://patents.google.com/patent/WO2016193695A1/en
https://patentimages.storage.googleapis.com/65/f9/1a/722617e3d56510/WO2016193695A1.pdf


One obvious part of the exclusion amplification as implemented is the very viscous enzyme mix. Probably the diffusion of the library fragments towards the flowcell is very much slowed down (requiring also higher library concentrations?) giving the molecule that arrives first the chance to become amplified and fill entire nanowells before a second one arrives (http://www.google.com/patents/WO2013188582A1?cl=en). The viscosity enhanced "drag" also could explain the stronger bias towards smaller inset size reads?
The high viscosity buffer together with high library concentrations and "RPA" amplification for the clustering process ("Recombinase Polymerase Amplification")) might be sufficient for the Kinetic Exclusion Amplification on the nanowell flowcells? It seems to me that the other methods described in the patent might not be compatible with the old cBots (these can be used for the Hiseq3000/4000 clustering after a software upgrade)?

**non-Patterned (Random) vs Patterned flow cells**

random: HiSeq 2500, MiSeq, NextSeq 500, MiniSeq, HiSeq X
patterned: HiSeq 3000/4000, NovaSeq, iSeq, NextSeq 1000/2000

patterned: Cheaper/read however, more index hopping, insert sizes less variable, higher duplication rates.

 - http://core-genomics.blogspot.com/2016/01/almost-everything-you-wanted-to-know.html
 - https://www.youtube.com/watch?v=oIJaA6h2bFM
 - https://emea.illumina.com/science/technology/next-generation-sequencing/sequencing-technology/patterned-flow-cells.html

Patterned flow cells contain billions to tens of billions of nanowells at fixed locations across both surfaces of the flow cell. The structured organization provides even spacing of sequencing clusters to deliver significant advantages over non-patterned cluster generation.

-   Clusters can only form in the nanowells, making the flow cells less susceptible to overloading, and more tolerant to a broader range of library densities.Each nanowell contains DNA probes used to capture prepared DNA strands for amplification during cluster generation. The regions between the nanowells are devoid of DNA probes.
-   Precise nanowell positioning eliminates the need to map cluster sites, and saves hours on each sequencing run.
-   Higher cluster density leads to more usable data per flow cell, driving down the cost per gigabase (Gb) of the sequencing run.

In patterned flow cells bridge amplification immediately starts when a single stranded DNA is introduced to the flow cell after it hybridzides to an oligo present in the nanowell. However if there are free floating adapters this may result in index hopping (See below).

**ExAmp Cluster Amplification (HiSeq 3000/4000, NextSeq 2000)**
Exclusion amplification allows simultaneous seeding (landing of the DNA strand in the nanowell) and amplification during cluster generation, which reduces the chances of multiple library fragments amplifying in a single cluster. This method maximizes the number of nanowells occupied by DNA clusters originating from a single DNA template, increasing the amount of usable data from each run.

The new amplification reagent is very different from the cyclical, bridge-PCR of random clustering. The details of this new chemistry are proprietary, and the only insight comes from patent descriptions. 
ExAmp does not include the regular bind-and-wash steps prior to cluster generation as described above. Instead, the single stranded library molecules—resulting from the alkali denaturation of double-stranded library molecules—are mixed with the ExAmp clustering reagents (Illumina) and loaded onto a patterned flow cell. The ExAmp chemistry involves a rapid isothermal amplification step necessary for cluster generation.

https://support.illumina.com/content/dam/illumina-support/courses/examp-cluster-workflow/story_html5.html

**4Channels SBS  (4 dyes) vs 2 channels SBS (2 dyes):**

4 colour: MiSeq, HiSeq 2500. Bases are identified using 4 different fluorescent dyes, one for each base and four images per sequencing cycles.
2 colour: MiniSeq, NextSeq, NovaSeq. A (green + red), G (no colour), T (green), C (Red).


**Illumina library prep**
https://vimeo.com/226448487


**Indexed sequencing**

 - Single-indexed libraries—Adds Index 1 (i7) sequences to generate
   uniquely tagged libraries.    
 - Dual-indexed libraries—Adds Index 1 (i7)    and Index 2 (i5)
   sequences to generate uniquely tagged libraries.
	   
	 - Unique dual (UD) indexes have distinct, unrelated index adapters for
	   both index reads. Index adapter sequences are eight or 10 bases long.

	 - Combinatorial dual (CD) indexes have eight unique dual pairs of index
   adapters, so most libraries share sequences on the i7 or i5 end.
   Index adapter sequences are eight bases long. During indexed
   sequencing, the index is sequenced in a separate read called the
   Index Read, where a new sequencing primer is annealed. When libraries
   are dual-indexed, the sequencing run includes two additional reads,
   called the Index 1 Read and Index 2 Read.

https://support-docs.illumina.com/SHARE/IndexedSeq/indexed-sequencing.pdf
https://thesequencingcenter.com/wp-content/uploads/2021/12/illumina-adapter-sequences.pdf


**Use Indexes with a hamming distance between any two pairs of indexes of greater than or equal to 3**

Source: https://support.illumina.com/bulletins/2021/08/why-is-allowing-mismatches-when-demultiplexing-desirable-.html

By default, bcl2fastq allows 1 mismatch in each barcode. If you allow one sequencing error, then the number of differences between barcodes must be equal to (2*sequencing errors + 1) = 3.   Illumina index sets are typically designed with a Hamming distance (n) or mismatch number (mm) between any two pairs of indexes of greater than or equal to 4. 

using R the hamming distance between indexes can be calculated using this script:

    require(Biostrings)
   
    index<-read.table('/home/p.krijger_cbs-niob.local/projects/index/index.tsv', header = FALSE, sep = '\t')
    barcodes<-DNAStringSet(index$V2)
    names(barcodes)<-index$V1
    
    dist<-stringDist(barcodes, method = "hamming", ignoreCase = FALSE, diag = TRUE, upper = TRUE)
    mat<-as.matrix(dist)
    write.table(mat, '/home/p.krijger_cbs-niob.local/projects/index/index_Hamming_distance.tsv')    
    
    dist<-stringDist(barcodes, method = "levenshtein", ignoreCase = FALSE, diag = TRUE, upper = TRUE)
    mat<-as.matrix(dist)
    write.table(mat, '/home/p.krijger_cbs-niob.local/projects/index/index_levenshtein_distance.tsv')    

In our lab we are using the TruSeq-LT and NEBNext indexes. The Hamming distance of all indexes was calculated using the above mentioned R script and can be downloaded from this repository (https://github.com/krijgerp/Usefull-stuff/blob/main/index_distance.xlsx, https://github.com/krijgerp/Usefull-stuff/blob/main/index_Hamming_distance.tsv). For example, NEBNext index 40 should not be used in combination with NEBNext/TruSeq-LT index 7, NEBNext index 26, TruSeq-LT index 19 and 20.  NEBNext index 41 should not be used in combination with NEBNext/TruSeq-LT index 11 and NEBNext index 31.


**Index Hopping**
[Index hopping](https://www.illumina.com/techniques/sequencing/ngs-library-prep/multiplexing/index-hopping.html) occurs when  an index initially assigned to a specific sample are incorrectly assigned to other sample(s) in a pool of samples.

The primary culprit that causes index hopping seems to be the presence of free adapters in samples during the library prep process, especially during the pooling or multiplexing steps. Libraries with higher levels of free adapters will see higher levels of index hopping. Apparently, free floating, unligated adapter sequences can hybridize with the wrong i5 or i7 index sequence, thus causing the wrong index to “hop” over to a different sample read. The elimination of free adapters is of paramount importance during library prep.

***Index hopping with ExAmp***:
Index hopping can be seen at (slightly?) elevated levels on instruments using patterned flow cells with exclusion amplification chemistry versus those that do not use patterned flow cells. 
Most likely it is free adapter that is acting as a primer for the recombinase/ploymerase to amplify from. As adapters are likely to come from all libraries in the pool they will randomly extend library molecules creating the swapped indexes.
Most likely this index-switching happens during seeding and before cluster generation, because all the active reagents (in particular DNA polymerase) necessary for cluster generation are present in the reaction mix while the library molecules are being guided to the nanowells to seed a cluster. If free index primers are present during this procedure they can prime the library fragments and get extended by the active DNA polymerase, forming a new library molecule with a different index. These new library molecules with switched identities can seed free nanowells and generate clusters, thus resulting in reads that get falsely assigned to a different sample

![](https://sequencing.qcfail.com/wp-content/uploads/sites/2/2017/05/barcode_swap_mechanism.png)

source:

 - https://www.biorxiv.org/content/10.1101/125724v1
 - http://enseqlopedia.com/2016/12/index-mis-assignment-between-samples-on-hiseq-4000-and-x-ten/
 - http://enseqlopedia.com/2017/04/index-swapping-illumina-examp-clustering/
 - https://www.10xgenomics.com/blog/sequence-with-confidence-understand-index-hopping-and-how-to-resolve-it
 - https://thesequencingcenter.com/knowledge-base/what-is-index-hopping/
 - https://emea.illumina.com/techniques/sequencing/ngs-library-prep/multiplexing/index-hopping.html
 - https://www.youtube.com/watch?v=DR_8KbGGIhA
 - https://sequencing.qcfail.com/articles/the-latest-illumina-sequencers-muddle-samples/

*





**Mixing short & long inserts in the same flow cell.**

Short fragments preferentially bind to the flow cell compared to larger fragments. This negatively affects run performance as shorter fragments are overrepresented on the flow cell and in the final sequencing data. You also have to keep in mind that the flowcells and clustering methods are not the same in the NovaSeq as in the MiSeq / NextSeq. A patterned flowcell is much worse for sequencing long libraries, since clusters bridge into neighbouring wells.
Also, the ExAmp chemistry has a higher bias against long fragments as the traditional bridge amplification. Shorter library molecules have always clustered more efficiently but this effect is amplified on patterned flow cells due to the rate of diffusion in the ExAMp chemistry.

Source: https://emea.support.illumina.com/bulletins/2020/12/how-short-inserts-affect-sequencing-performance.html






