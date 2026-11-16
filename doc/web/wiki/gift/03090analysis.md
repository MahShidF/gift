3.9	ANALYSIS FUNCTIONS

3.9.1	Setup ICA  Analysis

When you click Setup ICA button (Figure 3.2), Setup ICA GUI (Figure 3.3) will open after you have selected the output directory for the analysis. Setup ICA is the GUI used for entering parameters required for group ICA. Figure 3.3 shows the main user interface controls. Some of the parameters are plotted in ”Setup ICA-Defaults” menu (Figure 3.4). It is recommended that after entering the parameters in the main figure window parameters plotted in menu be changed. The parameters are explained below:

Main User Interface Controls
•	Enter Name (Prefix) Of Output Files’ is the prefix string to all the output files created by GIFT. This should be a valid character name as the files will be saved using this prefix. Avoid characters like \, /, :, *, ?, ”, < and > in the prefix.
•	‘Have You Selected the fMRI Data Files?’ Click on the push button Select to select the data. There are two options for selecting the data as explained in Section 3.6.3. After the data is selected, the push button Select will be changed to popup with ’Yes’ and ’No’ as the options.
o	Yes’ - Data reduction steps will be enabled if you have selected the parameters previously with the same output prefix.
o	’No’ - the data can be selected again
o	Note: After the data-sets are selected, a file will be saved with suffix Subject.mat. This MAT file contains information about number of subjects, sessions and files.
•	 ’Do you want to estimate the number of independent components?’ Components are estimated (Y.-O. Li, T. Adali and V. D. Calhoun, 2007) from the fMRI data using the MDL criteria. All the data-sets or a particular data-set can be used to estimate the components. When all the data-sets are used, components are estimated for each data-set separately. Mean, median, max and standard deviation are reported in a dialog box.
•	 ’Number of IC’ refers to the number of independent components that will be extracted from the data.
o	Note: If you have selected Constrained ICA (Spatial) and GIG-ICA algorithms, the number of independent components is set to the number of spatial reference files selected.
•	’Do you want to auto fill data reduction values?’ By default this option is set to ’Yes’ when the data is selected and the ’Number of IC’ is set to 20. If there are more than one data reduction step, initial PC numbers are set to 1.5 times the number of final components.
•	’Which Algorithm Do You Want To Use?’ There are 16 ICA/IVA algorithms available like Infomax, FastICA, ERICA, SIMBEC, EVD, JADE OPAC, AMUSE, SDD ICA, Semi-blind Infomax, Constrained ICA (Spatial), Radical ICA, Combi, ICA-EBM, ERBM, IVA-GL, GIG-ICA and IVA-L.
•	 ’Which Group ICA Analysis You Want To Use?’ Options are ’Regular’, ’ICASSO’ and ‘MST’. When you select ’ICASSO’ or ‘MST’, ICA is run several times and the best estimate for each component is used (See Section 3.13.1). Please note that algorithms like JADE OPAC, Constrained ICA (Spatial), GIG-ICA and IVA-GL don’t work with ICASSO. If you want to run stability analysis on IVA-GL algorithm, select ‘MST’. When you select ‘MST’, best run is selected using the highest correlation between the selected component estimates and t-maps obtained using all ICA/IVA runs. Please see (W. Du, S. Ma, G-S. Fu, V. Calhoun, and T. Adalı, 2014) for more information. 
•	‘How Do You Want To Run Group ICA? Options are ‘Serial’ and ‘Parallel’. Enter the number of MATLAB workers desired when group ICA is run in parallel. If Parallel Computing Toolbox is not installed, parts of code are run in separate MATLAB sessions.

Note: If the auto fill data reduction steps drop down box is set to ’No’ after entering the prefix, check the numbers for principal components by clicking the ”Setup-ICA Defaults” menu. (Figure 3.4).

 

Figure 3.3: Initial Parameter Window
 
