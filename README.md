# kallisto-transcriptome-indices
kallisto indices indices constructed from [Ensembl reference transcriptomes](https://uswest.ensembl.org/info/data/ftp/index.html). Downloads available from the [releases](https://github.com/pachterlab/kallisto-transcriptome-indices/releases) page.


## Building indices on kallisto

To build the indices, just download the full transcriptome form ensembl (ends in `cdna.all.fa.gz`) and build the index with kallisto.

For example, to build the human transcriptome index first we download the transcriptome, which is available under `cDNA` in the ensembl website, at ftp://ftp.ensembl.org/pub/release-94/fasta/homo_sapiens/cdna/:

```
curl -O ftp://ftp.ensembl.org/pub/release-94/fasta/homo_sapiens/cdna/Homo_sapiens.GRCh38.cdna.all.fa.gz
```

Then we call `kallisto index`, kallisto will work on `.fa` and `.fz.gz` files so no need to unzip it:

```
kallisto index -i 	Homo_sapiens.GRCh38.cdna.all.release-94_k31.idx	Homo_sapiens.GRCh38.cdna.all.fa.gz
```

Indiceds avaialble here were built with the default `--kmer-size=31`. 
You can also pass a different kmer than the default of 31 if desired.
```
kallisto 0.45.0
Builds a kallisto index

Usage: kallisto index [arguments] FASTA-files

Required argument:
-i, --index=STRING          Filename for the kallisto index to be constructed 

Optional argument:
-k, --kmer-size=INT         k-mer (odd) length (default: 31, max value: 31)
    --make-unique           Replace repeated target names with unique names
```
