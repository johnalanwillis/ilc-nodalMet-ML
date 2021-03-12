
# Digital Pathology Approaches to Nodal Metastasis in Breast Cancer

## Table Of Contents
* [Section Overview](#section-overview)
* [Elements of image preprocessing in Digital Pathology](#elements-of-image-preprocessing-in-digital-pathology)
* [Project Organization and Navigation](#project-organization-and-navigation)

## Section Overview
While not always applicable in sandbox educational projects, image acquisition and preprocessing are arguably the most important steps in actually generating insight from a dataset  
Optimal data extraction requires that the recorded data reflect the reality being measured, pixel intensity reflecting stain intensity in a pathology image  
This requires accounting for errors and artefacts introduced by the particularities of the particular image acquisition setup

Steps that attempt to compensate for the optics of the microscope are numerous
Light correction compensates for differences in illumination resulting from the non-uniform intensity of light provided by the source across the slide plane
Deconvolution attempts to improve the resultion of images by correcting for the slightly differing phases of incident light from different points in the slide plane

Steps that improve the utility of an image once acquired and its data is corrected to compensate for acquisition-related error
Cropping can improve the signal to noise in an image by increasing the % of the total image containing your features of interest. This is also useful for reducing resource costs
Inverting can
filtering through application of convolutional kernels creates a wealth of information about images. Filters can reduce noise, sharpen edges, and more
Gamma correction and Brightening can enhance the separation of features of interest
Color Correction and Normalization can enhance the definition of features and the comparability of elements across a dataset

## Elements of image preprocessing in Digital Pathology
### Light Correction
### Deconvolution

### Cropping
### Inverting
### Filtering
### Gamma Correction and Brightening
### Color Correction and Normalization