Figure 3.4: Setup ICA Defaults
Setup ICA Defaults
•	’Select Type Of Data Pre-processing’ - Data is pre-processed prior to the first data reduction. Options are discussed below: 
o	’Remove Mean Per Timepoint’ - At each time point, image mean is removed.
o	’Remove Mean Per Voxel’ - Timeseries mean is removed at each voxel.
o	’Intensity Normalization’ - At each voxel, time-series is scaled to have a mean of 100. When intensity normalization is selected as the pre-processing step, don’t use Z-scores or percent signal change for scaling components.
o	‘Variance Normalization’ - At each voxel, time-series is linearly detrended and converted to z-scores.
•	’What Mask Do You Want To Use?’ There are two options like ’Default Mask’ and ’Select Mask’.
o	‘Default Mask’ - Mask is calculated using all the files for subjects and sessions or only the first file for each subject and session depending upon the variable DEFAULT_MASK_OPTION value in defaults. Boolean AND operation is done to include the voxels that surpass the mean of each subject’s session.
	Note: By default first file for each subject session is selected because using all the files is time consuming. You can use all the files for each subject and session by setting variable DEFAULT_MASK_OPTION value to ‘all_files’. 
o	’Select Mask’ - You can specify a mask containing the selected regions for the analysis. This mask must be in Analyze or Nifti format.
 
Figure 3.5: PCA Options
•	’Select Type Of PCA’ - There are five options like ’Standard’, ’Expectation Maximization’, ’SVD’, ‘MPOWIT’ and ‘STP’. PCA options window (Figure 3.5) will change depending on the type of PCA selected. 
o	Standard 
	’Do You Want To Stack Datasets?’ - Options are ’Yes’ and ’No’.
•	’Yes’ - Data sets are stacked to compute covariance matrix. This option assumes that there is enough RAM available to stack the data sets and for computing covariance matrix. Please note that full storage of covariance matrix is required when you select this option. Storing covariance matrix in memory is expensive for large data.
•	’No’ – GIFT subsamples data in voxel dimension or loads a pair of data sets at a time to compute covariance matrix. This option uses less memory compared to stacked data option but requires multiple data loads and is very slow for large data.
	’Select Matrix Storage Type’ - Options are ’Full’ and ’Packed’. You have the option to store only lower triangular portion of the symmetric matrix with the packed storage scheme. 
	’Select Precision’ - Options are ’Double’ and ’Single’. Single precision uses 50% less memory required when compared to double precision. Single precision is accurate up to 7 digits after decimal point. 
	’Select Eigen Solver Type’ - Options are ’Selective’ and ’All’. These options will be used only for the packed storage scheme. 
•	’Selective’ - Only a few desired eigen values are computed. This option will compute eigen values faster when compared to ’All’ option. However, if there are convergence issues use option ’All’ to compute eigen values. 
•	’All’ - All eigen values are computed. We recommend to use this option for computing eigen values only when the selective eigen solver doesn’t converge.
o	Expectation Maximization (EM PCA) has fewer memory constraints and is advantageous over standard PCA when only few eigen values need to be computed from a large data-set (S.Roweis, 1998). PCA options of this approach are discussed below: 
	’Do You Want To Stack Datasets?’ - Options are ’Yes’ and ’No’. 
•	’Yes’ - This option assumes that there is enough RAM available to stack the data sets. 
•	’No’ – By default, GIFT runs MPOWIT when all data is not loaded in memory as EM PCA is very slow for large data.
	’Select Precision’ - Options are ’Double’ and ’Single’. 
	’Select Stopping Tolerance’ - Norm of residual error is used. Residual error is computed by subtracting the transformation matrix at the current iteration from the previous iteration.
	’Enter Max No. Of Iterations’ - Maximum number of iterations to use.
o	SVD – Singular value decomposition (SVD) is preferable when the data is ill-conditioned. Memory requirements of SVD are similar to covariance based PCA. 
	’Select Precision’ - Options are ’Double’ and ’Single’.
	’Select Solver’ - Options are ’Selective’ and ’All’.
o	MPOWIT – MPOWIT is very useful technique for analyzing large data. The algorithm uses larger subspace than the desired number of components and checks for convergence of desired number of components only.
	’Do You Want To Stack Datasets?’ - Options are ’Yes’ and ’No’. 
•	’Yes’ - This option assumes that there is enough RAM available to stack the data sets. 
•	’No’ – STP estimates are used as initial PCA subspace to minimize the number of data-loads.  
	’Select Precision’ - Options are ’Double’ and ’Single’. 
	’Select Stopping Tolerance’ - Norm of residual error is used. Residual error is computed by subtracting the eigen values in the current and previous iterations.
	’Enter Max No. Of Iterations’ - Maximum number of iterations to use.
	‘Enter block multiplier’ – Default value is set to 10.  
