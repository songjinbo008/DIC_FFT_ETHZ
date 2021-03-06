﻿
# Digital Image Correlation using an FFT-approach

#### State of the Art - for 8bit, equal dim, single- and multi-channel images

#### Quantify displacement of features in a series of images over time & retrieve displacement velocities. Output data include CVP 2D-displacement maps, the displacement resultant (magnitude), and displacement vectors.
#### Built-in pre-processing routines:
(1) Wallis Filter: Dynamic Contrast Enhancement of both input images; improves the quality of the FFT correlation significantly and helps to suppress noise.

(2) Sub-Pixel Co-Registration: Aligns both input images on a sub-pixel level; significantly improves the quality of the correlation and the absolute accuracy of the displacement measurement.

#### Built-in post-processing routines:
(1) RSME Threshold Filter: Filters DIC output based on a RMSE threshold.

(2) Mean Filter: Filters DIC output with a algorithmic mean kernel.

(3) Median Filter: Filters DIC output with a median kernel.

(4) Vector Filter: Filters DIC output based on the pixel neighborhood's displacement vector direction & magnitude.

<img src="https://github.com/bickelmps/DIC_FFT_ETHZ/blob/master/Figures/glacier.gif?raw=true">

-----------------------------------

V. T. Bickel & A. Manconi, May 2nd 2018

valentin.bickel@erdw.ethz.ch / andrea.manconi@erdw.ethz.ch

ETH Zurich / MPS Goettingen

##### MIT License - Copyright (c) 2018 Valentin Tertius Bickel & Andrea Manconi
Please cite this routine as:
#### Bickel, V.T.; Manconi, A.; Amann, F. Quantitative Assessment of Digital Image Correlation Methods to Detect and Monitor Surface Displacements of Large Slope Instabilities. Remote Sens. 2018, 10, 865.
http://www.mdpi.com/2072-4292/10/6/865
________________________________________________________________________________________________________

### Required Matlab toolboxes:
- MATLAB R2017a
- Image Processing Toolbox
- (Communication System Toolbox for Mean and Median filter, optional)


### External/integrated functions/algorithms:
- dftregistration.m   by Manuel Guizar-Sicairos, Samuel T. Thurman, and James R. Fienup, "Efficient subpixel image registration algorithms," Opt. Lett. 33, 156-158 (2008).
Parts of their code has been taken from: J.R. Fienup and A.M. Kowalczyk, "Phase retrieval for a complex-valued object by using a low-resolution image," J. Opt. Soc. Am. A 7, 450-458 (1990).
Online: https://de.mathworks.com/matlabcentral/fileexchange/18401-efficient-subpixel-image-registration-by-cross-correlation (Status: May 5th, 2018)
License included in "DIC/dft_registration_license.txt"

- wallis_filter.m,   underlying principle taken from Baltsavias, E. P. "Multiphoto geometrically constrained matching." Doctoral Thesis, ETH Zurich, (1991).


### Hardware requirements:

- Input image size of 30 MB requires at least ~5 GB RAM


## Instructions

1. Clone and unzip DIC_FFT_ETHZ_Repo

2. Place Master and Slave images in the "Input" folder (or copy images from 'Example' folder)

3. Customize setup for Preprocessing, DIC, and Postprocessing in run_pixel_offset.m:

          Inputs ----------------------------------------------------------------------------------
               - master = 'string' (name of master.type); # used for DIC
               - orig_m = 'string' (name of master.type); # used for plotting
               - slave = 'string' (name of slave.type);
               - orig_s = 'string' (name of slave.type);

          Preprocessing (Wallis filter & Co-registration) -----------------------------------------
               - wallis = 0/1  # wallis filter off/on
               - win = int. # window size, even numbers only
               - tarm = int. # target mean
               - tars = int. # target standard deviation
               - b = 0-1 # brightness enforcing constant
               - c = 0-1 # contrast enforcing constant

               - sp = int. # image split
               - co_os = int. # image oversampling

          DIC -------------------------------------------------------------------------------------
               - wi = 2^n, n = int. # window size in [pix]
               - os = int. # FFT oversampling factor
               - pix = float./int. # Ground sampling distance of used input imagery in [m]

          Postprocessing (RMSE, Mean, Vector, Median filter) --------------------------------------
               - filter = 1-4 # filter type, 1= RMSE threshold-, 2= Mean-, 3= Vector-, 4= Median filter

               - thr = 0-1 # threshold, 1 = no mask

               - mfws = [int. int.] # dimensions of mean filter window in [pix]
               - cut = int. # cut off value, OPTIONAL in [pix]
 
               - magcap = wi/int. or int. # tolerance-diff, values greater as value are cut, in [pix]
               - xcap = wi/int. or int.
               - ycap = wi/int. or int.

               - med = [int. int.] # dimensions of median filter window [pixel]

           Additional settings --------------------------------------------------------------------
               - scalax = [int. int.] # min and max values for the X displacement colorscale, in [m]
               - scalay = [int. int.] # min and max values for the Y displacement colorscale, in [m]

               - coppia = 'string' # name of output ascii file

               - skip_x = wi/int. # search window skip in X
               - skip_y = wi/int. # search window skip in Y

- Execute run_pixel_offset.m

- Collect displacement matrix ascii from "Output" folder

### Possible results

##### Advancing glacier, one image per day:

<img src="https://github.com/bickelmps/DIC_FFT_ETHZ/blob/master/Figures/glacier.gif?raw=true">

------------------
##### MIT License - Copyright (c) 2018 Valentin Tertius Bickel & Andrea Manconi
