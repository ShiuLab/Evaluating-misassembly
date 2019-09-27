# Evaluating-misassembly
Factors influencing and machine learning models predicting read coverage in a genome assembled using short reads

> ## Step 01: Map genome sequencing reads to tomato genome.

> ## Step 02: Determine the optimal bin size.

> ## Step 03: Determine the read depth (RD) in each bin region.

> ## Step 04: HC/LC designation

Determine regions with significantly higher (HC) or lower (LC) read coverages than genome wide average (background, BG). 

Note that in outputs of CNVnator, HC is referred to as "duplication", while LC is "deletion". The remain regions were taken as BG.
          
> ## Step 05: HC/LC designation filtering

Adjust p-values (q-value), then filter HC/LC regions based on q-value and q0 value. Before that q-value threshold was determined by evaluating the consistency between results using original reads and resampled reads. Reads were resampled based on simulated RDs: i) the only possible RD values were 0 (LC), 1 (BG), or 2 (HC) regions; ii) the analysisoriginal RD values were discretized (rounded) to their closest integers; iii) the analysis RD were used.

> ## Step 06: Determine HC/LC/BG regions with high confidence

Compare RD in HC, LC, and BG regions, then determine the threshold to call HC/LC/BG regions with high confidence.

> ## Step 07: Accuracy and precision of HC/LC/BG calling

To evaluate the accuracy and precision of HC/LC/BG calling, resample reads from genome with simulated RDs, and rerun CNVnator again and compare the original RDs (anslysis RDs) with the new RD. The simulated RDs are: i) the only possible RD values were 0 (LC), 1 (BG), or 2 (HC) regions; ii) the analysisoriginal RD values were discretized (rounded) to their closest integers; iii) the analysis RD were used.
          
> ## Step 08: Impact of read coverage on RD determination

To assess the extent to which read coverage impacts the RD determination, reads at 5-fold, 10-fold, 20-fold and 30-fold coverages were resampled from dataset2, and were used to rerun CNVnator.

> ## Step 09: Get the features to build the machine learning models

> ## Step 10: Build 3-class prediction models using Random Forest

> ## Step 11: Get importance value of each feature in the prediction models
  
 python 11_tree-based_FS.py your_dataset your_classes_list

> ## Step 12: Select K-mer and SSR features based on p-value of Kruskal-Wallis H test
 python 12_KS_test.py path_to_your_files output_name
       
> ## Step 13: Determine the correlation between densities of HC/LC/BG regions with densities of genome features.

> ## Step 14: Determine the correlation of prevalence of HC/LC/BG and genome features

To assess how the observed correlation between densities of HC/LC/BG regions with densities of genome features derived from random expectation, HC/LC/BG regions were reshuffled across the genome 1000 times, where HC/LC/BG regions don't overlap with each other.

> ## Step 15: Estimate gene proproties located in HC regions

To evaluate the properties of genes located in HC regions, first the number of each type of gene overlapping with HC regions were determined. Next, regions with same number and length of HC regions were randomly selected from BG regions, which was repeat 10,000 times. The observed numbers of genes were compared with the random null distribution to see which type of gene is over- or under-representative.

> ## Step 16: Gene set enrichment analysis (Fisher’s exact test)
 
 python 13_01_Test_Fisher.py your_file 0/1  ## contributed by Sahra Uygun
  
> ## Step 17: Validation of HC regions

To validate the HC regions detected in our study, one regions assembled using PCR sequneces was compared to the corresponding region assembled using short reads

