### Validation of phylogenetic tree

1. I downloaded two genes of Phaseolus from ENSEMBL Plants: **SUB1 e synthetase**

SUB1 will be identical for species (A,B)
syinthetase will be identical for state (wt,dom)

http://plants.ensembl.org/Phaseolus_vulgaris/Gene/Sequence?db=core;g=PHAVU_010G148300g;r=10:41896617-41903193;t=ESW07662
http://plants.ensembl.org/Phaseolus_vulgaris/Gene/Sequence?db=core;g=PHAVU_002G236500g;r=2:40207854-40209575;t=ESW31409

The len of these two genes is 2922.

2. I should generate four pieces for each gene, with 50% identity for each pair.

- So for generate random mutations, I used this:  https://github.com/mkpython3/Mutation-Simulator

Gene SUB1  = [(AD, AW), (BD,BW)]  50 % of identity between these

Gene Synthetase = [(AW, BW), (AD,BD)]50 % of identity between these


I obtained four new pieces, for SUB1 and Synthetase:

```shell
./mutation-simulator.py Phaseolus_vulgaris_SUB1_sequence.fa args -sn 0.50   #for AD-AW  and BD-BW  
./mutation-simulator.py Phaseolus_vulgaris_synthetase_sequence.fa args -sn 0.50
```

Per check if the similarity is of 50 % for the pieces I used this:

```shell
./clustalo-1.2.4-Ubuntu-32-bit -i syntetasewt+syntetasedom+sub1wt+sub1dom_50.fa --full --percent-id --distmat-out=50identity.distmat
```

I obtained a divergent matrix.

- I built trees for two genes:

```shell
./clustalo-1.2.4-Ubuntu-32-bit -i /home/flavia/Lab/phaesolus/identity50/buttami/synthe4pieces50.fa -o clustalsynt_50.aln --guidetree-out treeseqsynt_50 --outfmt=clustal

 ./clustalo-1.2.4-Ubuntu-32-bit -i /home/flavia/Lab/phaesolus/identity50/buttami/SUB_4pieces_150.fa -o clustalSUB1_50.aln --guidetree-out treeseqSUB1_50 --outfmt=clustal                                   
```

### Build 4 artificial sequences that shered pieces of Gene SUB1 and pieces of Gene synthetase

I generate 91 % of identity between these pieces:
AD----> AW 
BD----> BW
AD----> BD
AW-----> BW

This step for each pieces.


```shell
./mutation-simulator.py Phaseolus_vulgaris_SUB1_sequence_AD.fa args -sn 0.09 >  Phaseolus_vulgaris_SUB1_sequence_AW.fa  #similarity sequences 91 %
```


For check similarity between all pieces:

```shell
at Phaseolus_vulgaris_SUB1_AD.fa Phaseolus_vulgaris_SUB1_AW.fa Phaseolus_vulgaris_SUB1_BD.fa Phaseolus_vulgaris_SUB1_BW.fa Phaseolus_vulgaris_synthetase_AD.fa Phaseolus_vulgaris_synthetase_AW.fa Phaseolus_vulgaris_synthetase_BD.fa Phaseolus_vulgaris_synthetase_BW.fa > SUB1+SYNT90.fa

./clustalo-1.2.4-Ubuntu-32-bit -i /home/flavia/Lab/phaesolus/identity93/SUB1+SYNT90.fa --full --percent-id --distmat-out=90identity8pieces
```

I join pieces together for obtained four artificial sequences:

- synt+SUB1_AD
- synt+SUB1_AW
- synt+SUB1_BD
- synt+SUB1_BW