o	STP - Subsampled Time PCA borrows the concept from 3 step data reduction PCA by dividing the data into groups. STP overcomes the shortcomings of 3 step PCA by avoiding whitening in the intermediate PCA stage and updates PCA estimates for each group selected instead of stacking estimates from the intermediate PCA step. STP is an efficient approach for analyzing large data as there is only a single pass over the data. Also, STP estimates could be used as an initial PCA subspace in the MPOWIT algorithm. Options are discussed below:
	’Select Precision’ - Options are ’Double’ and ’Single’. 
	‘Enter number of intermediate components to retain’ – Default value is set to 500 for obtaining accurate estimates.
	‘Select number of subjects in each group’ – Default value is set to 10. If you have less memory on your Operating system, select a value of 4.
Note: Before setting up analysis, please see icatb_mem_ica.m script to get a close estimate of the RAM required for all the analysis types. In general for better performance, stack data-sets using single precision. However, if memory is an issue don’t stack data-sets and use MPOWIT or STP methods to estimate PCA subspace. By default, GIFT will save MAT files in the uncompressed format (-v6). Always use uncompressed format if you want a better performance during the analysis phase. 
•	 ’Select The Type Of Group PCA’ – These options are only used if you are using 2 data reduction approach. Options are ’subject specific’ and ’grand mean’.
o	’Subject Specific’ - PCA is done on each data-set before doing group PCA.
o	’Grand Mean’ - Each data-set is projected on to the eigen space of the mean of all data-sets before doing group PCA (MELODIC, 2004). This PCA requires that time points or number of images are the same between the data-sets.
Note: Subject specific approach retains maximum variance at the individual level PCA when compared to the grand mean approach. Grand mean approach retains more variance at the group PCA when compared to the subject specific approach.
•	’Select The Backreconstruction Type’ - Options are ’Regular’ (GICA2), ’Spatial-temporal regression’, ’GICA3’ and ’GICA’. GICA2 and GICA3 are not shown in the GUI but can be called in the batch script. 
o	’Regular’ - Regular or GICA2 has one desirable property that the sum of the reconstructed subject spatial maps equals the aggregate spatial map. However, product of time courses and spatial maps doesn’t estimate the PCA reduced data. 
o	’Spatial-temporal Regression’ - Back reconstruction is done using a two step multiple regression (N. Filippini, B. J. MacIntosh, M. G. Hough, G. M. Goodwin, G. B. Frisoni, S. M. Smith, P. M. Matthews, C.F. Beckmann, and C. E. Mackay, 2009). In the first step, aggregate component spatial maps are used as basis functions and projected on to the subject’s data resulting in subject component time courses. In the second step, subject component time courses are used as basis functions and projected on to the subject’s data resulting in component spatial maps for that subject. 
o	’GICA3’ - GICA3 has two desirable properties that the sum of the subject spatial maps is the aggregate spatial map and the product of the time courses and spatial maps estimate the data to the accuracy of the PCA’s. Please see (E. Erhardt, S. Rachakonda, E. Bedrick, T. Adali, and V. D. Calhoun, 2010) for more information. 
o	’GICA’ – GICA (V.D. Calhoun, T. Adali, G.D. Pearlson, and J.J. Pekar, 2001) is a more robust tool to back reconstruct components when compared to GICA2 and GICA3 for low model order. 
Note: 
	GICA, GICA2 and GICA3 back reconstruction methods use the PCA whitening and dewhitening matrices to reconstruct subject spatial maps and timecourses. GICA and GICA2 timecourses are similar to the timecourses obtained using Spatial-temporal Regression. 
	Spatial maps obtained using GICA2 are exactly equal to the GICA3 method. 
	All the back reconstruction methods give the same spatial maps and timecourses for one single subject single session analysis. 
	GICA, GICA2 and Spatial-temporal Regression component timecourses are equivalent when 100% variance is retained in the first step PCA.
