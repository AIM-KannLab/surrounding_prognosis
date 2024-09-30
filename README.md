# surrounding_prognosis
## Impact of Peritumoral Zone on Glioblastoma Prognosis based on Deep Learning Approach 

Glioblastoma Multiforme (GBM) is the most common and aggressive primary adult brain tumor, with a median overall survival of 15 months. The peritumoral brain zone (PBZ), the region surrounding the GBM, may be associated with tumor infiltration and aggressiveness and has been recognized as clinically and prognostically important. This study investigates quantitative imaging analysis of the PBZ and its impact on survival in GBM using deep learning (DL).

Peritumoral edema is a feature observed on MRI scans of aggressive brain tumors, such as glioblastoma and higher-grade adult diffuse gliomas. The presence of edema indicates the tumor's infiltrative nature and rapid growth, which can disrupt the blood-brain barrier and cause fluid accumulation in the surrounding brain tissue. In contrast, low-grade gliomas do not exhibit significant peritumoral edema due to their less aggressive growth pattern and limited ability to disrupt the blood-brain barrier. 

<p align="center">
  <img src="https://github.com/user-attachments/assets/64893dd2-0a17-4a3d-aa29-0559e6806ab8" alt="Glioblastoma" width="200" height="200">
  <img src="https://github.com/user-attachments/assets/1254b16d-50ab-4e23-a7c7-77060df83db3" alt="High-grade diffuse glioma" width="200" height="200">
  <img src="https://github.com/user-attachments/assets/88c2a23e-38a5-46de-bdae-9414fc74aab2" alt="Low grade glioma" width="200" height="200">
</p>

<p align="center">
  <em>Glioblastoma, High-grade diffuse glioma, Low grade glioma</em>
</p>


We conducted a retrospective study using the BraTS 2021 (1,251 subjects) and BraTS 2020 (235 subjects) datasets, both containing tumor segmentations, with the latter also including overall survival data (median: 370 days; 49% died within one year).

We developed a unified DL-based image reconstruction model to extract features from images. For each patient, we utilized four MRI sequences—T1, T2, T1CE, and FLAIR. For each sequence, we considered three regions of interest (ROIs) that included the tumor, tumor plus 5 mm dilation, and tumor plus 1 cm dilation, with the dilation region commonly used to define the PBZ. This combination resulted in 12 images per patient (4 sequences × 3 ROIs).

<p align="center">
  <img src="https://github.com/user-attachments/assets/2982df21-abc5-4991-aa1e-65a43ce523dd"  width="600" height="200">
  <img src="https://github.com/user-attachments/assets/f49c8e0c-c1b6-4bd4-bc9e-db4b3c9c4200"  width="600" height="200">
  <img src="https://github.com/user-attachments/assets/456eb383-5c51-46ce-afae-8307353167f1"  width="600" height="200">
</p>

<p align="center">
  <em>12 input images for a sample patient for training reconstruction model: Tumor, Tumor + 5mm dilation, Tumor + 10mm dilation</em>
</p>

Tumor reconstruction was trained by SwinUnetR on BRATS2021, using a comprehensive loss combining Mean Squared Error (MSE) and Structural Similarity Index (SSIM). The image feature vector from tumor reconstruction was fed into a separate, fully connected network for survival prediction. We trained and evaluated three survival models with the same architectures and patients but varying ROIs. The models were trained and evaluated on the BraTS 2020 dataset with an 80/20 split for training/validation and blinded testing, using the logistic hazard as the loss function. The survival prediction models were evaluated using the time-dependent concordance index (Ctd) and area under the receiver operating characteristic curve (AUC) at one year.

Of 47 patients in the blinded test set, 23 died in the first year of diagnosis (median survival: 387 days). The Ctd for models based on tumor features alone, tumor plus 5 mm dilation, and tumor plus 1 cm dilation were 0.56 [95% CI: 0.43-0.70], 0.63 [95% CI: 0.50-0.74], and 0.59 [95% CI: 0.46-0.71], respectively. The corresponding AUCs were 0.56 [95% CI: 0.39-0.72], 0.63 [95% CI: 0.47-0.79], and 0.58 [95% CI: 0.42-0.75] (no significant differences among the three models).

While no significant differences were observed among the three ROIs, the results suggest that incorporating analysis of the PBZ into DL models can enhance prognostic performance for GBM, with the 5 mm surrounding tissue outperforming the 1 cm tissue. Further independent validation of these findings should be performed using additional external GBM patient datasets. As tumor segmentation is crucial for this study, future work should investigate the impact of minor variations in tumor segmentation on model performance.

## Folders:
The code starting from the Tumor Reconstruction folder is where tumor reconstruction models were trained. The best model for tumor reconstruction is saved here. Then, in the Image Feature Extraction folder, the features of the images were extracted. Also, the features for 3 ROIs are saved in this folder. In the Survival Analysis folder, three survival models were trained to compare 3 ROIs. The three survival models are also saved here.

The requirements for running the files are in the requirements.txt.
