# ScAtt: an Attention based architecture to analyze Alzheimer's disease at cell type level from single-cell RNA-sequencing data  

**Alzheimer's disease** (AD) is a pervasive neurodegenerative disorder that leads to memory and behavior impairment that affects over 35 million people globally. Single-cell RNA sequencing technology (scRNA-seq) has allowed the studying of Alzheimer’s disease at the molecular level. Many machine learning methods have been proposed to analyze AD using scRNA-seq data. Despite their high accuracy in various tasks, the models provide limited information for AD for further analysis. In this paper, we propose an end-to-end attention based architecture, ScAtt, to analyze AD. ScAtt takes scRNA-seq data of all cells in a particular cell type as input and uses attention-based transformer architecture to aggerate global and local information to capture the complex linear and nonlinear patterns in the gene feature data. Our method can provide various types of information learned from scRNA-seq data, enabling studying AD from multiple perspectives. The merits of our method include: (1) It can accurately predict cell state (AD versus control) for different cell types; (2) It provides the importance of gene features related to AD. More importantly, it can extract unique genes associated with specific cell types that affect AD; (3) It can construct cell-type-specific gene-gene interaction networks using the gene feature embeddings provided by the trained model and uncover modules of genes that are most informative for cell state. Results show that our method performs better on cell state prediction than other machine learning methods. Importantly, it captures more cell-type-specific unique genes related to AD, with far less overlap between cell types than traditional marginal association methods, which could help to analyze the effect of genes from different types of cells on AD. Lastly, functional enrichments of the identified AD modules show significant enrichment of biologically meaningful AD-related pathways, discovering uniqueness in functional enrichments between different cell types. This is the source code for the method as described in our paper:
**ScAtt: an Attention based architecture to analyze Alzheimer's disease at cell type level from single-cell RNA-sequencing data**. 

<div align=center><img width="1000" height="600" src="https://github.com/circustata/ScAtt/blob/main/figure/model_framework_whole_structure.jpg"/></div>
<p align="left">
The framework of our end-to-end Transformer based method. In the data processing component, the single-cell RNA expression profiles of AD patients and control individuals are obtained and shuffled. In the Transformer component, a linear layer converts the processed data into lower-dimensional representations. After that, the Transformer encoder learns the relationships between each cell. Finally, the model can be trained to identify the source for the cells through the loss function.
</p>

## Data
The scRNA-seq data of 95,186 single-nucleus transcriptomes from 17 hippocampus (8 controls and 9 AD cases), stratified by 14 cell types, were used to evaluate the performance of our model. In order to make it easier for the readers to reproduce and understand the code, we have provided a small amount of **synthesized** Arterial cell type related data under the **dataset** folder, where provides 20 synthesized scRNA-seq data for each patient.

Cell type | Training cell number | Validation cell number | Test cell number |
---- | --- | --- | --- |
Oligo | 16,293 | 2,743 | 3,880 |
Astrocyte | 10,627 | 2,287 | 3,840 |
Pericyte | 10,383 | 1,610 | 3,791 |
Capillary | 7,500 | 1,847 | 3,111 |
Veinous | 3,852 | 1,011 | 1,897 |
SMC | 2,961 | 899 | 1,570 |
Arterial | 2,338 | 606 | 1,433 |
OPC | 2,177 | 308 | 624 |
Microglia | 1,854 | 244 | 428 |
P. Fibro | 1,104 | 209 | 641 |
Ependymal | 1,008 | 183 | 289 |
Neuron | 778 | 50 | 270 |
M. Fibro | 124 | 60 | 117 |
T cell | 114 | 31 | 94 |

## Requirements
* inplace_abn==1.1.0
* numpy==1.22.2
* pandas==1.2.4
* pretrainedmodels==0.7.4
* scikit_learn==1.0.2
* torch==1.8.0
* torchvision==0.9.0

## File declaration
**data/scRNASeq.py**：the data preprocessing step.

**models/AttentionBasedModel.py**：The Transformer-based method.

**main.py**: The codes for training, validating and testing.

## Run the codes
Install the environment.
```bash
pip install -r requirements.txt
```
Train and test the model.
```bash
python main.py
```

