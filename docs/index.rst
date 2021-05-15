=================
Welcome to BASIN!
=================

.. figure:: fair_chart.png
   :height: 180 px
   :width: 180 px
   :scale: 50 %
   :alt: alternate text
   :align: right

   `FAIR Assessment`_
.. _FAIR Assessment: https://fairshake.cloud/project/130/stats/

---------
Objective
---------

In order to assist researchers with quantitative, objective analysis of experiments
involving cell treatment and/or movement, we have developed a suite of applications
under the BASIN Project.

BASIN is a set of R packages that utilize Shiny to provide a user interface
for statistical analysis of two-dimensional confocal microscope images. Users
can upload two images directly or a folder of images with the help of a
user-generated csv file, edit their experimental design, create tables and
graphs for analysis results, and generate a fully-formatted report of their
experiment. Source code for the BASIN applications can be found at our Github
repository at https://github.com/bicbioeng/BASIN.

------------
Publication
------------

=========
Tutorials
=========

---------
Workflow
---------

Here is an abstract illustration of experimental workflow in the BASIN application. Two sources of images and two types of image processing techniques can be used.
First, desired features are extracted from the processed images. Then, statistical analytical tools are used to present the comparable results.

.. image:: figure1.png

Visualized below is the schematic overview of the BASIN workflow. As indicated, the application
is divided into four main modules: input, extraction, analysis and visualization, and reporting.

.. image:: figure2.png

We provide a `notebook`_ on Kaggle that can be used to run the full workflow and visualize all code used in our analysis.

.. _notebook: https://www.kaggle.com/evgeniradichev/basin-workflow


-------
Videos
-------

Video tutorials for all BASIN applications can be found at our YouTube channel (https://www.youtube.com/channel/UCGe9s37qZSgvufQNPnAcyCw). Below you can find
the first video in our BASINlite tutorial series.

.. raw:: html

    <iframe width="560" height="315" src="https://www.youtube.com/embed/139lNDBp_YY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

========
tryBASIN
========

---------
Overview
---------

tryBASIN can be accessed through the following online application: https://bicbioeng.shinyapps.io/tryBASIN/. This
version only takes in 2 images, but the workflow is nearly identical to the complete version and serves as a gentle tutorial to most of BASIN's features.

==========
BASIN-lite
==========

---------
Overview
---------

BASIN-lite is the standard BASIN application. It allows users to upload an arbitrary
amount of images, as well as partition them into as many experimental groups as
they want.

------------
Installation
------------

1. Make sure you have the latest version of R and Rstudio installed on your computer (free and open-source, available online). Rstudio is an IDE for the R programming language, and all successive steps should be ran through the Rstudio terminal.
2. Install the required R and Bioconductor packages::

  `install.packages(c("purrr", "plyr", "shiny", "shinyBS", "shinyjs",
    "shinydashboard", "shinycssloaders", "shinythemes", "shinyWidgets",
    "DT", "stringi", "ggpubr", "tcltk", "autothresholdr"))`
  `if (!requireNamespace("BiocManager", quietly = TRUE))`\
    `install.packages("BiocManager") #installs Bioconductor`\
    `BiocManager::install("EBImage") #installs EBImage`

3. (ONLY FOR BASIN-ML USERS) Install the reticulate, keras, and tensorflow packages in RStudio using::

  `install.packages(c(“reticulate”, “keras”, “tensorflow”))`

4. Test the ability for the packages to connect to the Python environment:
  - Run the following commands in R and check for errors:\
  `library(reticulate)`\
  `env <- conda_list()$name == "basin"`\
  `envPath <- conda_list()[env,]$python`\
  `envPath <- stringi::stri_replace(envPath,"",regex = "python.exe")`\
  `reticulate::use_condaenv(envPath, required=TRUE)`\
  `keras::use_condaenv(envPath, required=TRUE)`\
  `tensorflow::use_condaenv(envPath, required=TRUE)`

  - Restart your R session and run the BASIN app from the server.R or ui.R files inside of the shinyBASIN folder.

========
BASIN-ML
========

---------
Overview
---------

BASIN-ML is a developmental package that utilizes the BASIN-lite workflow but
in addition incorporates Python-based cell segmentation models for improved
cell detection. We have two available models in our developmental version:
Cellpose [1]_ and a Tensorflow-based U-Net model.

.. [1] Stringer, C., Wang, T., Michaelos, M. et al. Cellpose: a generalist algorithm for cellular segmentation. Nat Methods 18, 100–106 (2021). https://doi.org/10.1038/s41592-020-01018-x

------------
Installation
------------

In addition to the R Setup outlined in the BASIN-lite Installation section, the following
setup in Python is required:

~~~~~~~~~~~~~
Python Setup:
~~~~~~~~~~~~~

1. Install Anaconda on your local machine:
  - Quick Setup - install Miniconda using the following link: https://docs.conda.io/en/latest/miniconda.html
  - If any successive steps don’t work, uninstall Miniconda and install Anaconda instead using the following link: https://docs.anaconda.com/anaconda/install/
2. Open the Anaconda terminal (Anaconda Prompt) and switch to the folder containing the “full_environment.yml” file using ` cd path\to\folder\... `
3. Install the BASIN python environment using the command ` conda env create -f full_environment.yml ` - this will take a few minutes
4. Make sure you have the latest version of cellpose by running `pip install cellpose --upgrade`
5. Ensure the installation worked by executing the following commands in the terminal:
  - Activate the environment using ` conda activate basin `
  - Run cellpose using ` python -m cellpose `
  - If the cellpose GUI appears, your installation has been successful
6. Once Python installation is complete, you can always run cellpose by running ` python -m cellpose ` in the Anaconda terminal. Note that any time you open a new Anaconda terminal, you will have to re-run the ` conda activate basin ` command in order to activate your cellpose environment.
