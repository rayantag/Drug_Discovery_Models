This repository contains the code for 2 models (currently) that have been trained with the goal of discovering novel drug molecules. The first is modeled after the paper "Predicting Drug–Target Interaction Using a Novel Graph Neural Network with 3D Structure-Embedded Graph Representation". The architecture introduces a "distance-aware graph attention algorithm to differentiate various type sof intermolecular interactions. Furthermore, [they] extract the graph feature of intermolecular interactions directly from the 3D structural information on the protein-ligand binging pose." I trained the model using Google Colab and showed promising results--however, I could not efficiently obtain protein-ligand docking posesin the for which the model was trained on, so screening thousands of ligands against a protein conformation was not feasible with my computational resources. HTE experiments from a lab would be very useful here.

As a result, I tried a different approach, drawing inspiration from "Deep generative model for drug design from protein target sequence." They propose a 3-module architecture which conditions the generation of a ligand SMILES sequence on an amino acid input. I was able to follow closely until their use of a large heteroencoder, used to decode the latent representation of a protein into a SMILES string. Due to extremely long training times on both Colab and SageMaker, I have explored other opportunities in fine-tuning this model, including the training of the WGan. As a result, the molecules generated are not closely resembling true ligands conditioned on some protein sequence, but this is a work in progress. 

I am currently exploring other models that do not require extensive experimental data/docking algorithms for ligand generation, and once this is accomplished I will benchmark the generated compounds with MOSES or some other accepted format. 

DEMO: Currently an very **PRIMITIVE** demo version can be viewed at https://main--sparkling-fox-28df8d.netlify.app/. The user input is processed by a pretrained BioBERT model fine-tuned on disease-gene associativity scores, and then converted into the corresponding amino acid sequence. During fine-tuning, gradual unfreezing and slanted triangular learning rates were used; however, predictions were very volatile and I will use a different approach altogether. Knowledge graphs mapping diseases to potential genes based on PubMed abstracts are an alternative, and I have also begun using Amazon Omics for GWAS using the breadth of -omics data available online. More to come.

Sources: 

Predicting Drug–Target Interaction Using a Novel Graph Neural Network with 3D Structure-Embedded Graph Representation
Jaechang Lim, Seongok Ryu, Kyubyong Park, Yo Joong Choe, Jiyeon Ham, and Woo Youn Kim
Journal of Chemical Information and Modeling 2019 59 (9), 3981-3988
DOI: 10.1021/acs.jcim.9b00387

Chen, Y., Wang, Z., Wang, L. et al. Deep generative model for drug design from protein target sequence. J Cheminform 15, 38 (2023). https://doi.org/10.1186/s13321-023-00702-2

Structure-Based Drug Discovery with Deep Learning
R. Özçelik, D. van Tilborg, J. Jiménez-Luna, F. Grisoni
04 April 2023 https://doi.org/10.1002/cbic.202200776