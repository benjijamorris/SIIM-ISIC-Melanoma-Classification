This project is a part of the Kaggle competition SIIM-ISIC Melanoma Classification. I was inspired by the paper ["Feature extraction from dermoscopy images for melanoma diagnosis"
by Sharmin Majumder and Muhammad Ahsan Ullah](https://link.springer.com/article/10.1007/s42452-019-0786-8), but thought their methods could be improved upon. This paper describes the 
extraction of 8 features based on "ABCD Diagnosis", which examines the asymmetry, border irregularity, color variegation, and diameter of skin lesions to determine whether they are
benign or malignant. 

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