## Results

#### Cell type level results
The detailed results of the cell source identification for 14 cell types. 
<table>
<tr>
<td><b>Method</b></td>
<td><b>AUC</b></td>
<td><b>ACC</b><sup>a</sup></td>
<td><b>PPV</b><sup>b</sup></td>
<td><b>Sensitivity</b></td>
<td><b>F-score</b></td>
<td><b>Specificity</b></td>
<td><b>NPV</b><sup>c</sup></td>
</tr>
<tr>
<td colspan="8" align=center><b>Veinous</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.886 </td>
<td>0.763 </td>
<td>0.855 </td>
<td>0.583 </td>
<td>0.693 </td>
<td>0.583 </td>
<td>0.720 </td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.861 </td>
<td>0.756 </td>
<td>0.797 </td>
<td>0.631 </td>
<td>0.705 </td>
<td>0.631 </td>
<td>0.733 </td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.645 </td>
<td>0.541 </td>
<td>1.000 </td>
<td>0.003 </td>
<td>0.007 </td>
<td>0.003 </td>
<td>0.541 </td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.828 </td>
<td>0.724 </td>
<td>0.788 </td>
<td>0.549 </td>
<td>0.647 </td>
<td>0.549 </td>
<td>0.694 </td>
</tr>
<tr>
<td>XGboost</td>
<td>0.854 </td>
<td>0.746 </td>
<td>0.816 </td>
<td>0.580 </td>
<td>0.678 </td>
<td>0.580 </td>
<td>0.713 </td>
</tr>
<tr>
<td>Ours</td>
<td>0.935</td>
<td>0.849</td>
<td>0.877</td>
<td>0.781</td>
<td>0.826</td>
<td>0.781</td>
<td>0.829</td>
</tr>
<tr>
  <td colspan="8" align=center><b>SMC</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.958 </td>
<td>0.892 </td>
<td>0.919 </td>
<td>0.838 </td>
<td>0.876 </td>
<td>0.838 </td>
<td>0.874 </td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.955 </td>
<td>0.894 </td>
<td>0.895 </td>
<td>0.870 </td>
<td>0.882 </td>
<td>0.870 </td>
<td>0.894 </td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.824 </td>
<td>0.762 </td>
<td>0.705 </td>
<td>0.819 </td>
<td>0.758 </td>
<td>0.819 </td>
<td>0.826 </td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.927 </td>
<td>0.854 </td>
<td>0.856 </td>
<td>0.815 </td>
<td>0.835 </td>
<td>0.815 </td>
<td>0.852 </td>
</tr>
<tr>
<td>XGboost</td>
<td>0.923 </td>
<td>0.846 </td>
<td>0.819 </td>
<td>0.849 </td>
<td>0.834 </td>
<td>0.849 </td>
<td>0.870 </td>
</tr>
<tr>
<td>Ours</td>
<td>0.972 </td>
<td>0.923</td>
<td>0.942</td>
<td>0.885</td>
<td>0.913</td>
<td>0.885</td>
<td>0.909</td>
</tr>
<tr>
  <td colspan="8" align=center><b>Arterial</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.898 </td>
<td>0.746 </td>
<td>0.915 </td>
<td>0.534 </td>
<td>0.674 </td>
<td>0.534 </td>
<td>0.678 </td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.867 </td>
<td>0.749 </td>
<td>0.871 </td>
<td>0.575 </td>
<td>0.693 </td>
<td>0.575 </td>
<td>0.690 </td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.763 </td>
<td>0.620 </td>
<td>0.732 </td>
<td>0.360 </td>
<td>0.482 </td>
<td>0.360 </td>
<td>0.584 </td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.857 </td>
<td>0.763 </td>
<td>0.830 </td>
<td>0.652 </td>
<td>0.730 </td>
<td>0.652 </td>
<td>0.720 </td>
</tr>
<tr>
<td>XGboost</td>
<td>0.865 </td>
<td>0.760 </td>
<td>0.830 </td>
<td>0.644 </td>
<td>0.726 </td>
<td>0.644 </td>
<td>0.716 </td>
</tr>
<tr>
<td>Ours</td>
<td>0.956 </td>
<td>0.872</td>
<td>0.922</td>
<td>0.807</td>
<td>0.861</td>
<td>0.807</td>
<td>0.833</td>
</tr>
<tr>
  <td colspan="8" align=center><b>P. Fibro</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.922 </td>
