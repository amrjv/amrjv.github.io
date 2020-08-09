## Semi-supervised segmentation with AutoML

**Project description:** 

In this project I demonstrate an app that leverages semi-supervised learning to aid labelling and segmentation of data that could be used for further analysis or training of a deep learning model. For demonstration purposes we will use an example of a Molybdenum Oxide Crystal from <a href="https://deben.co.uk/detectors/stem-detector/">here</a> recorded using annular dark field (ADF) STEM imaging. 

A schema of the JEOL ARM 200CF electron microscope at the University of Oxford Materials Department is shown below. 

<img src="/pages/semi_supervised_segmentation_with_autoML/STEM schema.png?raw=true"/>

Often images taken from electron microscopes are processed manually. Here we want to segment the various phases of the crystal.

<img src="/pages/semi_supervised_segmentation_with_autoML/Molybdenum-Oxide-Crystals-in-DFa-620x400.jpg?raw=true"/>
credit: https://deben.co.uk/detectors/stem-detector/

### 1. Segmentation method

A few months ago, the Dash – Plotly <a href="https://plotly.com/">team</a> created the <a href="https://github.com/plotly/dash-canvas">dash-canvas tool</a> . This inspired me to create a segmentation tool like <a href="https://imagej.net/Trainable_Weka_Segmentation">WEKA</a>  and <a href="https://www.ilastik.org/">Ilastik</a> in Python. 

The idea of the workflow is as follows: 

<img src="/pages/semi_supervised_segmentation_with_autoML/segmentation_workflow.PNG?raw=true"/>

For the interactive segmentation the dash canvas tool was used to paint over the relevant pixels within the image

<img src="https://raw.githubusercontent.com/plotly/dash-canvas/master/doc/segmentation.gif"/>
credit: https://github.com/plotly/dash-canvas

For the image pre-processing, a set of filters similar to the WEKA segmentation approach was used

<img src="/pages/semi_supervised_segmentation_with_autoML/WEKA.png?raw=true"/>
credit: https://imagej.net/Trainable_Weka_Segmentation

For creating the machine learning classifier, an autoML tool such as TPOT was used. TPOT allows the automation of ML pipeline building by combining genetic programming and data pre-processing workflows from scikit-image. 

<img src="/pages/semi_supervised_segmentation_with_autoML/TPOT.png?raw=true"/>
credit: https://imagej.net/Trainable_Weka_Segmentation

For demonstration purposes, the optimiser was run for 20mins to create the pipeline shown below that was used for segmentation. 

```python
classification_pipeline = make_pipeline( 
    RobustScaler(),
    ZeroCount(),
    StackingEstimator(estimator=DecisionTreeClassifier(criterion="gini", max_depth=210, min_samples_leaf=17, min_samples_split=18)),
    XGBClassifier(learning_rate=0.1, max_depth=20, min_child_weight=15, n_estimators=10, nthread=-1, subsample=0.7)
)
```

### 2. The demonstration of the workflow as a web application 

The complete workflow describe here can be packaged into a web application shown in the video. In this demonstration a MoS2 crystal’s phases are identified by painting over them and then used to train a classifier model for segmentation purposes. 

<video width="500" height="246" controls>
  <source src="/pages/semi_supervised_segmentation_with_autoML/dash_ml_paint.mp4" type="video/mp4">
</video>

.

### 3. Closing remarks and things to improve on

Here we have seen an example of a semi-supervised machine learning pipeline to segment images from various imaging experiments. The strength of this approach is that it leverages the scientist’s expertise over a generic mechanical Turk service to provide improved labelling for more advanced machine learning pipelines. 

This is a relatively simple setup however there are many things to improve on depending on the sample. One example is to use relevant filters depending on the material analysed and the other is to optimise the classifier even more by letter the genetic algorithm fine-tune for longer.  
