# Generating_molecules-GAN-
In this project, I try to generate new molecules active against EGFR receptor using GANs
## Introduction
The target I chose this time is the EGFR receptor. The reason for choosing a different
target was the unavailability of a large number of compounds against PKCα since
training GANs require a large amount of data. The EGFR receptor had ~13,900
compounds in the ChEMBL database. It is a biological target for a variety of diseases
including cancer, psoriasis, eczema, atherosclerosis,multi organ epithelial inflammation
and tissue fibrosis.
## Objective
The objective of this project is to produce novel compounds by feeding our GAN model
with the set of active compounds against our biological target - EGFR receptor. Next
was predicting the bioactivity, solubility and toxicity of these novel compounds using ML
models used in the last assignment. QED and SA scores were calculated using the
RDKit package in python.
## Methodology
1. I downloaded the bioactivites dataset for EGFR receptor from the ChEMBL
database. Only the IC50 parameter was considered for this particular assignment
and also because it had the highest number of active compounds (~13,900).
2. The IC50 values were converted to pIC50 values and pIC50>8 were considered
as active which gave us 1109 compounds as inactive and the remaining
compounds as active.
3. The active compounds were undersampled in order to have a balanced dataset.
4. The solubility dataset was downloaded from AqSolDB from the Harvard
dataverse. It had 9983 compounds in the database with logS values. The logS
values >=-2 were labelled as soluble & the logS<-4 as insoluble.
5. The toxicity dataset was taken from : https://github.com/pulimeng/eToxPred. It
contained 8948 compounds with safe compounds labelled as ‘0’ and toxic
compounds labelled as ‘1’.
6. All the molecular descriptors were calculated using the RDKit node in Knime.
7. The ML models for predicting toxicity, solubility and bioactivities were done using
Sci-Kit learn in Python
8. The SMILES for compounds were on-hot encoded and fed into the GAN model.
The architecture was similar to the original Ian Goodfellow GAN model from his
seminal 2014 paper.
9. The produced molecules were checked against the list of molecules used to train
the GAN and only the ‘novel’ molecules were considered for subsequent
analysis
## Discussion
This assignment has the centerpiece objective of producing ‘novel’ molecules against
our target : EGFR receptor. Solubility and toxicity were calculated using models already
used in the Assignment 2. I had to build ML models for classifying our compounds as
either active or inactive. Random Forest was the best model for classification with an
F-score of 84.19%.
The SMILES for the molecules active against EGFR receptor were one-hot encoded
and then inputted into the GAN model. The GAN architecture was the same as the
original Ian Goodfellow paper of 2014: https://arxiv.org/abs/1406.2661. The code was
tweaked to accommodate the one-hot encoding of molecules as well as decoding the
encoded matrix that was outputted by the GAN model. The batch size was set as 16
and the number of epochs was set at 100. A molecule was sampled at the start of each
epoch and hence 100 molecules were sampled. I considered only the last 20 molecules
as they would be the best fine-tuned molecules. I found 12 ‘novel’ molecules out of
those 20. Here novel means molecules not found in the input dataset.
The next thing was predicting solubility, toxicity and bioactivity of these compounds
using the built ML models. SA and QED scores were calculated using RDKit package
The following were the non-toxic, soluble and biologically active compounds :
![pic1](https://user-images.githubusercontent.com/72453054/167280323-50f554fb-d033-4e1c-899b-3e7caf908097.png)

![pic4](https://user-images.githubusercontent.com/72453054/167280369-01d3984f-c5b8-4284-9d5a-d82b8de3deee.png)

![pic8](https://user-images.githubusercontent.com/72453054/167280390-08e4b97a-1679-49d1-8dac-61cdbadc6d05.png)

These three compounds I believe could be subsequently tried to synthesize them in a
lab and the bioactivities experimentally determined.
