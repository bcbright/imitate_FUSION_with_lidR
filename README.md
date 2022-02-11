# imitate_FUSION_with_lidR
# Summary
These scripts are designed to imitate some [FUSION](http://forsys.cfr.washington.edu/FUSION/fusion_overview.html) gridmetric ouputs with the [lidR R package](https://cran.r-project.org/web/packages/lidR/lidR.pdf).

# How to run
The user edits the variables in Section 1 of 'run_lidr_grid_metrics.r' before running. 'run_lidr_grid_metrics.r' calls 'Metrics.r' as well as the 'lasindex' (free without license) and 'blast2dem' (not free) functions of [LAStools](https://rapidlasso.com/lastools/). If a LAStools license is not available, another method could be used to create a bare-earth digital terrain model (DTM). 

# Differences between this output and FUSION
1.	Lower Strata Density metrics (0-1 m) differ appreciably in some cases; the reason is likely differences in height normalization. This script relies upon on-the-fly TIN normalization available in lidR, but normalization could be done using a DTM in lidR or with LAStools (which might be faster). This difference in normalization also explains some of the slight differences in the >2 m metrics.
2.	The three topographic curvature outputs differ quite a bit, even though they are based on the same paper. My script uses the curvature functions of Jeff Evan’s spatialEco R package. I went to the paper to see about recoding curvature from scratch, but looked at it for about 1 minute and decided that I probably couldn’t improve upon Bob or Jeff.
3.	That CHM-based FPV variable – I threw in the towel trying to figure out how to implement that in R. I thought I came up with some logic for a least a weak imitation, but my logic is no bueno, since values should be between 0-1.
4.	The other CHM metrics, including rumple, agree well, but do differ. lidR’s rumple and FUSION’s rumple were developed based on the same concept, but because of different implementations/interpretations they differ.
5.	Other differences likely exist. I haven't extensively evaluated each of the many metrics.

# Limitations
1.	For a reason unknown to me, I have to run the CHM-based metrics in a separate R session. In other words, if you copy and paste the entire script into an R window, it will crash at the last section, 4.4 (the CHM metrics section). So to run the CHM metrics you need to paste Section 1., Section 4.1, and then Section 4.4.
2.	Lastly, this was only tested/developed on one small test set of 2.6 GB of laz. Running on other acquisitions might reveal issues. I don’t know how well it’d scale with a large acquisition of say 200 GB worth of laz on a normal workstation (16 GB memory); I suspect it would either crash or take a long time to process a much bigger acquisition.
