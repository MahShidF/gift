1	TABLE OF CONTENTS
2	Introduction	5
2.1	What is GIFT?	5
2.2	Why ICA On fMRI data?	5
2.3	Why Group ICA?	5
3	Getting Started With GIFT	8
3.1	Installing GIFT	8
3.2	Installing Example Subjects	8
3.3	HTML Help Manual	8
3.4	New Features	8
3.5	GIFT Updates	9
3.6	Things to do before configuring the analysis	9
3.6.1	Compiling MEX files	9
3.6.2	Memory Requirements	10
3.6.3	Organizing data	10
3.6.4	Defaults	10
3.7	Spatial Templates	11
3.8	Menus	12
3.9	Analysis Functions	15
3.9.1	Setup ICA  Analysis	15
3.9.2	Run Analysis	25
3.9.3	Analysis Info	27
3.10	Visualization methods	29
3.10.1	Display GUI	29
3.10.2	Subject Component Explorer	32
3.10.3	Orthogonal Explorer	34
3.10.4	Composite Viewer	35
3.11	Sorting Components	36
3.11.1	Temporal Sorting	36
3.11.2	Spatial Sorting	41
3.12	Utilities	44
3.12.1	Generate Mask	45
3.12.2	Remove Component (s)	46
3.12.3	Temporal Sorting	49
3.12.4	Stats On Beta Weights	49
3.12.5	SPM Stats	51
3.12.6	Spatial-temporal Regression	51
3.12.7	Write Taliarach Table	52
3.12.8	Component Labeler	52
3.12.9	Ascii To SPM.mat	53
3.12.10	Event Average	53
3.12.11	Calculate Stats	54
3.12.12	Spectral Group Compare	54
3.12.13	Single Trial Amplitudes	55
3.12.14	Z-shift	56
3.12.15	Percent Variance	56
3.13	Toolboxes	57
3.13.1	ICASSO	57
3.13.2	Mancovan	59
3.13.3	Temporal dFNC	75
3.13.4	Spatial dFNC	84
3.13.5	Noise cloud	88
3.14	Batch Script	89
3.14.1	Analysis	89
3.14.2	Display	94
3.14.3	Stats On Beta Weights	95
3.14.4	Mancovan	96
3.14.5	Temporal dFNC	97
3.15	GICA Command line	98
3.16	Output files naming	98
3.17	Source Based Morphometry	99
3.17.1	SBM Stats	100
3.18	Independent Vector Analysis	101
3.19	Display Tools	103
3.19.1	Image Viewer	103
3.19.2	Component Viewer	106
3.19.3	Network Summary	107
4	Process Involved In Group ICA	111
4.1	Data Reduction (PCA)	111
4.2	Independent Component analysis	111
4.2.1	Infomax	112
4.2.2	Fast ICA	112
4.2.3	JADE OPAC	112
4.2.4	SIMBEC	113
4.2.5	AMUSE	113
4.2.6	ERICA	113
4.2.7	EVD	113
4.2.8	Constrained ICA (Spatial)	114
4.2.9	GIG-ICA	114
4.2.10	Real-valued ICA-EBM	114
4.2.11	Real-valued ICA-ERBM	114
4.3	Back-reconstruction	115
4.4	Scaling Components	115
4.5	Group Stats	115
5	Bibliography	115
6	Appendix	120
6.1	Experimental Paradigms	120
6.2	Defaults	120
6.3	Options Window	123
6.4	Defaults GUI	125
6.5	Regular Expressions	125
6.6	Interactive Figure Window	126
6.7	GIFT Startup	127

2	INTRODUCTION

This manual is divided mainly into three chapters. Motivation for using the group ICA of fMRI Toolbox (GIFT) is discussed in this chapter. In Chapter 3, quick start to the toolbox is discussed. Chapter 4 focusses on the process involved in group ICA. In Section 3.17, Source Based Morphometry is discussed. A brief discussion is given on Independent Vector Analysis (IVA) in Section 3.18.

2.1	WHAT IS GIFT?

GIFT is an application developed in MATLAB that enables group inferences from fMRI data using Independent Component Analysis (ICA). A detailed explanation of ICA is explained in the next section. GIFT is used to run both single subject and single session analysis as well as group analysis. Toolbox is thoroughly tested and works on MATLAB R2008a and higher.

2.2	WHY ICA ON FMRI DATA?

Functional Magnetic Resonance Imaging (fMRI) is a modality for studying the brain function. fMRI techniques use Blood Oxygenation Level Dependent (BOLD) signal as a measure for detecting the neural activity. Since fMRI uses an indirect measure of neural activity, mathematical models are needed to analyze the data. Many fMRI experiments use a block design in which the subject is instructed to perform experimental and control tasks in an alternating sequence of 20-40 second blocks. The resulting activity is recorded for each volume element (voxel) of the brain. Based on events of the experimental task and knowing shape of the haemodynamic response, a reference function is constructed. Model based techniques such as SPM (Statistical Parameteric Mapping, 1991) use this reference function to separate the signals of interest and the signals not of interest. A general method is necessary which does not depend on the prior information of the experiment or task. In this respect, a statistical technique called Independent Component Analysis (ICA) (M. J. McKneown, Scott Makeig, Greg G. Brown, Tzyy-Ping Jung, Sandra S. Kindermann, Anthony J. Bell and Terrence J. Sejnowski, 1998) is proposed that allows the extraction of signals of interest and not of interest without any prior information about the task. Thus ICA analysis could reveal characteristics of the brain function that cannot be modeled due to lack of prior information. Independent Component Analysis (ICA) is a method of blind source signal separation i.e., ICA allows one to extract or “unmix” unknown source signals which are linearly mixed together (Figure 2.1). For fMRI data, temporal and spatial ICA are possible, but spatial ICA is by far the most common approach. The GIFT implements spatial ICA of fMRI data. In the current version, option is provided to do temporal ICA. In spatial ICA, spatially independent brain sources or components are calculated from fMRI data. Figure 2.2 shows a component extracted from the fMRI data. For a complete description of this experiment please see Appendix 6.1.

2.3	WHY GROUP ICA?

ICA has been successfully applied to single subject and single session analyses. Group analysis of fMRI is important to study specific conditions within or between groups of subjects. It is not clear how ICA can be applied on a group of subjects as different individuals in the group will have different time courses. In (V.D. Calhoun, T. Adali, G.D. Pearlson, and J.J. Pekar, 2001), a model was proposed to extend ICA to group studies. The GIFT contains an implementation of ICA for analyzing the fMRI data. Specifically, the GIFT implements both analysis and display tools, each using standard input and output file types (Analyze or Nifti format). There are three main stages to Group ICA; Data Compression, ICA, and Back Reconstruction (V.D. Calhoun, T. Adali, G.D. Pearlson, and J.J. Pekar, 2001). The outputs from these stages are multiple time courses. Each time course has an image map associated with it. A detailed explanation of the process involved in group ICA is discussed in the Chapter 4.

 
Figure 2.1: Unknown source signals (top row) are determined from mixed signals (bottom row).
 
Figure 2.2: A component consists of a spatial map and a timecourse