<td>0.716 </td>
<td>0.931 </td>
<td>0.466 </td>
<td>0.621 </td>
<td>0.466 </td>
<td>0.644 </td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.912 </td>
<td>0.727 </td>
<td>0.914 </td>
<td>0.500 </td>
<td>0.646 </td>
<td>0.500 </td>
<td>0.657 </td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.652 </td>
<td>0.502 </td>
<td>1.000 </td>
<td>0.003 </td>
<td>0.006 </td>
<td>0.003 </td>
<td>0.502 </td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.856 </td>
<td>0.657 </td>
<td>0.917 </td>
<td>0.344 </td>
<td>0.500 </td>
<td>0.344 </td>
<td>0.597 </td>
</tr>
<tr>
<td>XGboost</td>
<td>0.877 </td>
<td>0.672 </td>
<td>0.958 </td>
<td>0.359 </td>
<td>0.523 </td>
<td>0.359 </td>
<td>0.607 </td>
</tr>
<tr>
<td>Ours</td>
<td>0.932 </td>
<td>0.856</td>
<td>0.835</td>
<td>0.887</td>
<td>0.861</td>
<td>0.887</td>
<td>0.880</td>
</tr>
<tr>
  <td colspan="8" align=center><b>Ependymal</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.694 </td>
<td>0.637 </td>
<td>0.451 </td>
<td>0.327 </td>
<td>0.379 </td>
<td>0.327 </td>
<td>0.697 </td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.637 </td>
<td>0.633 </td>
<td>0.465 </td>
<td>0.541 </td>
<td>0.500 </td>
<td>0.541 </td>
<td>0.743 </td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.565 </td>
<td>0.626 </td>
<td>0.444 </td>
<td>0.408 </td>
<td>0.426 </td>
<td>0.408 </td>
<td>0.709 </td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.740 </td>
<td>0.692 </td>
<td>0.622 </td>
<td>0.235 </td>
<td>0.341 </td>
<td>0.235 </td>
<td>0.702 </td>
</tr>
<tr>
<td>XGboost</td>
<td>0.738 </td>
<td>0.692 </td>
<td>0.615 </td>
<td>0.245 </td>
<td>0.350 </td>
<td>0.245 </td>
<td>0.704 </td>
</tr>
<tr>
<td>Ours</td>
<td>0.823 </td>
<td>0.709</td>
<td>0.547</td>
<td>0.827</td>
<td>0.659</td>
<td>0.827</td>
<td>0.879</td>
</tr>
<tr>
  <td colspan="8" align=center><b>Microglia</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.909 </td>
<td>0.783 </td>
<td>0.947 </td>
<td>0.656 </td>
<td>0.775 </td>
<td>0.656 </td>
<td>0.676 </td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.916 </td>
<td>0.745 </td>
<td>0.953 </td>
<td>0.582 </td>
<td>0.723 </td>
<td>0.582 </td>
<td>0.634 </td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.639 </td>
<td>0.636 </td>
<td>0.718 </td>
<td>0.594 </td>
<td>0.650 </td>
<td>0.594 </td>
<td>0.562 </td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.860 </td>
<td>0.738 </td>
<td>0.847 </td>
<td>0.660 </td>
<td>0.742 </td>
<td>0.660 </td>
<td>0.651 </td>
</tr>
<tr>
<td>XGboost</td>
<td>0.903 </td>
<td>0.794 </td>
<td>0.915 </td>
<td>0.705 </td>
<td>0.796 </td>
<td>0.705 </td>
<td>0.700 </td>
</tr>
<tr>
<td>Ours</td>
<td>0.928 </td>
<td>0.813</td>
<td>0.956</td>
<td>0.705</td>
<td>0.811</td>
<td>0.705</td>
<td>0.710</td>
</tr>
<tr>
 <td colspan="8" align=center><b>OPC</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.780 </td>
