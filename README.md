# Fungal Genomics 



Idea: Fungi Genome Sequencing at the Era of Long Reads: A Giant Step into Horizontal Gene Transfer and Genome compartimentalization


Co-authors: Scott Hotaling | Julien Alban Nguinkal 

Core Idea: Assembly quality | Itentification of lineage species-specific contigs/chromosome | Their functionnal attributes | Detection of horizontal gene transfer BY MACHINE LEARNING APPROACH FOR EXAMPLE |



Useful resources: 

1. [Representation and participation across 20 years of plant genome sequencing](https://doi.org/10.1038/s41477-021-01031-8)
2. [Toward a genome sequence for every animal: Where are we now?](https://doi.org/10.1073/pnas.2109019118)
3. [Long Reads Are Revolutionizing 20 Years of Insect Genome Sequencing](https://doi.org/10.1093/gbe/evab138)
4. [Comparative genomic analysis of 31 Phytophthora genomes reveal genome plasticity and horizontal gene transfer](https://doi.org/10.1094/mpmi-06-22-0133-r)















[Lifestyle Transitions in Fusarioid Fungi are Frequent and Lack Clear Genomic Signatures](https://academic.oup.com/mbe/article/39/4/msac085/6575681)

![img](https://oup.silverchair-cdn.com/oup/backfile/Content_public/Journal/mbe/39/4/10.1093_molbev_msac085/1/m_msac085f2.jpeg?Expires=1654420537&Signature=GaZVZUb9eYqusadLxLSHkY4G4XMdI-JBfbzsk5hI6QIQL2Q~jFWRnFB9y7quhZ5IQHy5IECLLMwkaQvxR~UnFZCVAWhWzZMo1dbjRze-FVeUL65C0E94HukoqHLsPS48kCghO6yoo7SXqKKv20YPwZohul5TD0lC6A42jQZBcbbEUuSitHgOd17MPWpKfvy-9QZ6dtkYtZEcst~VJ7MZ~oj5bOyooXfktL270m3e-X87ZLM2PeACVHm1VbJ~O~c2TAJcnE-0VHxNhA9rxo~2HhVV4Iq79uyJaDHK71ynTSx7IQoFj3nh7c31Z48MkXrxWzTQ08W28yGdZnnVDDo0Gw__&Key-Pair-Id=APKAIE5G5CRDK6RD3PGA)



[A chromosome-scale genome assembly of the tomato pathogen Cladosporium fulvum reveals a compartmentalized genome architecture and the presence of a dispensable chromosome](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000819)

![img](https://www.microbiologyresearch.org/docserver/fulltext/mgen/8/4/mgen000819-f1.gif)





Le script utilise pour le papier de Jon Hwa Jin




## Go to the working directory

```bash

cd /NABIC/HOME/yedomon1/fusarium_phylogenetics

```

## Step 1 Just keep a small name


```bash

vi rename.sh

```

```bash

#/bin/bash

set -e

for seq in *.fasta

do

base=$(basename $seq .fasta)

cat ${base}.fasta | awk -F' ' '{print $1}' > ${base}_renamed.fasta


done

## Bye!


```


Run

```bash

$ bash rename.sh

```



## Step 2: Multiple sequence alignment


## We need to merge the sequence first.

```bash

cat *renamed.fasta > ITS.fasta

```


## Write the script


```bash

vi run_phylo.sh

```

The content



```bash


#/bin/bash

set -e

### Multiple sequence alignment

source activate mafft_env

mafft --maxiterate 1000 --localpair --thread 60 ITS > ITS.mafft

source deactivate mafft_env


### Alignment trimming

source activate trimal_env

trimal -automated1 -in ITS.mafft -out ITS.mafft.trimal

source deactivate trimal_env

### Tree construction with automatic model selection

source activate iqtree_env

iqtree -s ITS.mafft.trimal -nt AUTO -alrt 1000 -bb 1000

source deactivate iqtree_env


## Bye!

```



## Run

```bash

bash run_phylo.sh &> log.phylo &

```



## See the tree with Fig tree sofware

```bash

cd /NABIC/HOME/yedomon1/genomeassemblyfungiMR004/13_Orthologs_identification_with_Blast/genome_assemblies_from_NCBI/genomes_assemblies/01/gbfiles/good/goodfasta/FigTree_v1.4.4/lib

```



## Run Figtree



```bash

java -jar figtree.jar

```




- #### Love the paper.. way they grab fungal related genes as well as plant-fungal interaction genes


[The Whole Genome Sequence of Fusarium redolens strain YP04, a Pathogen that Causes Root Rot of American Ginseng](https://apsjournals.apsnet.org/doi/pdf/10.1094/PHYTO-03-21-0084-A)


- #### [A genome-scale phylogeny of the kingdom Fungi](https://www.cell.com/current-biology/fulltext/S0960-9822(21)00139-1#secsectitle0105)


![img](https://els-jbs-prod-cdn.jbs.elsevierhealth.com/cms/attachment/b6f9af85-a4d2-49a8-b687-6ce278add5d4/gr1.jpg)


[code availability](https://figshare.com/articles/dataset/Scripts_and_analyses_used_for_the_fungal_phylogeny/12751736)


side codes [1](https://github.com/JLSteenwyk/Phylogenetic_scripts/blob/master/LB_score.py) , [2](https://github.com/evolbioinfo/gotree), [3](https://github.com/smirarab/1kp/tree/master/scripts/hypo-test)



- #### [Genome Resource of Podosphaera xanthii, the Host-Specific Fungal Pathogen That Causes Cucurbit Powdery Mildew](https://apsjournals.apsnet.org/doi/full/10.1094/MPMI-11-20-0307-A)


- #### [Development of a PCR-based assay for rapid and reliable identification of pathogenic Fusaria](https://academic.oup.com/femsle/article/218/2/329/531537)



- #### [Genome sequence of Monilinia vaccinii-corymbosi sheds light on mummy berry disease infection of blueberry and mating type](https://academic.oup.com/g3journal/article-abstract/11/2/jkaa052/6062400)

- #### [Genome sequence resource of Phomopsis longicolla strain YC2-1, a fungal pathogen causing Phomopsis stem blight in soybean](https://apsjournals.apsnet.org/doi/10.1094/MPMI-12-20-0340-A)

- #### [Proximity Ligation Technology](http://phasegenomics.com/technology/proximity-ligation/)

- #### [Unravel the mysteries of the fungal world](https://phasegenomics.com/applications/metagenomics-microbiology/fungal-genomics/?utm_campaign=Fungus%20February%202021&utm_medium=email&_hsmi=113150619&_hsenc=p2ANqtz-_SZRFVKn-8UsWiMOFIiRSt3ucnPZZvW39SxFCqLZ2QdDeF65Vu7CSQMk1PlV3vy4oHX3oJdSFbXFqvzwjI0obu2rJVdQ&utm_content=113150619&utm_source=hs_email)


- #### [Morphological and molecular characterization of Fusarium tricinctum causing postharvest fruit rot of pumpkin in Korea](https://link.springer.com/article/10.1007/s10327-018-0803-6) |  For Mrs Chin Paper


- #### [Repetitive Elements Contribute to the Diversity and Evolution of Centromeres in the Fungal Genus Verticillium](https://mbio.asm.org/content/11/5/e01714-20)





- #### 19 chromosomes here [A Chromosome-Scale Genome Assembly for the Fusarium oxysporum Strain Fo5176 To Establish a Model Arabidopsis-Fungal Pathosystem](https://www.g3journal.org/content/10/10/3549.long)


- #### [Great inspiration discovered today 16 december 2020 on research square |  Genome sequencing and comparative genomic analysis of highly and weakly aggressive strains of Sclerotium rolfsii, the causal agent of peanut stem rot](https://assets.researchsquare.com/files/rs-38224/v2/9acd3546-03af-4b93-8e48-085d43b35327.pdf)

- #### [FocSge1 in Fusarium oxysporum f. sp. cubense race 1 is essential for full virulence](https://bmcmicrobiol.biomedcentral.com/articles/10.1186/s12866-020-01936-y)

- #### [ONT assembly with Canu with mitogenome resolution](https://academic.oup.com/gigascience/article/9/9/giaa099/5908739)
- #### [Inspi](https://link.springer.com/article/10.1186/gb-2010-11-7-r73)

- #### [Inspiration paper 1 for Graph color respect with R  ](https://bmcgenomics.biomedcentral.com/articles/10.1186/s12864-020-06871-w)
- #### [Inspirational paper 2](https://imafungus.biomedcentral.com/articles/10.1186/s43008-019-0011-9)
- #### [Inspirationnal paper 3](https://www.nature.com/articles/s41598-018-30335-7)
- #### [Code and script Fungal annotation assemblies and so on](https://gitlab.gwdg.de/alice.feurtey/genome_architecture_zymoseptoria)
- #### [Mechanism of pathogenicity](https://books.google.fr/books?hl=fr&lr=&id=wGgCEAAAQBAJ&oi=fnd&pg=PA185&dq=NBS-LRR+gene+cloning+plant+disease+resistance&ots=pwwZ21T0-W&sig=yZRXOuy_gzvH6aC-TSjfgZoU0Sg#v=onepage&q=NBS-LRR%20gene%20cloning%20plant%20disease%20resistance&f=false)

- #### [Grouped barchart customization](https://www.r-graph-gallery.com/48-grouped-barplot-with-ggplot2.html)
- #### [Change label order](https://www.datanovia.com/en/fr/blog/ggplot-comment-changer-lordre-des-legendes/)
