# PTVProcessor
post-processing tools, including main Gaussian Process regression (GPR) function 

See the manual.pdf for detailed instructions on usage.

# Requirements (and Recommendations)
MATLAB 
Statistics and Machine Learning Toolbox (included in MATLAB 2016+) 
Parallel Processing Toolbox (optional, but recommended)

# Functions and structure

The prepare function takes a raw tiff file and either a .xml file or .csv file from a tracking algorithm (TrackMate or Mosaic) and converts to a format easily readable into GPR function. The format is also useful for exploring with other methods. We call this format "input" and include functions for converting to "vol" which give velocities as pairs of 3D volumes.  (Note that doing so will lose some subpixel resolution in the location of the observed velocities.) This may prove useful for researchers exploring other postprocessing methods.

The hyperparams includes our grid-search based hyperparameter tuning, built on top of MATLAB's fitrgp function, and will output a pair of matrices encoding the computed velocities, as well as a number of parameter options and model standard deviation.

For example, suppose we had a tiff file called 'flow.tiff' and after applying TrackMate obtained 'tracks.xml'. We use a segmentation file saved as 'seg' in the workspace. Then to obtain the velocity estimates we might run in the MATLAB console: 

[X, V, tracks, img] = prepare('flow.tiff', 'tracks.xml', 33, 'TrackMate', 17, 35) ;

[mu_x, mu_y, mu_xsd, mu_ysd, ~ , ~ , ~ , ~ , ~ , ~ , ~] = hyperparams(X,V,seg);

# Data

The data includes every file we used except for the raw tiff file and segmentation data files. Both types are too large for Github, but either the first or last author would be more than happy to provide the dataset. The segmentation files in particular are easy to produce on your own and do not significantly affect the results.

# GUI 

The GUI is provided in the directory 'PTVProcessor' and can be accessed by opening Matlab (with that directory included in the path) and running the command 'PTVProcessor'. An additional README file is provided in the directory.