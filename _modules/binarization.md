---
title: Thresholding
layout: module
tags: ["segmentation", "binarization"]
prerequisites:
  - "[Image segmentation](../segmentation)"
  - "[Basic properties of images and pixels](../pixels)"
  - "[Data types](../datatypes)"
objectives:
  - "Describe the relationship between an intensity image and a derived binary image"
  - "Apply a threshold to segment an image into foreground and background regions"
motivation: |
  One strategy to detect objects or specific regions in images is to first distinguish so-called background pixels,
  which do not contain objects or interesting regions from foreground pixels, which mark the areas of interest.
  This process is called **two class semantic segmentation** and is often referred to as **image binarization**.
  The foreground regions can then be further processed, e.g. to detect objects or perform intensity measurements.

concept_map: >
  graph TD
    I("Image") --> T("Threshold")
    T --> BI("Binary image / Binary mask")
    BI --- BG("Background pixels (false, 0)")
    BI --- FG("Foreground pixels (true, 1, 255)")

figure: /figures/binarization.png
figure_legend: Image before and after binarization

activity_preface: |
  - Open the image [xy_8bit__two_cells.tif](https://github.com/NEUBIAS/training-resources/raw/master/image_data/xy_8bit__two_cells.tif)
  - Visualise the image and inspect its data type and value content
  - Threshold the image
    - Identify a threshold value that segments both cells
    - Apply that threshold, generating a binary image
    - Visualise the binary image and inspect its data type and value content
   - Threshold again, now choosing a threshold such that only the brighter cell is segmented

activities:
  - ["ImageJ GUI", "binarization/activities/binarization_imagejgui.md", "markdown"]
  - ["ImageJ Macro", "binarization/activities/binarization_imagejmacro.ijm", "java"]
  - ["skimage napari", "binarization/activities/binarization_skimage_napari.py", "python"]
  - ["ImageJ Jython", "binarization/activities/binarization_jython.py", "python"]
  - ["MATLAB", "binarization/activities/binarization_matlab.m", "matlab"]
  - ["KNIME", "binarization/activities/binarization_knime.md", "markdown"]

exercise_preface: |
  Perform one of the following exercises.

exercises:
  - ["ImageJ GUI", "binarization/exercises/binarization_imagejgui.md"]
  - ["ImageJ Macro", "binarization/exercises/binarization_imagejmacro.md"]
  - ["ImageJ Jython", "binarization/exercises/binarization_jython.md"]

assessment: >

  ### Fill in the blanks

    - Pixels in a binary image can have maximally ___ different values.
    - If the threshold is larger than the maximal pixel value in the intensity image, all pixels in the binary image have a value of ___.

    > ## Solution
    >   - Pixels in a binary image can have maximally **2** different values.
    >   - If the threshold is larger than the maximal pixel value in the intensity image,
    > all pixels in the binary image have a value of **0**.
    {: .solution}

  ### True or False
    - There is only one correct threshold value in order to convert an intensity image into a binary image.
    - Binary images are always unsigned 8-bit where the foreground is 255.

    > ## Solution
    >   - There is only one correct threshold value in order to convert an intensity image into a binary image. **False**
    >   -  Binary images are always unsigned 8-bit where the foreground is 255. **False**
    {: .solution}

learn_next:
  - "[Automatic threshold for binarization](../auto_threshold)"
  - "[Finding objects in a binary image](../connected_components)"

external_links:
  - "[Wikipedia: Binary image](https://en.wikipedia.org/wiki/Binary_image)"

---
#### Image thresholding
A common algorithm for binarization is thresholding. A threshold value `t` is chosen, either manually or automatically,
and all pixels with intensities below `t` are set to 0, whereas pixels with intensities `>= t` are set to the value for the foreground.
Depending on the software the foreground value can be different (e.g. 1 in MATLAB or 255 in ImageJ). At any pixel `(x,y)`:

`p_im(x,y) < t` `->` `p_bin(x,y) = 0`

`p_im(x,y) >= t` `->` `p_bin(x,y) = 1`

where, p_im and p_bin are the intensity and binary images respectively.

It is also possible to define an interval of threshold values, i.e. a lower and upper threshold value. Pixels with intensity values
within this interval belong to the foreground and vice versa.
