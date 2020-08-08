## End-to-end pipeline for rodent brain cell tomography

**Project description:** 

In this project I demonstrate an app where the data pre-processing, analysis and reporting is automatically handled with a combination of machine learning and “classical” image processing. For this we will use an example of a rodent brain cell from the <a href="https://www.epfl.ch/labs/cvlab/research/">EPFL CV lab</a>

We want to measure morphological changes within the shapes of these cells as these can be linked to diseases. One of the approaches to measure these morphological changes at high resolution as shown <a href="https://en.wikipedia.org/wiki/Serial_block-face_scanning_electron_microscopy">here</a>

This technique slices the samples into sections using an ultramicrotome and preiodically records a scanning electron microscope image. The GIF below demonstrates the idea.

<img src="/pages/end_to_end_pipeline_for_brain_cell_tomography/slice_view.gif?raw=true"/>

The image stack represents a 5x5x5µm section taken from the CA1 hippocampus region of the brain, corresponding to a 1065x2048x1536 volume with a voxel resolution of ~5nm.

### 1. The analysis method 

To obtain quantitative information for the sample, the mitochondria need to be segmented from the images. For this dataset, a simple U-Net architecture (called this because the network resembls a U shape) is used. Figure credit : <a href="https://github.com/HarisIqbal88/PlotNeuralNet/blob/master/examples/Unet/Unet.pdf">here</a>. For further reading please refer to the publication <a href=" https://arxiv.org/ftp/arxiv/papers/1605/1605.09612.pdf">here</a>

<img src="/pages/end_to_end_pipeline_for_brain_cell_tomography/figure3.PNG?raw=true"/>

Once we have trained the neural network, we can load the data we want to make predictions on (Blue labels show the predictions)

<img src="/pages/end_to_end_pipeline_for_brain_cell_tomography/figure4.PNG?raw=true"/>

To measure various features within the image, we can use the <a href="https://scikit-image.org/">scikit-image</a> package. In this instance I measure the equivalent diameter of the segmented labels. 

### 2. The demonstration of the workflow as a web application 

All of the workflow described here can be packaged into a web application shown in the video. In this instance the 3D volume renders have been pre-computed along with the final results and the neural network model due to limitations of the free cloud hosting instance. However, it is easy to extrapolate this concept into a full pipeline using a real sample with more compute. 

<video width="500" height="246" controls>
  <source src="/pages/end_to_end_pipeline_for_brain_cell_tomography/rodent_tomo_app.mp4" type="video/mp4">
</video>

.

### 3. Closing remarks and things to improve on

Here we have seen an example of a machine learning pipeline that can be extended for tomography samples from microscopy. We see that the data can be visualised in 3D, segmented and analysed in a matter of few minutes using deep learning and more traditional approaches. There are many things to improve upon in this relatively simple set-up such as using a more sophisticated model or interactively computing the volumetric plots. However for demonstration purposes it explores the scope pretty well. 