•	 ’Do You Want To Scale The Results?’ The options available are ’No Scaling’, ’Scale To Original Data(%)’, ’Z-Scores’, ’Scaling in Timecourses’ and ’Scaling in Maps and Timecourses’. ’
o	Scale To Original Data(%)’ - Each subject component image and time course will be scaled to represent percent signal change. 
o	’Z-Scores’ - Each subject component image and time course will be converted to Z-scores. Standard deviation of image is calculated only for the voxels that are in the mask. 
o	’Scaling in Timecourses’ - Spatial maps are normalized using the average of top 1% voxels and the resulting value is multiplied to the timecourses. 
o	’Scaling in Maps and Timecourses’ - Spatial maps are scaled using the standard deviation of timecourses and timecourses are scaled using the maximum spatial intensity value. 
Note: By default, subject component images are centered based on the peak of the distribution. Please see variable CENTER_IMAGES in icatb_defaults.m. 
•	‘Select Group ICA Type’ – Options are ‘Spatial’ and ‘Temporal’. By default, GIFT uses spatial ICA. Options are described below:
o	‘Spatial’ – Independent components are estimated by maximizing independence in space. 
o	‘Temporal’ - Independent components are estimated by maximizing independence in time.
•	’How Many Reduction (PCA) Steps Do You Want To Run?’ A maximum of two reduction steps is provided. If the number of data-sets are greater than one, option is provided to use one or two data reductions. For the example data-set, two reduction steps are automatically selected. 
o	If you are using IVA-GL or IVA-L, each subject’s data is PCA reduced and whitened. There is no data reduction prior to running ICA if you use Constrained ICA (spatial) and GIG-ICA algorithms.
o	If you have selected one data reduction step when analyzing multiple data-sets, group PCA is computed on the stacked pre-processed data-sets.
•	’Number Of PC (Step 1)’ - Number of principal components extracted from each subject’s session. For one subject one session this control will be disabled as the number of principal components extracted from the data is the same as the number of independent components.
•	’Number Of PC (Step 2)’ - Number of principal components extracted during the second reduction step. This control will be disabled for two data reduction steps as the number of principal components is the same as the number of independent components.
Figure 3.6 shows the completed parameters window. Press Done button after selecting all the answers for the parameters. This will open a figure window (Figure 3.7) to select the ICA options. You can select the defaults, which are already selected in the dialog box or you can change the parameters within the acceptable limits that are shown in the prompt string. ICA options window can be turned off by changing defaults (icatb_defaults.m). Currently, the dialog box is only available for the Infomax, FastICA, SDD ICA, Semi-blind ICA, Constrained ICA (Spatial) algorithms and ERBM. After selecting the options, parameter file for the analysis is created in the working directory with the suffix ica_parameter_info.mat.
Note:
•	Different analyses for the same functional data can be run by copying subject and parameter files to a different directory.
•	All the parameters can also be entered by using an input file (3.14.1) or using the GICA command line (Section 3.15). Batch option is very useful for analyzing large data-sets.
 
Figure 3.6: Completed parameters window
 
Figure 3.7: ICA Options
 
Figure 3.8: Run Analysis
3.9.2	Run Analysis