<td>0.720 </td>
<td>0.676 </td>
<td>0.627 </td>
<td>0.651 </td>
<td>0.627 </td>
<td>0.747 </td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.759 </td>
<td>0.694 </td>
<td>0.639 </td>
<td>0.612 </td>
<td>0.625 </td>
<td>0.612 </td>
<td>0.731 </td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.640 </td>
<td>0.627 </td>
<td>0.536 </td>
<td>0.769 </td>
<td>0.632 </td>
<td>0.769 </td>
<td>0.761 </td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.714 </td>
<td>0.660 </td>
<td>0.575 </td>
<td>0.712 </td>
<td>0.636 </td>
<td>0.712 </td>
<td>0.752 </td>
</tr>
<tr>
<td>XGboost</td>
<td>0.764 </td>
<td>0.692 </td>
<td>0.622 </td>
<td>0.665 </td>
<td>0.643 </td>
<td>0.665 </td>
<td>0.749 </td>
</tr>
<tr>
<td>Ours</td>
<td>0.858 </td>
<td>0.720</td>
<td>0.615</td>
<td>0.877</td>
<td>0.723</td>
<td>0.877</td>
<td>0.874</td>
</tr>
<tr>
  <td colspan="8" align=center><b>Neuron</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.809 </td>
<td>0.774 </td>
<td>0.684 </td>
<td>0.600 </td>
<td>0.639 </td>
<td>0.600 </td>
<td>0.812 </td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.857 </td>
<td>0.781 </td>
<td>0.682 </td>
<td>0.644 </td>
<td>0.663 </td>
<td>0.644 </td>
<td>0.827 </td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.551 </td>
<td>0.619 </td>
<td>0.420 </td>
<td>0.378 </td>
<td>0.398 </td>
<td>0.378 </td>
<td>0.704 </td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.721 </td>
<td>0.711 </td>
<td>0.567 </td>
<td>0.567 </td>
<td>0.567 </td>
<td>0.567 </td>
<td>0.783 </td>
</tr>
<tr>
<td>XGboost</td>
<td>0.784 </td>
<td>0.733 </td>
<td>0.594 </td>
<td>0.633 </td>
<td>0.613 </td>
<td>0.633 </td>
<td>0.810 </td>
</tr>
<tr>
<td>Ours</td>
<td>0.881 </td>
<td>0.752</td>
<td>0.595</td>
<td>0.800</td>
<td>0.682</td>
<td>0.800</td>
<td>0.879</td>
</tr>
<tr>
    <td colspan="8" align=center><b>M. Fibro</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.727 </td>
<td>0.675 </td>
<td>0.588 </td>
<td>0.638 </td>
<td>0.612 </td>
<td>0.638 </td>
<td>0.742 </td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.859 </td>
<td>0.718 </td>
<td>0.613 </td>
<td>0.809 </td>
<td>0.697 </td>
<td>0.809 </td>
<td>0.836 </td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.537 </td>
<td>0.496 </td>
<td>0.427 </td>
<td>0.745 </td>
<td>0.543 </td>
<td>0.745 </td>
<td>0.657 </td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.779 </td>
<td>0.650 </td>
<td>0.544 </td>
<td>0.787 </td>
<td>0.643 </td>
<td>0.787 </td>
<td>0.796 </td>
</tr>
<tr>
<td>XGboost</td>
<td>0.795 </td>
<td>0.718 </td>
<td>0.613 </td>
<td>0.809 </td>
<td>0.697 </td>
<td>0.809 </td>
<td>0.836 </td>
</tr>
<tr>
<td>Ours</td>
<td>0.774 </td>
<td>0.701</td>
<td>0.607</td>
<td>0.723</td>
<td>0.660</td>
<td>0.723</td>
<td>0.787</td>
</tr>
<tr>
  <td colspan="8" align=center><b>T cell</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.540 </td>
