# Investigating the Microvessel Architecture of the Mouse Brain:
## An Approach for Measuring, Stitching, and Analyzing 50 Terabytes of Data 

The presentation and related material for the SRI 2015 Conference
- The [slides](https://rawgit.com/4Quant/SRI2015/master/SRIPres.html) can be seen here
- A Demo of our [Quantitative Image Search Engine](https://kmader.shinyapps.io/SearchMachineDemo)

## Relevant Links

- [Quantitative Big Imaging Course](http://kmader.github.io/Quantitative-Big-Imaging-2015/)
- [X-Ray Imaging Group at ETH Zurich](http://www.biomed.ee.ethz.ch/research/x-ray_imaging)
- [Presentation at Spark Summit 2014](http://4quant.com/spark-summit-2014-presentation)
- [Spark Introduction](http://4quant.com/spark-introduction/)

## Bio
Kevin Mader is the founder of 4Quant and a lecturer in the X-ray Microscopy Group within the Department for Information Technology and Electrical Engineering at ETH Zurich. His research focuses on turning big hairy 3D images into simple, robust, reproducible numbers without resorting to black boxes or magic. In particular, as part of several collaborations, he is currently working on automatically segmenting full animal zebrafish images, characterizing rheology in 3D flows, and measuring viral infection dynamics in cell lines.

## Abstract
The task of processing and analyzing such large collections of measurements is exceptionally difficult. In this work, we address the challenge of stitching together terabytes worth of scans in a parallel, distributed manner. Building on the distributed frameworks of Apache Spark and Spark Imaging Layer, we have extended the methods of (S. Preibisch, Saalfeld, and Tomancak 2009) to work on these images enabling the use of many machines in parallel and drastically accelerating the speed and ease with which these large datasets can be stitched and analyzed.
By automating the acquisition, we conduct all of the scans locally in a zigzag pattern to minimize the effect of motor position drift. Each scan consists of 1000 projections sized 2560 x 2160 (14GVx) with 0.65μm isotropic voxel size. To measure the entire mouse brain approximately 15 steps will be taken in each direction (~3400 total→ 50TVx). A correlation is performed and the maximum value is taken to produce an offset vector. The entire set of positions is then updated in an iterative manner with a smoothing function applied to these vectors.

### Supplemental Materials 
#### Measurements
For the pilot study the brain sample was measured at the TOMCAT Beamline at 25keV. The scans were performed locally and consisted of 1000 projections of 2560 x 2160 resulting in a final volume of 14 GVx covering a field of view of 1.67 x 1.67 x 2.8mm with an isotropic voxel size of 650nm. The tests consisted of 60 scans of 5 x 6 x 2.
#### Stitching
The images are stored as key-value pairs ([(x ⃗,Img),⋯]) with the key being the position of the slicee and the value being the image contents of that slice. The stitching is performed by performing comparing all of the images to all of the other images which are touching it. The keys (positions) are then updated and the process can be interated until the the image can be perfectly combined or a tolerance is reached. The results can then be stored in this format. For processing they can be reading and caching as 'views' taken from ImgLib2 (Pietzsch et al. 2012) to generate a given view or slice of the data by reading and actively stitching the components together.
#### Citations
- Pietzsch, T., S. Preibisch, P. Tomancak, and S. Saalfeld. 2012. “ImgLib2–generic image processing in Java.” Bioinformatics 28 (22): 3009–11. doi:10.1093/bioinformatics/bts543.
- Preibisch, Stephan, Stephan Saalfeld, and Pavel Tomancak. 2009. “Globally optimal stitching of tiled 3D microscopic image acquisitions.” Bioinformatics (Oxford, England) 25 (11): 1463–5. doi:10.1093/bioinformatics/btp184