Run Analysis is the step used to perform the group ICA on fMRI data. 
•	The parameter file required for the analysis should be selected (*ica_parameter_info.mat). This file is the same file where you entered all the analysis information. Once the parameter file is selected, a figure (Figure 3.8) will pop up showing the options for run analysis. The options are as follows:
o	’All***’ - All the group ICA steps are run at once. The analysis can also be run by selecting steps from ’Parameter Initialization’ to ’Group Stats’ in order. 
o	’Resume’ - Resume option is used to handle interrupted analysis. Resume option also detects changes in the user input and runs the appropriate group ICA steps. For example, if you changed back-reconstruction approach resume option runs the steps from back-reconstruction to group stats. Resume option is currently disabled if you have run analysis in parallel. 
o	’Parameter Initialization’ - All the variables that are needed later on or during the analysis are declared and initialized. A parameter error check is also preformed to try and catch errors before the group analysis begins.
o	’Data Reduction’ – Depending on the number of data reduction steps and number of data-sets, there is difference in how the common group PCA space is obtained. Please see Section 4.1 for more information. Each reduced data is saved in a MAT file and will be used in both ICA and back reconstruction steps. 
o	’Calculate ICA’ - The concatenated data from the data reduction step is used and the aggregate ICA components are saved in both MAT and Analyze (or Nifti) format. 
o	’Back Reconstruction’ - For ’GICA’, ’GICA2’ and ’GICA3’, the aggregate components and the results from data reduction are used to compute the individual subject components. ’Spatial-temporal Regression’ - The aggregate components and the original data are used to compute the individual subject components. The individual subject components are saved in Analyze (or Nifti) format. 
o	’Calibrating Components’ - By default, components are in arbitrary units. Components are scaled to percent signal change, Z-scores, scaling in timecourses or scaling in maps and timecourses. 
o	’Group Stats’ -  The individual back reconstructed components are used to compute a mean spatial map and time course, a standard deviation spatial map and time course and a t-statistic spatial map. The time course used for the t-statistic component is the mean time course. These group stats components are calculated for each session and are saved in Analyze (or Nifti) format. Results during each of the steps are printed to the MATLAB command window. After the analysis is completed, Display GUI (Figure 3.10) will open automatically for visualizing components.
•	Group PCA Performance Settings - There are three options like ’Maximize Performance’, ’Less Memory Usage’ and ’User Specified Settings’. Best match for each option is selected based on the variable MAX_AVAILABLE_RAM. 
o	’Maximize Performance’ - Reduced data-sets from the first data reduction step are stacked by default.
o	’Less Memory Usage’ – Small groups of data-sets are loaded at a time in a memory.
o	’User Specified Settings’ - User specified PCA options are selected.
Note:
•	All the analysis information is stored in the _results.log file. This file gets appended each time the analysis is run with the same prefix for the output files.
•	Run analysis steps can also be accessed from the command line.
•	load(param_file); % Load parameter file (*ica*param*mat) 
•	sesInfo = icatb_runAnalysis(sesInfo, 1); % Run All Steps 
•	sesInfo = icatb_runAnalysis(sesInfo, 2); % Parameter Initialization 
•	sesInfo = icatb_runAnalysis(sesInfo, 3); % Data Reduction 
•	sesInfo = icatb_runAnalysis(sesInfo, 4); % ICA 
•	sesInfo = icatb_runAnalysis(sesInfo, 5); % Back reconstruction 
•	sesInfo = icatb_runAnalysis(sesInfo, 6); % Scaling components 
•	sesInfo = icatb_runAnalysis(sesInfo, 7); % Group Stats
•	sesInfo = icatb_runAnalysis(sesInfo, 8); % Resume interrupted analysis
•	Option is provided in the GIFT to run a particular data reduction step. This is useful when a particular data reduction step was already done and you would like to go to the next step without re-running the earlier step.
•	load(param_file); % Load parameter file (*ica*param*mat) sesInfo.reductionStepsToRun = 2;  %Run 2nd reduction only
•	sesInfo = icatb_runAnalysis(sesInfo, 3); % Call Data Reduction
•	You could also switch between PCA types using command line. For example, the first data reduction could be done using standard PCA and the memory intensive second data reduction could be done using MPOWIT algorithm.
•	load(param_file); % Load parameter file (*ica*param*mat)
•	%% Run 1st data reduction using Standard PCA
•	sesInfo.pcaType = ’standard’; % Standard PCA sesInfo.reductionStepsToRun = 1; % First reduction 
•	sesInfo = icatb_runAnalysis(sesInfo, 3); % Call data reduction

•	%% Run 2nd data reduction using MPOWIT 
•	sesInfo.pcaType = ’mpowit’; % MPOWIT
•	sesInfo.reductionStepsToRun = 2; % Second reduction
•	sesInfo=icatb_runAnalysis(sesInfo, 3); % Call data reduction
• By default, the component spatial maps and time courses will be written as Nifti files. You have the option to compress image files according to their viewing set name like subject 1 session 1, mean for session 1, etc. The variable used for compressing files is ZIP_IMAGE_FILES (Appendix 6.2).
3.9.3	Analysis Info

Analysis Info contains the information about the parameters, data reduction and the output files. Once the analysis is done, click on the Analysis Info button on the GIFT main window and select the parameter file that you want to look at. Then a figure (Figure 3.9) will pop up showing the information contained within this window.

 
Figure 3.9: Analysis Info
 
Figure 3.10: Display GUI
3.10	VISUALIZATION METHODS