<td>0.521 </td>
<td>0.500 </td>
<td>0.778 </td>
<td>0.609 </td>
<td>0.778 </td>
<td>0.583 </td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.594 </td>
<td>0.553 </td>
<td>0.526 </td>
<td>0.667 </td>
<td>0.588 </td>
<td>0.667 </td>
<td>0.595 </td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.623 </td>
<td>0.606 </td>
<td>0.583 </td>
<td>0.622 </td>
<td>0.602 </td>
<td>0.622 </td>
<td>0.630 </td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.645 </td>
<td>0.628 </td>
<td>0.581 </td>
<td>0.800 </td>
<td>0.673 </td>
<td>0.800 </td>
<td>0.719 </td>
</tr>
<tr>
<td>XGboost</td>
<td>0.597 </td>
<td>0.564 </td>
<td>0.530 </td>
<td>0.778 </td>
<td>0.631 </td>
<td>0.778 </td>
<td>0.643 </td>
</tr>
<tr>
<td>Ours</td>
<td>0.624 </td>
<td>0.574</td>
<td>0.558</td>
<td>0.533</td>
<td>0.545</td>
<td>0.533</td>
<td>0.588</td>
</tr>
<tr>
<td colspan="8" align=center><b>Pericyte</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.971</td>
<td>0.848</td>
<td>0.962</td>
<td>0.695</td>
<td>0.807</td>
<td>0.695</td>
<td>0.792</td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.973</td>
<td>0.865</td>
<td>0.967</td>
<td>0.728</td>
<td>0.831</td>
<td>0.728</td>
<td>0.811</td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.880</td>
<td>0.765</td>
<td>0.908</td>
<td>0.540</td>
<td>0.677</td>
<td>0.540</td>
<td>0.712</td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.967</td>
<td>0.838</td>
<td>0.959</td>
<td>0.673</td>
<td>0.791</td>
<td>0.673</td>
<td>0.781</td>
</tr>
<tr>
<td>XGboost</td>
<td>0.968</td>
<td>0.858</td>
<td>0.949</td>
<td>0.726</td>
<td>0.823</td>
<td>0.726</td>
<td>0.808</td>
</tr>
<tr>
<td>Ours</td>
<td>0.976 </td>
<td>0.923</td>
<td>0.917</td>
<td>0.913</td>
<td>0.915</td>
<td>0.913</td>
<td>0.928</td>
</tr>
<tr>
<td colspan="8" align=center><b>Capillary</b></td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.943</td>
<td>0.726</td>
<td>0.975</td>
<td>0.519</td>
<td>0.678</td>
<td>0.519</td>
<td>0.621</td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.887</td>
<td>0.737</td>
<td>0.906</td>
<td>0.586</td>
<td>0.712</td>
<td>0.586</td>
<td>0.642</td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.792</td>
<td>0.596</td>
<td>0.966</td>
<td>0.282</td>
<td>0.436</td>
<td>0.282</td>
<td>0.525</td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.900</td>
<td>0.724</td>
<td>0.931</td>
<td>0.543</td>
<td>0.686</td>
<td>0.543</td>
<td>0.625</td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.943</td>
<td>0.726</td>
<td>0.975</td>
<td>0.519</td>
<td>0.678</td>
<td>0.519</td>
<td>0.621</td>
</tr>
<tr>
<td>Ours</td>
<td>0.955 </td>
<td>0.833</td>
<td>0.965</td>
<td>0.725</td>
<td>0.828</td>
<td>0.725</td>
<td>0.738</td>
</tr>
<tr>
<td colspan="8" align=center><b>Oligo</b></td>  
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.838</td>
<td>0.760</td>
<td>0.763</td>
<td>0.796</td>
<td>0.779</td>
<td>0.796</td>
<td>0.757</td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.702</td>
<td>0.653</td>
<td>0.650</td>
<td>0.753</td>
<td>0.698</td>
<td>0.753</td>
<td>0.658</td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.610</td>
<td>0.561</td>
<td>0.552</td>
<td>0.921</td>
<td>0.690</td>
<td>0.921</td>
<td>0.630</td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.776</td>
<td>0.695</td>
<td>0.657</td>
<td>0.894</td>
<td>0.757</td>
<td>0.894</td>
<td>0.796</td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.838</td>
<td>0.760</td>
<td>0.763</td>
<td>0.796</td>
<td>0.779</td>
<td>0.796</td>
<td>0.757</td>
</tr>
<tr>
<td>Ours</td>
<td>0.873 </td>
<td>0.788</td>
<td>0.774</td>
<td>0.850</td>
<td>0.810</td>
<td>0.850</td>
<td>0.809</td>
</tr>
<tr>
<td colspan="8" align=center><b>Astrocyte</b></td>  
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.891</td>
<td>0.805</td>
<td>0.811</td>
<td>0.640</td>
<td>0.715</td>
<td>0.640</td>
<td>0.802</td>
</tr>
<tr>
<td>Support Vector Machine</td>
<td>0.913</td>
<td>0.820</td>
<td>0.853</td>
<td>0.641</td>
<td>0.732</td>
<td>0.641</td>
<td>0.806</td>
</tr>
<tr>
<td>Decision Tree</td>
<td>0.690</td>
<td>0.653</td>
<td>0.539</td>
<td>0.667</td>
<td>0.596</td>
<td>0.667</td>
<td>0.757</td>
</tr>
<tr>
<td>AdaBoost</td>
<td>0.842</td>
<td>0.767</td>
<td>0.730</td>
<td>0.625</td>
<td>0.673</td>
<td>0.625</td>
<td>0.786</td>
</tr>
<tr>
<td>Logistic Regression</td>
<td>0.891</td>
<td>0.805</td>
<td>0.811</td>
<td>0.640</td>
<td>0.715</td>
<td>0.640</td>
<td>0.802</td>
</tr>
<tr>
<td>Ours</td>
<td>0.919 </td>
<td>0.837</td>
<td>0.756</td>
<td>0.849</td>
<td>0.799</td>
<td>0.849</td>
<td>0.898</td>
</tr>
<tr>
<td colspan="8"><sup>a</sup>ACC stands for accuracy. <sup>b</sup>PPV stands for positive predictive value. <sup>c</sup>NPV stands for negative predictive value. 
</td>
</tr>
</table>

