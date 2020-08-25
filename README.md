This project is a part of the Kaggle competition SIIM-ISIC Melanoma Classification. I was inspired by the paper ["Feature extraction from dermoscopy images for melanoma diagnosis"by Sharmin Majumder and Muhammad Ahsan Ullah](https://link.springer.com/article/10.1007/s42452-019-0786-8), but thought their methods could be improved upon. This paper describes the extraction of 8 features based on "ABCD Diagnosis", which examines the asymmetry, border irregularity, color variegation, and diameter of skin lesions to determine whether they arebenign or malignant. 

## Paper Issues
1. Doesn't include demographic information/lesion location
2. Doesn't account for secondary "satellite lesions" around a primary lesion
3. Segmentation can be fooled by poor foreground/background separation
4. RGB thresholding approach ignores 10-100% of pixels in lesion images, can be fooled by different lighting
5. Small training/test set could overrepresent diagnostic capabilities

## Modifications
1. Inclusion of demographic information and lesion information
2. Calculcation of 8 ABCD features for each lesion accounting for >10% of total lesion area in an image
3. [BCDU-net segmentation](https://github.com/rezazad68/BCDU-Net) yields improved segmentation
4. Channel-wise pixel value distribution approach for color features
5. 4.67x larger training set, 11.7x larger validation set

## Results
![All Loss](/allloss.png)
![Most Loss](/mostloss.png)

While the model described in the paper and my modifications to that model both showed improvements in loss across epochs, the loss converges to a much lower value with my modifications versus the original paper. Further, the modified model seems adequately fit as shown by the small difference between training and validation loss. Early stopping was used during training with a patience of 25 epochs, resulting in the original model stopping training at 25 epochs after failing to improve.

![ROC-AUC Score](/allauc.png)

The area under the receiver operating characteristics curve (ROC-AUC score) was used as the performance metric in this competition. This ROC curve plots the true positive rate versus the false positive rate at various thresholds for models that output a probabilistic prediction, and the area under this curve corresponds to the probability that the model can distinguish between two classes. This metric is more indicative of a model's ability than a metric like accuracy when the problem has a high class imbalance. The modified model significantly outperformed the original paper with regards to the ROC-AUC score, indicating that it was better able to distinguish between benign and malignant melanomas. 

