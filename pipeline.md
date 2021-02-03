### Before calculating the convergent evolution

1. I downloaded two genes of Phaseolus from ENSEMBL Plants: **SUB1 e synthetase**

http://plants.ensembl.org/Phaseolus_vulgaris/Gene/Sequence?db=core;g=PHAVU_010G148300g;r=10:41896617-41903193;t=ESW07662
http://plants.ensembl.org/Phaseolus_vulgaris/Gene/Sequence?db=core;g=PHAVU_002G236500g;r=2:40207854-40209575;t=ESW31409

The len of these two genes is 2922.

2. I should generate two couple of sequences from these genes with 50 % of identity. 

- So for generate random mutations, I used this:  https://github.com/mkpython3/Mutation-Simulator

I would obtained four pieces:

Gene SUB1 Domesticated and gene SUB1 WT (already downloaded)---> 50 % of identity between these

Gene Synthetase Domesticated and Gene Synthetase WT (already downloaded)--> 50 % of identity between these


I obtained two new pieces, SUB1 Domesticated and Synthetase Domesticated:

```shell
./mutation-simulator.py Phaseolus_vulgaris_SUB1_sequence.fa args -sn 0.50     
./mutation-simulator.py Phaseolus_vulgaris_synthetase_sequence.fa args -sn 0.50
```


Per check if the similarity is right from the sequence obtained by ensembl and the last for each gene I used this:

```shell
./clustalo-1.2.4-Ubuntu-32-bit -i syntetasewt+syntetasedom+sub1wt+sub1dom_50.fa --full --percent-id --distmat-out=50identity.distmat
```

I obtained a divergent matrix.

- I built the tree:

```shell
./clustalo-1.2.4-Ubuntu-32-bit -i syntetasewt+syntetasedom+sub1wt+sub1dom_50.fa -o clustal.aln --guidetree-out treeseq50 --outfmt=clustal
```

3. I should generate two couple of sequences with 90 % of identity from the previous pieces

- From Gene SUB1 Domesticated: I obtaine SUB1 DOM and SUB1 DOM1---> 90 % between these
- From Gene SUB1 wt: I obtaine SUB1wt and SUB1wt1--> 90 % between these
- From Gene synthetase domesticated: synthetase dom and synthetasedom1--> 90%
- From the Gene synthetase wt: synthetase wt and synthetase wt1--> 90 %

I obtained these with this step for each pieces:

```shell
./mutation-simulator.py Phaseolus_vulgaris_SUB1_sequence_wt.fa args -sn 0.09 >  Phaseolus_vulgaris_SUB1_sequence_wt1.fa  #similarity sequences 91 %
```

For check similarity between all pieces:

```shell
./clustalo-1.2.4-Ubuntu-32-bit -i SUB1dom+SUBdom1+SUB1wt+SUB1wt1+syntedom+syntedom1+syntewt+syntewt1.fa --full --percent-id --distmat-out=90identity8pieces
```
For build tree:

```shell
./clustalo-1.2.4-Ubuntu-32-bit -i SUB1dom+SUBdom1+SUB1wt+SUB1wt1+syntedom+syntedom1+syntewt+syntewt1.fa -o clustal.aln --guidetree-out treeseq90 --outfmt=clustal                                                                          
```