**The top ten ranking genes based on feature importance for each cell type.**
<table>
   <tr>
      <td><b>Cell Type</b></td>
      <td><b>Top 1</b></td>
      <td><b>Top 2</b></td>
      <td><b>Top 3</b></td>
      <td><b>Top 4</b></td>
      <td><b>Top 5</b></td>
      <td><b>Top 6</b></td>
      <td><b>Top 7</b></td>
      <td><b>Top 8</b></td>
      <td><b>Top 9</b></td>
      <td><b>Top 10</b></td>
   </tr>
   <tr>
      <td><b>T cell</b></td>
      <td>NEAT1</td>
      <td>ADAMTS9</td>
      <td>MBD5</td>
      <td>HSPB1</td>
      <td>UTY</td>
      <td>RNF152</td>
      <td>PCBP3</td>
      <td>ELOVL7</td>
      <td>SGIP1</td>
      <td>REV3L</td>
   </tr>
   <tr>
      <td><b>SMC</b></td>
      <td>ADAMTS9</td>
      <td>PCBP3</td>
      <td>IGFBP4</td>
      <td>DNAJB1</td>
      <td>CEBPD</td>
      <td>PTP4A3</td>
      <td>OSMR</td>
      <td>SERPINH1</td>
      <td>CHORDC1</td>
      <td>SLC12A2</td>
   </tr>
   <tr>
      <td><b>Pericyte</b></td>
      <td>XIST</td>
      <td>SLC6A1-AS1</td>
      <td>APBB2</td>
      <td>SLC20A2</td>
      <td>ATP1A2</td>
      <td>GRID2</td>
      <td>MIR99AHG</td>
      <td>IMMP2L</td>
      <td>PTPRG</td>
      <td>CRIM1</td>
   </tr>
   <tr>
      <td><b>Capillary</b></td>
      <td>ADAMTS9</td>
      <td>PDE10A</td>
      <td>BACE2</td>
      <td>AC092957.1</td>
      <td>CP</td>
      <td>GALNT18</td>
      <td>MEF2A</td>
      <td>HSPA1A</td>
      <td>ADIPOR2</td>
      <td>ELOVL7</td>
   </tr>
   <tr>
      <td><b>Arterial</b></td>
      <td>FLT1</td>
      <td>AC092957.1</td>
      <td>ADAMTS9</td>
      <td>ABCD3</td>
      <td>CP</td>
      <td>RFTN1</td>
      <td>ANO2</td>
      <td>PLSCR4</td>
      <td>BSG</td>
      <td>CRIM1</td>
   </tr>
   <tr>
      <td><b>Oligo</b></td>
      <td>ADAMTS18</td>
      <td>XIST</td>
      <td>MAN2A1</td>
      <td>CIRBP</td>
      <td>LINC01505</td>
      <td>SLC44A1</td>
      <td>PI16</td>
      <td>LPAR1</td>
      <td>SGCD</td>
      <td>IL1RAPL1</td>
   </tr>
   <tr>
      <td><b>P. Fibro</b></td>
      <td>XIST</td>
      <td>CEMIP</td>
      <td>ADAMTS12</td>
      <td>AC093772.1</td>
      <td>FLRT2</td>
      <td>ATP1A2</td>
      <td>ABCA1</td>
      <td>IL1RAPL1</td>
      <td>RNF220</td>
      <td>DLG2</td>
   </tr>
   <tr>
      <td><b>Ependymal</b></td>
      <td>TTTY14</td>
      <td>UTY</td>
      <td>AC092957.1</td>
      <td>AC019330.1</td>
      <td>PDE4DIP</td>
      <td>TMEM161B-AS1</td>
      <td>BOC</td>
      <td>CFAP46</td>
      <td>MT-ATP6</td>
      <td>ERBIN</td>
   </tr>
   <tr>
      <td><b>Microglia</b></td>
      <td>ACSL1</td>
      <td>SLC11A1</td>
      <td>XIST</td>
      <td>PDE3B</td>
      <td>HSPB1</td>
      <td>RUNX1</td>
      <td>TBC1D14</td>
      <td>ELL2</td>
      <td>TMEM163</td>
      <td>SEC14L1</td>
   </tr>
   <tr>
      <td><b>Astrocyte</b></td>
      <td>LINC00278</td>
      <td>DGKB</td>
      <td>MT-ATP6</td>
      <td>TMTC1</td>
      <td>MT-ND2</td>
      <td>OSMR-AS1</td>
      <td>ADCY9</td>
      <td>DDIT4</td>
      <td>IRS2</td>
      <td>ELOVL7</td>
   </tr>
   <tr>
      <td><b>OPC</b></td>
      <td>VEGFA</td>
      <td>ADAMTS9-AS2</td>
      <td>BNIP3L</td>
      <td>RBFOX1</td>
      <td>GALNT18</td>
      <td>SCARB1</td>
      <td>VWF</td>
      <td>HSPA1B</td>
      <td>ADAMTS9</td>
      <td>OSMR</td>
   </tr>
   <tr>
      <td><b>M. Fibro</b></td>
      <td>PCDHA1</td>
      <td>MAPK8IP1</td>
      <td>PRR29-AS1</td>
      <td>TRPC3</td>
      <td>CNTN4-AS1</td>
      <td>FZD7</td>
      <td>P3H2-AS1</td>
      <td>FCAR</td>
      <td>GCK</td>
      <td>ANKRD27</td>
   </tr>
   <tr>
      <td><b>Neuron</b></td>
      <td>MT-ATP6</td>
      <td>XKR6</td>
      <td>MT-ND4</td>
      <td>NEAT1</td>
      <td>TTTY14</td>
      <td>PRKG1</td>
      <td>FLT1</td>
      <td>ZNF638</td>
      <td>NALCN</td>
      <td>TTC3</td>
   </tr>
   <tr>
      <td><b>Veinous</b></td>
      <td>XIST</td>
      <td>SLC39A10</td>
      <td>GPCPD1</td>
      <td>APBB2</td>
      <td>ABCG2</td>
      <td>FGD6</td>
      <td>NR3C1</td>
      <td>PGM5</td>
      <td>IL1RAPL1</td>
      <td>TXNIP</td>
   </tr>
   <tr>
      <td></td>
   </tr>
</table>


The experimental results show that our model could be used for predicting AD and also for studying the AD-related genes. We hope our method could help researchers for studing Alzheimer’s disease. The method also can be applied to single-cell data for other diseases.
