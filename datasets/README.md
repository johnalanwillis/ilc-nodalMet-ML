
# Digital Pathology Approaches to Nodal Metastasis in Breast Cancer

## Table Of Contents
* [Breast Cancer and its Subtypes] (https://github.com/johnalanwillis/ilc-nodalMet-ML/tree/main/clinical#breast-cancer-and-its-subtypes)
* [Digital Pathology and ILC] (https://github.com/johnalanwillis/ilc-nodalMet-ML/tree/main/clinical#digital-pathology-and-invasive-lobular-carcinoma)
* [Project Organization and Navigation] (https://github.com/johnalanwillis/ilc-nodalMet-ML/tree/main/clinical#project-organization-and-navigation)

## Overview

As computation permeates more and more of medicine, the scale of problems and the complexity of the approaches necessary to produce safe, clinically useful technology increases rapidly. Algorithms heralded for their utility and innovation not long ago are only small pieces of xxx. 

Digital Pathology, the use of digitized "whole slide images" with computational methods to enhance to productivity and accuracy of pathologists, is a field that integrates diverse expertise in medicine, computer science and data science to extract the most utility from physical slides as possible.

A full-stack digital pathology system needs to address the storing and serving massive WSI, coordinating sample and patient identifiers, identifying regions of interest, providing diagnostic decision support, and providing a robust set of explainability tools to ensure that any actions taken by the machine with or without the input of the operator are appropriate. 

## Digital Pathology and Invasive Lobular Carcinoma

Detecting lymph node metastases from the "invasive lobular carcinoma" subtype of breast cancer is an ideal use case for a mature digital pathology stack. Identifying lymph nodes metastasis from breast cancer affects tumor staging, which can affect both the same-day actions of the surgeon and the later decision to pursue a particular course of treatment. Failure to identify lymph node metastases may require costly and painful additional surgery, and may result in a treatment delay with dire consequences. Overidentification of nodal metastasis is also harmful however, as the resection of a contaminated node bed may lead to painful chronic side-effects like lymphedema in a patient who may have otherwise been cured through surgery alone. 

The possibility of misdiagnosis of ILC nodal metastasis is high due to the similar morphology of specifically ILC tumor epithelium and the resident immune cells of the lymph node. Both cell types can appear as small, round groups of cells with well defined nuclei. ILC tumor cells lack much of the structural abnormalities that make identification of nodal metastases from the more common "invasive ductal carcinoma" subtype  much easier to do. Intra-operative diagnoses, the sort that would be used to guide decision-making regarding the need for lymph node bed resection, is performed on rapidly fixed and stained sections of flash frozen tissue. These "frozen sections" can be very high quality, but they can also lack the detail and resolution of the slowly prepared formalin-fixed and paraffin-embeded slides used to provide final diagnoses. In trying to detect subtle differences between otherwise similar-appearing cell types, the sometimes poor quality of ILC lymph node frozen sections can contribute to misdiagnosis, particularly when exacerbated by clinician fatigue. 

## Project Organization and Navigation

This project intends to prototype an analysis pipeline that takes WSI as an input and classifies a slide as positive or negative for the presence of tumor metastasis. The project is divided into 5 components, with each component consisting of relevant lit review and an ipython notebook integrating methods from the relevant literature into the prototype pipeline.

### Navigation
* [The Clinical Problem and Lit Review] (#xxx)
* [Datasets Employed] (#xxx)
* [Cloud Computing Approaches] (#xxx)
* [Whole Slide Imaging] (#xxx)
* [Image Segmentation] (#xxx)
* [classification] (#xxx)
* [Interpretability and Explainability] (#xxx)
* [Summary of Results and the Mature Pipeline] (#xxx)


