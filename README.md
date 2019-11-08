
# Standard Operating Procedure: IF_particles_analysis_macro

This is the SOP for the IF_particles_analysis_macro created by Arya Akkus, Frederique Larroquette and
Eddie Cai for the Fon Lab at the Montreal Neurological Institute of McGill University.

## User Guide

### Purpose and Output

This macro in Python is designed to perform particle and colocalization analysis on 3 channeled RGB
images. It is meant to be run on FIJI (ImageJ) platform. The output of the analysis is saved to a .csv file in
the output directory chosen by the user.

This macro takes images from the input folder and its subfolders, then it detects distinct particles in
each channel (regions of interests – ROI) and measures the tissue area, number of particles and cells,
total area of particles and cells, staining ratio and colocalization percentage.

.

### Manual

#### Getting Started
To be able to run this macro, you should have FIJI (ImageJ) installed on your computer. Once you open
FIJI, select File>Open> or simply drag the macro to FIJI menu. Then you can run the macro from the
editor. Before analyzing, the user is asked to choose the threshold mode, input and output directories
as well as Min and Max ROIs. For further information see following sections: Thresholds and Threshold
mode _Thresholds and Threshold mode_ and Particle Analysis and ROIs

#### Thresholds and Threshold mode
Thresholding is a technique for dividing an image into two (or more) classes of pixels, which are typically
called "foreground" and "background". This will help separate the specific signal in each channel from
the background. If the threshold mode is NOT enabled, the user must define default thresholds for each
channel beforehand.


If the threshold mode is enabled, user can adjust and change the threshold after seeing the ROIs until a
correct value is found. In the threshold mode, there is a loop where the user can choose the threshold
as many times they want and see the ROIs until they decide to move on to analysis.

#### Particle Analysis
_Tissue Area and Intensity_
Before proceeding to particle detection and analysis, this macro measures the tissue area. The total
tissue area value will be used in the output to normalize the number of particles detected or total
staining area to the tissue area observed. Then, each original channel’s intensity is also calculated. These
values are added to the output table.

_Particle Analysis and ROIs_
In this macro, maximum and minimum size of ROIs detected are set before the particle analysis. This
means that the user have to choose their minimum and maximum ROI sizes at the beginning of the
macro in the ‘Other Thresholds’ window.Hence, it is important to have an idea of your desired particle
size interval for each channel before running the macro.

Once the user has chosen the correct ROIs size exclusion parameters and thresholding values, image
processor finds all the ROIs. Then, it counts the number of particles, total area of particles, number of
cells and total area of cells. A cell is assumed to be a particle with size between 100 and 3000 for this
macro. However, it is possible to change it. For this macro, the cell analysis is only output for the red
channel, similarly, it is also very possible to extend it to other channels.

#### Colocalization
This macro focuses on the colocalization between particles detected in the green and red channels. It
simply measures the ratio of common particle area and the channels (green and red) particle area. So
there are two colocalization ratio at the end: red /green colocalization percentage and green/red
colocalization percentage. For visualization, the new composite image is created and saved to output
directory with the name “coloc_<yourimagename>”.


_More details on Colocalization_
For measuring colocalization percentage, we work on a duplicate image and get its green and red
channels. Then, both channels are thresholded (user’s chosen threshold taken here) and converted to a
mask and measured for their integrated density. Finally, both images are multiplied measured for their
integrated density (coloc. intensity) again.

The red green colocalization percentage is equal to (coloc. density/red density)*100.

The green red colocalization percentage is equal to (coloc. density/green density)*100.

#### Output file
Output file is basically a csv table named “output”. It has information about:


- Image name
- Tissue area
- Big area (total image area)
- Used thresholds and ROIs
- Cell Areas and Cell Count
- Particle Areas and ROI count
- Ratio of Areas and Counts/ Tissue Area
- Colocalization percentages


## Questions and answers

_What does it mean if I get “NA” for my ROI count or in the colocalization values?_

It means that the macro was not able to find any particles in that channel or process your image. Try
running the macro with new ROI and threshold settings.

_The macro is not counting some of my particles even though I highlight them when choosing a
threshold, what can I do?_

It is normal for the macro to not count all your particles; however, you can try to change your ROI
settings.


