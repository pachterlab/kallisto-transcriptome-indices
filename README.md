# kallisto-transcriptome-indices
kallisto indices indices constructed from [Ensembl reference transcriptomes](https://uswest.ensembl.org/info/data/ftp/index.html). Downloads available from the [releases](https://github.com/pachterlab/kallisto-transcriptome-indices/releases) page.


## Building indices with kallisto

To build the indices, download the full transcriptomes from Ensembl (files ending in `cdna.all.fa.gz`) and build the indices with kallisto.

For example, to build the human transcriptome index, first download the transcriptome, which is available under `cDNA` on the Ensembl website, at ftp://ftp.ensembl.org/pub/release-94/fasta/homo_sapiens/cdna/:

```
curl -O ftp://ftp.ensembl.org/pub/release-94/fasta/homo_sapiens/cdna/Homo_sapiens.GRCh38.cdna.all.fa.gz
```

Then run `kallisto index`. kallisto will work on `.fa` and `.fz.gz` files so there is no need to unzip the downloaded file:

```
kallisto index -i 	Homo_sapiens.GRCh38.cdna.all.release-94_k31.idx	Homo_sapiens.GRCh38.cdna.all.fa.gz
```

Indices avaialble here were built with the default `--kmer-size=31`. 
A different k-mer size can be chosen using the `-k` or `--kmer-size` option (odd k only). A full description of the command can be obtained by typing `kallisto index`:

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
