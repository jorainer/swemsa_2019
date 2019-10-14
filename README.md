# Presentation for the SWEMSA 2019 conference

This repository contains the code, data and presentation of my talk at the
[SWEMSA conference 2019](https://swemsa.eu) in Erding, Germany. The talk is
focused on LC-MS/MS data analysis with `xcms` and mentions also recent
developments in the [RforMassSpectrometry](https://rformassspectrometry.org)

The online version of the talk can be accessed
[here](https://jorainer.github.io/swemsa_2019/xcms-ms.html).



## Extended abstract

### Handling and processing metabolomics data with Bioconductor’s MSnbase and xcms packages

#### Open source software for efficient mass spectrometry and metabolomics data analysis


Bioconductor is an open-software, open-development software project for the
analysis of high throughput data in genomics and molecular biology [1] in the
context of the rich statistical programming environment offered by the R
project. Bioconductor enables the rapid creation of workflows combining multiple
data types and analysis methods provided by any of its over 1,500 software
packages. The xcms package [2] is a well established Bioconductor package and
one of the standard toolboxes for the preprocessing of untargeted metabolomics
data. The MSnbase package [3], primarily designed for proteomics data analysis,
provides basic infrastructure for import and handling of mass spectrometry (MS)
data.

We recently improved the MS data handling capabilities of MSnbase by introducing
an on-disk data mode that, in contrast to keeping the full MS data in memory,
holds only a subset of the data in memory, importing MS peak data (m/z and
intensity value pairs) from the original MS data files on demand. The resulting
reduction in memory demand enables the analysis also of very large experiments,
even on standard hardware. High performance is achieved by making extensive use
of the random-access capabilities of indexed mzML, mzXML and CDF files and by
parallelizing all operations on a per-file basis. Because peak data are now no
longer residing in memory, they can also not be directly manipulated anymore. We
thus implemented an approach employing a lazy evaluation strategy, that adds
manipulation operations (such as centroiding or base line correction) to a
processing queue and applies them to the peak data upon request (i.e. each time
the user accesses MS peak data).

In addition to above described improvements in MSnbase, we rewrote big parts of
xcms to reuse objects and functionality from the MSnbase and thus better
integrate xcms into the Bioconductor framework. xcms gained native support for
MS level > 1 data handling and inherits all data processing, sub-setting and
filtering methodology from MSnbase. As a consequence, access to raw data and
extraction of ion chromatograms (EICs) was simplified and is now possible at any
stage during data preprocessing. Because settings for preprocessing algorithms,
such as centWave-based chromatographic peak detection, are highly data set
specific, we implemented functions to to aid in evaluation of parameters for the
various methods. It is for example now possible to perform peak detection
directly on EICs (Figure 1) which enables the fine-tuning of peak detection
settings on selected signals.

The most recent improvements in xcms comprise tools to work with LC-MS/MS
experiments. For experiments employing data dependent acquisition (DDA), MS2
spectra can be identified and extracted for each detected chromatographic peak
or feature thus facilitating an improved compound annotation. For data
independent acquisition (DIA) data such as SWATH data, xcms allows to perform
chromatographic peak detection on MS2 data and reconstruct MS2 spectra for MS1
chromatographic peaks by matching MS2 chromatographic peaks to MS1
chromatographic peaks based on the isolation window and peak shape correlation.

While xcms’ lack of a graphical user interface might seem disadvantageous at
first, its command line usage enables the definition of analysis scripts which,
as a consequence, ensure reproducibility of analyses, even more so in
combination with rmarkdown which allows to create reproducible analysis
workflows and, more importantly, human readable analysis reports.

Over and above, we improved the MS data handling infrastructure in
R/Bioconductor enabling also the analysis of large experiments and, by re-using
the capabilities of MSnbase in xcms, allowing also an efficient preprocessing of
very large metabolomics data sets. The recent changes simplified metabolomics
data handling in R and added support for the analysis of LC-MS/MS data.


Acknowledgements

The author thanks Laurent Gatto, Michael Witting, Jan Stanstrup and Steffen
Neumann for their contributions, suggestions and comments.


1. Huber W, Carey VJ, Gentleman R, Anders S, Carlson M, Carvalho BS, et
   al. Orchestrating high-throughput genomic analysis with Bioconductor. Nat
   Meth. 2015;12:115–21.
2. Smith CA, Want EJ, O'Maille G, Abagyan R, Siuzdak G. XCMS: processing mass
   spectrometry data for metabolite profiling using nonlinear peak alignment,
   matching, and identification. Anal. Chem. 2006;78:779–87.
3. Gatto L, Lilley KS. MSnbase-an R/Bioconductor package for isobaric tagged
   mass spectrometry data visualization, processing and
   quantitation. Bioinformatics. 2012;28:288–9.

Author
Dr. Johannes Rainer
Institute for Biomedicine, Eurac Research
Via Luigi Galvani 31, I-39100 Bolzano Italy

 


