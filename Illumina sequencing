## **Illumina sequencing**

**Mixing short & long inserts in the same flow cell.**

Short fragments preferentially bind to the flow cell compared to larger fragments. This negatively affects run performance as shorter fragments are overrepresented on the flow cell and in the final sequencing data. You also have to keep in mind that the flowcells and clustering methods are not the same in the NovaSeq as in the MiSeq / NextSeq. A patterned flowcell is much worse for sequencing long libraries, since clusters bridge into neighbouring wells.
Also, the ExAmp chemistry has a higher bias against long fragments as the traditional bridge amplification.

Source: https://emea.support.illumina.com/bulletins/2020/12/how-short-inserts-affect-sequencing-performance.html


**Allowing mismatches when demultiplexing bcl files**

Source: https://support.illumina.com/bulletins/2021/08/why-is-allowing-mismatches-when-demultiplexing-desirable-.html

By default, bcl2fastq allows 1 mismatch in each barcode. If you allow one sequencing error, then the number of differences between barcodes must be equal to (2*sequencing errors + 1) = 3.   Illumina index sets are typically designed with a Hamming distance (n) or mismatch number (mm) between any two pairs of indexes of greater than or equal to 4. 

using R the hamming distance between indexes can be calculated using this script:

    require(Biostrings)
    require(ShortRead)
    
    index<-read.table('/home/p.krijger_cbs-niob.local/projects/index/index.tsv', header = FALSE, sep = '\t')
    barcodes<-DNAStringSet(index$V2)
    names(barcodes)<-index$V1
    
    dist<-stringDist(barcodes, method = "hamming", ignoreCase = FALSE, diag = TRUE, upper = TRUE)
    mat<-as.matrix(dist)
    write.table(mat, '/home/p.krijger_cbs-niob.local/projects/index/index_Hamming_distance.tsv')    
    
    dist<-stringDist(barcodes, method = "levenshtein", ignoreCase = FALSE, diag = TRUE, upper = TRUE)
    mat<-as.matrix(dist)
    write.table(mat, '/home/p.krijger_cbs-niob.local/projects/index/index_levenshtein_distance.tsv')    


**Index Hopping**

