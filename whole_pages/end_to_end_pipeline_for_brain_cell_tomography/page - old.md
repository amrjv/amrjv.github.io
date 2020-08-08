## End-to-end pipeline for rodent brain cell tomography

**Project description:** Biological labs use several experimental techniques and instruments to analyse their samples. These techniques output vast quantities of data daily that requires to be processed. On a fundamental level, research is performed in an iterative manner which as be summarised in a closed cycle where data is collected, pre-processed, analysed and compared. 

<img src="/pages/end_to_end_pipeline_for_brain_cell_tomography/figure1.png?raw=true"/>

### 1. Proposed approach

To maintain the competitive edge and iterate as quickly as possible, automation is required. With recent developments in machine learning and deployment frameworks, it is possible to create robust end to end analysis pipelines rapidly. 

<img src="/pages/end_to_end_pipeline_for_brain_cell_tomography/figure2.png?raw=true"/>

### 2. The sample

In this project I demonstrate an app where the data pre-processing, analysis and reporting is automatically handled with a combination of machine learning and “classical” image processing. For this we will use an example of a rodent brain cell from the <a href="https://www.epfl.ch/labs/cvlab/research/">EPFL CV lab</a>

We want to measure morphological changes within the shapes of these cells as these can be linked to diseases. One of the approaches to measure these morphological changes at high resolution as shown <a href="https://en.wikipedia.org/wiki/Serial_block-face_scanning_electron_microscopy">here</a>

This technique slices the samples into sections using an ultramicrotome and preiodically records a scanning electron microscope image. The GIF below demonstrates the idea.

<img src="/pages/end_to_end_pipeline_for_brain_cell_tomography/slice_view.gif?raw=true"/>

The image stack represents a 5x5x5µm section taken from the CA1 hippocampus region of the brain, corresponding to a 1065x2048x1536 volume with a voxel resolution of ~5nm.

### 3. The analysis method 

To obtain quantitative information for the sample, the mitochondria need to be segmented from the images. For this dataset, a simple U-Net architecture (called this because the network resembls a U shape) is used. Figure credit : <a href="https://github.com/HarisIqbal88/PlotNeuralNet/blob/master/examples/Unet/Unet.pdf">here</a>. For further reading please refer to the publication <a href=" https://arxiv.org/ftp/arxiv/papers/1605/1605.09612.pdf">here</a>

<img src="/pages/end_to_end_pipeline_for_brain_cell_tomography/figure3.PNG?raw=true"/>

Once we have trained the neural network, we can load the data we want to make predictions on (Blue labels show the predictions)

<img src="/pages/end_to_end_pipeline_for_brain_cell_tomography/figure4.PNG?raw=true"/>

To measure various features within the image, we can use the <a href="https://scikit-image.org/">scikit-image</a> package 

### 4. The demonstration of the workflow as a web application 




### 5. Closing remarks and things to improve on