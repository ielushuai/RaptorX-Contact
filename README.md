# RaptorX-Contact: a software package for protein contact and distance prediction by deep residual neural network. 
This package has source code of the deep learning method developed by Xu group for protein contact/distance prediction and distance-based folding. The code and documentation will be improved gradually. Anaconda (for Python 2.7), Theano and possibly BioPython shall be installed in order to use this package.

The package contains core code used to produce results in the following papers. 
1) Analysis of distance-based protein structure prediction by deep learning in CASP13. PROTEINS, 2019
2) Distance-based protein folding powered by deep learning. PNAS, August 2019. A 2-page abstract also appeared at RECOMB2019 in April 2019.
3) Protein threading using residue co-variation and deep learning, ISMB and Bioinformatics, July 2018. This paper describes how to extend deep learning to distance prediction.
4) ComplexContact: a web server for inter-protein contact prediction using deep learning. NAR, May 2018
5) Analysis of deep learning methods for blind protein contact prediction in CASP12. PROTEINS, March 2018
6) Folding Membrane Proteins by Deep Transfer Learning. Cell Systems, September 2017. This paper shows in details that deep ResNet works well on membrane proteins even if trained without any membrane proteins.
7) Accurate De Novo Prediction of Protein Contact Map by Ultra-Deep Learning Model. PLoS CB, Jan 2017. An early version was first posted to bioRxiv and arXiv in September 2016. See https://www.biorxiv.org/content/10.1101/073239v8 and https://arxiv.org/abs/1609.00680. This is the first paper that describes deep convolutional residual neural network for protein contact prediction. This paper also shows that contacts predicted by deep ResNet can fold large proteins without detectable homology in PDB. 

Some auxiliary code will be gradually uploaded.

The testsets used in the PLoS CB paper and the multiple sequence alignment for the CASP13 hard targets are available at http://raptorx.uchicago.edu/download/ . Two deep models are also available for download at the same site. After login this site,
please check out 0README.data4contactPrediction.txt and 0README.models4ContactDistancePrediction.txt for the download of data and models.

Here are a list of input features needed for our deep models: 
1) primary sequence represented as a string of letters (upper case);
2) position-specific scoring matrix represented as a L*20 matrix. You may generate multiple sequence alignment by PSI-BLAST/HHblits/Jackhmmer and then construct such a matrix. To generate such a matrix from an HHM file (generated by HHblits/HHpred), you may use the script LoadHHM.py in the folder Common/ .
3) predicted secondary structure confidence score represented as a L*3 matrix. Please make sure that the order of Helix, Beta and Loop is consistent with our example data. You may determine our order by comparing the confidence scores. We used DeepCNF_SS_Con at https://github.com/realbigws/Predict_Property/tree/master/bin to predict secondary structure.
4) predicted solvent accessibility score represented as a L*3 matrix. Again please make sure that the order of the three labels is consistent with our example data. We used AcconPred at https://github.com/realbigws/Predict_Property/tree/master/bin to predict solvent accessibility.
5) normalized CCMpred matrix (L*L), i.e., the original CCMpred output matrix normalized by its mean and standard deviation. We used option "-R -d GPU" to run CCMpred where GPU is the ID of GPU (e.g., 1) on your machine.
6) three other 2D matrices (each has shape L*L) for pairwsie relationship generated by alnstats in MetaPSICOV. You may download the code at https://github.com/psipred/metapsicov/blob/master/src/alnstats.c . 

For a single protein, its features are deposited as a Python dict(). Please check out our testdata for the dict() keys and exact format. The keys related to PSICOV and disorder information are not needed. In addition, protein name and sequence length are also needed in the dict(), although they are not used as input features. The input features of all test proteins are saved as a list of dict() and then packed as a cPickle file. 

Contact: Jinbo Xu, jinboxu@gmail.com
