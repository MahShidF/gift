3	GETTING STARTED WITH GIFT

The source code and the example subjects fMRI data need to be installed. These are available on project web page (http://mialab.mrn.org/software/gift/index.html). Also available on this web page are posters on GIFT at the conferences like Society of Biological Psychiatry and Human Brain Mapping. The mailing list is: icatb-discuss@lists.sourceforge.net. Please send comments and bug reports to: vcalhoun@unm.edu or srachakonda@mrn.org.

3.1	INSTALLING GIFT

Unzip the file GroupICATv4.0b.zip and copy the folder GroupICATv4.0b onto your local machine. Add GIFT directories to the MATLAB search path or run the gift.m file to automatically add GIFT directories. The GIFT path by default will be set at the bottom of the MATLAB path. You can create gift_startup.m (Appendix 6.7) file for setting the path according to your needs. After the GIFT path is set, GIFT toolbox (Figure 3.2) opens in a new figure window. There is also an option to run group ICA using a batch script (Section 3.14.1). Batch script is very useful for running large data-sets.

Note:
•	GIFT toolbox can also be invoked by using the statement groupica and clicking on the fMRI button (Figure 3.1) or by typing groupica fmri at the MATLAB command window.
•	If you have downloaded an older version of GIFT, make sure that there is only one version on path at a time.
3.2	INSTALLING EXAMPLE SUBJECTS

Download the example_subjects.zip file and unzip into an appropriate directory. Included in this file are three subjects pre-processed fMRI data from a visuomotor task (See (V.D. Calhoun, T. Adali, G.D. Pearlson, and J.J. Pekar, 2001) for a complete description of the task). Whole brain and single slice data (for rapid testing) are provided. More information on the task the subject performed while in the scanner is given in the Appendix 6.1. Each example subject also contains a functional data-set, which contains only one brain slice. If you are having problems with this toolbox you may test this with a smaller data-set.

3.3	HTML HELP MANUAL

When you click Help button (Figure 3.2), HTML help manual is opened in the default web browser. ”GIFT-help” menu is plotted on some figures which will directly open a particular topic.
3.4	NEW FEATURES

1)	A subject outlier detection tool is now added as a “Generate Mask” utility in the GIFT toolbox. An average mask is generated and subjects below a certain correlation threshold are excluded from the analysis. At the end of the mask generation, a GIFT batch file is created which can be used to run the group ICA.
2)	An option is now provided to generate results summary in the Mancovan toolbox. This tool can be accessed using “display” button in the Mancovan toolbox. Univariate results are plotted in a separate figure for each significant covariate and a connectogram display (Rashid, B., et al. (2014), “Dynamic connectivity states estimated from resting fMRI Identify differences among Schizophrenia, bipolar disorder, and healthy control subjects”, Frontiers in human neuroscience) is used to show the FNC plots.
3)	We now provide an option in the Mancovan toolbox to run univariate tests using the selected covariates bypassing the multivariate tests. This tool can be accessed using “Run analysis” button in the Mancovan toolbox.
4)	The “Group networks” tool is renamed to a more general “network summary” in the GIFT display tools. The network summary display uses the component network information and optional FNC information to generate composite orthogonal views (Damaraju, E., et al. (2014), “Dynamic functional connectivity analysis reveals transient states of dysconnectivity in schizophrenia", NeuroImage), composite rendered surfaces of brain, stacked orthogonal slices, FNC matrix viewer and connectogram FNC plot. 
5)	We now provide an option to use the temporal design matrix information in the “Results Summary” button to compute R2 and one sample t-test on beta weights in the GIFT toolbox. This tool can also be accessed as temporal sorting under “Utilities” drop down box. 
6)	The stand-alone image viewer tool is now enabled to select multiple component images which can be plotted independently or in a composite plot (montage, render or orthogonal slices). 
7)	An option is now provided to export results to PDF or HTML file in the component viewer display tool.
8)	MOO-ICAR algorithm name is changed to GIG-ICA.
3.5	GIFT UPDATES

