# Useful datasets for Digital pathology exploration of breast cancer

## Table Of Contents
* [Breast Cancer and its Subtypes] (https://github.com/johnalanwillis/ilc-nodalMet-ML/tree/main/clinical#breast-cancer-and-its-subtypes)
* [Digital Pathology and ILC] (https://github.com/johnalanwillis/ilc-nodalMet-ML/tree/main/clinical#digital-pathology-and-invasive-lobular-carcinoma)
* [Project Organization and Navigation] (https://github.com/johnalanwillis/ilc-nodalMet-ML/tree/main/clinical#project-organization-and-navigation)

## Overview
### Kaggle BC patches
://www.kaggle.com/paultimothymooney/breast-histopathology-images
`Context
Invasive Ductal Carcinoma (IDC) is the most common subtype of all breast cancers. To assign an aggressiveness grade to a whole mount sample, pathologists typically focus on the regions which contain the IDC. As a result, one of the common pre-processing steps for automatic aggressiveness grading is to delineate the exact regions of IDC inside of a whole mount slide.

Content
The original dataset consisted of 162 whole mount slide images of Breast Cancer (BCa) specimens scanned at 40x. From that, 277,524 patches of size 50 x 50 were extracted (198,738 IDC negative and 78,786 IDC positive). Each patch’s file name is of the format: uxXyYclassC.png — > example 10253idx5x1351y1101class0.png . Where u is the patient ID (10253idx5), X is the x-coordinate of where this patch was cropped from, Y is the y-coordinate of where this patch was cropped from, and C indicates the class where 0 is non-IDC and 1 is IDC.

Acknowledgements
The original files are located here: http://gleason.case.edu/webdata/jpi-dl-tutorial/IDC_regular_ps50_idx5.zip
Citation: https://www.ncbi.nlm.nih.gov/pubmed/27563488 and http://spie.org/Publications/Proceedings/Paper/10.1117/12.2043872

Inspiration
Breast cancer is the most common form of cancer in women, and invasive ductal carcinoma (IDC) is the most common form of breast cancer. Accurately identifying and categorizing breast cancer subtypes is an important clinical task, and automated methods can be used to save time and reduce error.`


### HISTOBREAST Dataset 
https://www.nature.com/articles/s41597-020-0500-0
`The HISTOBREAST31 collection is comprised of BM images acquired on a tissue fragment from a patient diagnosed with moderately differentiated (G2) invasive breast cancer of no special type (NST) with extensive foci of high grade ductal carcinoma in situ (DCIS)33. More specifically, HISTOBREAST consist of four Sets of NITs and two Sets of HSIMs, with each Set hosting multiple Subsets, which are further structured in Versions. The four NITs Sets are comprised of a total number of 1216 of image tiles, summing up ~35 GB. All image tiles have been recorded at a digital resolution of 3648 × 2736 pixels and are provided in Tagged Image File Format (TIFF). The two HSIMs Sets are comprised of a total number of 578 HSIMs, summing up 163 GB. All six HISTOBREAST Sets are accompanied by ReadMe.txt files describing their structure, which we also briefly detail next.`
