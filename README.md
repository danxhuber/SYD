## Summary

Translation of the asteroseismic SYD pipeline ([Huber et al. 2009](https://ui.adsabs.harvard.edu/abs/2009CoAst.160...74H/abstract)) from IDL into python.

The pipeline works in two major parts:
1) findex: automatically finds power excess due to solar-like oscillations using a frequency resolved collapsed autocorrelation function
2) fitbg: perform a fit to the granulation background and measures the frequency of maximum power (nu_max), the large frequency separation (Delta_nu) and oscillation amplitude

## File Overview

### Files/
- todo.txt: File containing IDs of stars to be processed 
- todo/: Directory containing data to be processed. File format: ID_LC.txt (lightcurve: days versus fractional flux) and ID_PS.txt (power spectrum: muHz versus ppm^2 muHz^-1). 
- params_findex.txt: input parameters for findex module (detailed documentation coming)
- params_fitbg.txt: input parameters fot fitbg module (detailed documentation coming)
- star_info.csv: basic information on stars to be processed. If no estimate of numax is provided, the stellar parameters are used to calculate as estimate
- results/L Directory containing result plots

### Code/
- utils.py : bulk of the SYD pipeline
- functions.py : models, distributions, ffts, smoothing functions are all in this file
- SYD.py : initiates SYD through utils.main
- QUAKES.py : asteroseismology pipeline created in parallel with SYD under advisor Dan Huber (i.e. a more pythonic approach to asteroseismology). The initial use and intent of this pipeline also considers planet hosts and has additional time domain tools to remove planet transits and other anomalies in the time domain.

Documentation and code under construction.

## Example

To run example code clone/download the repository and then do:
- cd Code/
- python SYD.py

This will run the pipeline on the two stars specified in the todo.txt file (KIC1435467 and KIC2309595), first using the findex module followed by the fitbg module. If you'd like to skip findex (e.g. useful for a handful of high S/N stars where you can visually estimate nu_max and thus specify it manually in star_info.csv), set findex = False in SYD.py.