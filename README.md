# kallisto-transcriptome-indices

kallisto indices indices constructed from [Ensembl reference transcriptomes](https://useast.ensembl.org/index.html) version 108. Downloads available from the [releases](https://github.com/pachterlab/kallisto-transcriptome-indices/releases) page. These indices apply to kallisto version >=0.50.1 (which is part of kb-python >=0.28.0).

## List of species

Indices for five species are available: **human** (*Homo sapiens*), **mouse** (*Mus musculus*), **dog** (*Canis lupus familiaris*), **monkey** (*Macaca mulatta*), and **zebrafish** (*Danio_rerio*).

The genome FASTA files and GTF files used to generate the indices are listed below.

1. **human**
   Genome: https://ftp.ensembl.org/pub/release-108/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
   GTF: https://ftp.ensembl.org/pub/release-108/gtf/homo_sapiens/Homo_sapiens.GRCh38.108.gtf.gz
3. **mouse**
   Genome: https://ftp.ensembl.org/pub/release-108/fasta/mus_musculus/dna/Mus_musculus.GRCm39.dna.primary_assembly.fa.gz
   GTF: https://ftp.ensembl.org/pub/release-108/gtf/mus_musculus/Mus_musculus.GRCm39.108.gtf.gz
4. **dog**
   Genome: https://ftp.ensembl.org/pub/release-108/fasta/canis_lupus_familiaris/dna/Canis_lupus_familiaris.ROS_Cfam_1.0.dna.toplevel.fa.gz
   GTF: https://ftp.ensembl.org/pub/release-108/gtf/canis_lupus_familiaris/Canis_lupus_familiaris.ROS_Cfam_1.0.108.gtf.gz
5. **monkey**
   Genome: http://ftp.ensembl.org/pub/release-108/fasta/macaca_mulatta/dna/Macaca_mulatta.Mmul_10.dna.toplevel.fa.gz
   GTF: https://ftp.ensembl.org/pub/release-108/gtf/macaca_mulatta/Macaca_mulatta.Mmul_10.108.gtf.gz
6. **zebrafish**
   Genome: http://ftp.ensembl.org/pub/release-108/fasta/danio_rerio/dna/Danio_rerio.GRCz11.dna.primary_assembly.fa.gz
   GTF: http://ftp.ensembl.org/pub/release-108/gtf/danio_rerio/Danio_rerio.GRCz11.108.gtf.gz

## Types of indices

Two indices are supported:

1. The **standard** index (which does not contain introns and is therefore only suitable for quantifying bulk and single-cell RNA-seq)
2.  The **nac** index (which contains both nascent transcripts and cDNAs and therefore can be used for applications where quantifying intron-spanning reads is important, such as single-nucleus RNA-seq or biophysical models that jointly consider spliced and unspliced transcripts).

Note: The term *cDNA* used throughout follows that of Ensembl. That is, the cDNA represents the sequences of the mature transcripts wherein introns are not included as they have been spliced out.

## Contents of indices

Both the *standard* and *nac* index are packaged with the following two files:

* **index.idx**: The kallisto index that reads will be pseudoaligned against
* **t2g.txt**: A file containing the transcript-to-gene mapping

The *nac* index will be packaged with two additional files:

* **cdna.txt**: The IDs of the cDNA transcripts
* **nascent.txt**: The IDs of the nascent transcripts

## Downloading the indices

While you could download the indices, you could use the **kb ref** command within kb-python to download the index. For example, to download the zebrafish indices, you would do:

<pre># Standard index:
kb ref -d zebrafish -i index.idx -g t2g.txt
# nac index:
kb ref --workflow=nac -d zebrafish -i index.idx -g t2g.txt -c1 cdna.txt -c2 nascent.txt
</pre>

## How indices were generated

All indices were generated using kb-python 0.28.0 (with the kallisto 0.50.1 binary) with the respective species's genome FASTA (genome.fa.gz) and genome GTF annotation (genome.gtf.gz) as follows:

### standard index

<pre>kb ref --workflow=standard -i index.idx -g t2g.txt -f1 cdna.fa \
  --include-attribute gene_biotype:protein_coding \
  --include-attribute gene_biotype:lncRNA \
  --include-attribute gene_biotype:lincRNA \
  --include-attribute gene_biotype:antisense \
  --include-attribute gene_biotype:IG_LV_gene \
  --include-attribute gene_biotype:IG_V_gene \
  --include-attribute gene_biotype:IG_V_pseudogene \
  --include-attribute gene_biotype:IG_D_gene \
  --include-attribute gene_biotype:IG_J_gene \
  --include-attribute gene_biotype:IG_J_pseudogene \
  --include-attribute gene_biotype:IG_C_gene \
  --include-attribute gene_biotype:IG_C_pseudogene \
  --include-attribute gene_biotype:TR_V_gene \
  --include-attribute gene_biotype:TR_V_pseudogene \
  --include-attribute gene_biotype:TR_D_gene \
  --include-attribute gene_biotype:TR_J_gene \
  --include-attribute gene_biotype:TR_J_pseudogene \
  --include-attribute gene_biotype:TR_C_gene \
  genome.fa.gz genome.gtf.gz
</pre>

### nac index

<pre>kb ref --workflow=nac -i index.idx -g t2g.txt \
  -f1 cdna.fa -f2 nascent.fa -c1 cdna.txt -c2 nascent.txt \
  --include-attribute gene_biotype:protein_coding \
  --include-attribute gene_biotype:lncRNA \
  --include-attribute gene_biotype:lincRNA \
  --include-attribute gene_biotype:antisense \
  --include-attribute gene_biotype:IG_LV_gene \
  --include-attribute gene_biotype:IG_V_gene \
  --include-attribute gene_biotype:IG_V_pseudogene \
  --include-attribute gene_biotype:IG_D_gene \
  --include-attribute gene_biotype:IG_J_gene \
  --include-attribute gene_biotype:IG_J_pseudogene \
  --include-attribute gene_biotype:IG_C_gene \
  --include-attribute gene_biotype:IG_C_pseudogene \
  --include-attribute gene_biotype:TR_V_gene \
  --include-attribute gene_biotype:TR_V_pseudogene \
  --include-attribute gene_biotype:TR_D_gene \
  --include-attribute gene_biotype:TR_J_gene \
  --include-attribute gene_biotype:TR_J_pseudogene \
  --include-attribute gene_biotype:TR_C_gene \
  genome.fa.gz genome.gtf.gz
</pre>

## Questions and Issues

Please consult the issues section of the [kallisto repo](https://github.com/pachterlab/kallisto/issues) or the [kb-python](https://github.com/pachterlab/kb_python/issues) repo