We post the updates to the software that contain new features or any bug fixes in the updates section of the project web page (http://mialab.mrn.org/software/gift/index.html). Please see Updates_Readme.txt in updates webpage for more details.

3.6	THINGS TO DO BEFORE CONFIGURING THE ANALYSIS

3.6.1	Compiling MEX files

•	SPM MEX binaries - We use SPM8 volume functions to read and write image data. 
•	Group ICA MEX binaries - C-MEX files are provided for computing the eigen values of a symmetric matrix. The compiled MEX binaries are used only when you select packed storage scheme for computing covariance matrix. 
•	GLASSO - FORTRAN MEX file (GLASSO, 2007) is provided for estimating a sparse inverse covariance matrix using a L1 penalty when using temporal dFNC toolbox.

To compile the MEX source code, type icatb_compile_mex_files at the MATLAB command prompt. Please see below to copy the SPM MEX binaries manually if the source code fails to compile: 

•	Copy SPM8 MEX binaries like spm_bwlabel*, spm_existfile*, spm_sample_vol*, spm_slice_vol* to the directory icatb\icatb_spm8_files and prefix them with icatb_. 
•	Copy SPM8 MEX binaries like spm8\@file_array\private\* to icatb_spm8_files\@icatb_file_array\private and prefix them with icatb_.

Note: * refers to the MEX file extension on your Operating System. Type mexext on the MATLAB command window to get the MEX file extension on the Operating System you are working on.

3.6.2	Memory Requirements

Since PCA and ICA are multivariate approaches unlike General Linear Model, there are some memory requirements to do the group ICA/IVA analysis. We added a script icatb_mem_ica.m which will give a close estimate of RAM required to do the group ICA/IVA analysis. Please enter the parameters like number of voxels, time points, subjects, sessions, components and reduction steps in the input parameters section of the script and run the script to get an approximate amount of RAM required in gigabytes.

3.6.3	Organizing data

Organizing data reduces the amount of selection. GIFT has two ways to enter the data for GUI and four ways to enter the data using the batch script.
•	First method requires the data to be in one root folder with a common file pattern (like sw*.img) for all subjects and sessions. Each subject folder can have session folders and the number of session folders with the matching file pattern should be the same over subjects.
•	Second method does not require the data to be in one root folder or have a common file pattern but the selection process through GUI can be tedious for large data-sets and therefore batch script (Section 3.14.1) is recommended.
•	Third method uses regular expressions to get the subject and session directories. This option is useful in matching directories that have nested paths. However, this option still requires a common file pattern for all the subjects. Please see Section 3.14.1 for more information.
•	Option is provided to paste the file names in the fourth method (Section 3.14.1).

3.6.4	Defaults

Defaults are stored in icatb_defaults.m file. You could also change these defaults from the GUI (Appendix 6.4). Configure the specified defaults before using setup ICA as needed.
•	FUNCTIONAL_DATA_FILTER - Set the variable to *.nii if you would like to write components as 4D Nifti files.
•	ZIP_IMAGE_FILES - By default, components will be compressed in zip format. If you want to turn off the compression, set variable value to ’no’. Uncompressed data is faster to load in memory.
•	SPM_STATS_WRITE_TAL - If you plan to do one sample t-tests on components over subjects using SPM5, SPM8 or SPM12, set variable value to 1.
•	CENTER_IMAGES - By default, subject component spatial maps after the scaling components step is centered based on the skewness of the distribution of the mean component maps. If you want to turn off this option, set the variable to 0.
•	MAX_AVAILABLE_RAM - This variable is used during the run analysis step and best PCA settings for each option (maximize performance or less memory usage) are used. Set this variable value to the maximum available RAM.
•	WRITE_ANALYSIS_STEPS_IN_DIRS - Organize analysis results in directories. When this variable is set to 1, analysis steps are saved in separate directories. The directories naming are as follows:
o	Data reduction files are stored in *_data_reduction_files
o	ICA files are stored in *_ica_files
o	Back-reconstruction files are stored in *_back_reconstruction_files
o	Scaled components are stored in *_scaling_components_files
o	Group stats are stored in *_group_stats_files
•	CONSERVE_DISK_SPACE - Set the variable value as needed. The following are the options:
o	0 - Analysis runs faster with this option. All the intermediate analysis files are written.
o	1 - Only the required analysis files are written which will be used during the post-processing (display, components sorting, remove components, etc).
o	2 - All the intermediate analysis files (Data reduction, back-reconstruction, scaled components MAT files) are cleaned up after the end of the group stats step. Only the basic post-processing steps like display and components sorting will work with this option.
•	DEFAULT_MASK_OPTION - By default, first file of each subject is used to generate the default mask. If you want to use all files, set the variable value to ‘all_files’.
•	REMOVE_CONSTANT_VOXELS - Constant voxels are removed in the fMRI data when this variable is set to 1.
•	DEFAULT_MASK_SBM_MULTIPLIER - Default mask multiplier in SBM. Defaults is 1% of mean i.e., voxels greater than or equal to 1% of mean will be used.
•	EXPERIMENTAL_TR – Specify experimental TR in seconds. This information is used when computing spectra, filtering and despiking.
•	USE_UNIFORM_COLOR_COMPOSITE – By default, composite plots in the network summary and image viewer are shown as intensity maps. You have the option to use uniform colors when you set a value of 1 in the  “USE_UNIFORM_COLOR_COMPOSITE” variable.
•	CONNECTOGRAM_SM_WIDTH – By default, the size of the connectogram spatial maps is automatically determined. If the thumbnails are too small, you could set a specified value like 0.06.

3.7	SPATIAL TEMPLATES

The following example spatial templates are provided in icatb\icatb_templates:
•	ref_right_visuomotor.nii - Mask containing the right visual regions.
•	ref_left_visuomotor.nii - Mask containing the left visual regions.
•	ref_default_mode.nii - Mask containing the default mode network regions. Please see (A. R. Franco, A. Pritchard, V. D. Calhoun, A. R Mayer, 2009) for more information.
•	*DMN_ICA_REST*.nii - This mask was created from a data-set of 42 subjects. During a fMRI scan, subjects were asked to relax and passively stare at a fixation cross. A pooled group ICA was performed and the default mode component network was selected to create this mask. We provide templates like rDMN_ICA_REST_3x3x3.nii and rDMN_ICA_REST_3x3x4.nii in the GIFT. Please see (A. R. Franco, A. Pritchard, V. D. Calhoun, A. R Mayer, 2009) for more information.
•	*DMN_MASK.WFU*.nii - This mask was constructed using the Wake Forest Pick atlas toolbox. A binary mask was created by selecting the anatomical regions that have been most commonly reported to comprise the default mode network. The labels from the Wake Forest Atlas that constituted this mask included posterior cingulate (BAs 23/31), inferior and superior parietal lobes (BAs 7/39/40), superior frontal gyrus (BAs 8/9/10), and anterior cingulate cortex (BAs 11/32). In addition, a larger weight was given to the anterior and posterior cingulate cortex, which are believed to be the central nodes of the default mode network. A higher correlation was observed when giving a higher weight to these two central nodes. We provide templates like rDMN_MASK.WFU.3x3x3.nii and rDMN_MASK.WFU.3x3x4.nii in the GIFT. Please see (A. R. Franco, A. Pritchard, V. D. Calhoun, A. R Mayer, 2009) for more information.


3.8	MENUS

Menus are provided as a shortcut to the user-interface controls in the GIFT toolbox (Figure 3.2). The function of each menu is given below:

•	File 
o	New - Setup ICA GUI will open after you have selected the output directory.
o	Open - Setup ICA GUI will open showing the values for the parameters after you have selected the subject file that has suffix Subject.mat.
o	Close - Closes the GIFT Toolbox and the figures generated by the GIFT.
•	View 
o	Analysis Info - Analysis information will be shown after you have selected the parameter file that has suffix ica_parameter_info.mat.
•	Tools
o	Run Analysis - Analysis will be run after you have selected the parameter file.
o	Display GUI - Display GUI will be opened after you have selected the parameter file.
o	Utilities 
	Generate mask – Please see Section 3.12.1.
	Batch – This option runs multiple batch analyses. More information on input file required for batch analysis is provided in Section 3.14.1.
	Remove component (s) - Removes a component or components from the data after you have selected the parameter file. Please see Section 3.12.1 for more information.
	Ascii_to_spm.mat - Creates SPM.mat from ascii file (containing regressor time courses) that is needed during temporal sorting. Please see Section 3.12.9 for more information.
	Event Average - Event average is calculated for the ICA time courses. Please see Section 3.12.10 for more information.
	Calculate Stats - Mean, standard deviation, t-maps are calculated for components over sessions, subjects or subjects and sessions.
	Spectral Group Compare - This utility is used to compare the power spectra between groups. Please see Section 3.12.12 for more information. 
	Temporal Sorting – Stand-alone tool is now provided to do multiple linear regression on ICA timecourses and model timecourses (Section 3.12.3). 
	Stats on beta weights - This utility is used to do one sample t-test or two sample t-test on the component images. Please see Section 3.12.3 for more information.
	SPM Stats - Group statistics are computed on individual subject component maps using SPM toolbox. We integrated option to do t-tests using SPM in the GIFT toolbox.
	Spatial-temporal regression - Given a set of GLM or ICA spatial maps and the original data of the subjects, you could use this utility to back reconstruct subject components (Section 3.12.6).
	Write talairach table - Talairach daemon client is used to generate the talairach tables for the selected image. Please see Section 3.12.7 for more information.
	Single trial amplitudes - We provide the option for calculating single trial amplitudes (Section 3.12.13) in GIFT.
	Z-shift - Please see Section 3.12.14 for more information.
	Percent variance – Variance explained by the components in the data is determined. Please see Section 3.12.15 for more information.
o	Display Tools 
	Image viewer - Options to do image rendering and displaying images as a montage or orthogonal slices are provided. We now provide options to do composite plots if multiple images are selected.
	Component explorer - Standalone tool to display component maps and timecourses.
	Composite viewer - Multiple components could be displayed as a composite map.
	Orthogonal viewer - Component timecourse and orthogonal slices of components are shown. Also, BOLD timecourse is plotted for the selected voxel.
	Component viewer - Mean and standard error mean of spectra is shown. Also orthogonal slices are plotted at the maximum voxel.
	Network summary – This tool uses network information and corresponding components to generate composite orthogonal plots, rendered surface plots, stacked orthogonal slices, FNC matrix viewer and connectogram plots. 
o	Toolboxes 
	ICASSO – ICA is run several times and best stable run estimates are used to reconstruct individual subject components.
	Mancovan - Mancovan toolbox works on the ICA output. Multivariate stats is used to determine the significant covariates which will be used later in the univariate tests. Please see 3.13.2 for more information. 
	Temporal dFNC - Dynamic FNC (dFNC) toolbox is used to study functional network connectivity dynamics. dFNC toolbox is based on paper (E. Allen, E. Damaraju, S. M. Plis, E. Erhardt, T. Eichele, and V. D.Calhoun, 2012). Please see 3.14.5 for using the toolbox.
	Spatial dFNC – Dynamic FNC is computed in space using the mutual information between component maps. Please see Section 3.13.4 for more information.
o	Results summary - Results are summarized using HTML or PDF report. Report includes ICASSO plots, components (maps, timecourses and spectra), statistics on beta weights obtained from temporal sorting, kurtosis values of components, FNC correlations and FNC values of spatial maps. To get accurate values for spectra, you need to set EXPERIMENTAL_TR in icatb_defaults.m for your experiment before doing group ICA.

 

Figure 3.1: Group ICA/IVA Toolbox

 

Figure 3.2: GIFT Toolbox
