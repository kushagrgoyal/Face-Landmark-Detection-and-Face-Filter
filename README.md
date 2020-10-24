# Face-Landmark-Detection-and-Face-Filter

This repository is an experiment in developing a small project baed on Landmark Detection using Deep Learning models and then using the generated Landmarks to add a face filter. A Pig Nose Emoji in this case.

### The Training Dataset
* The training data was taken from Kaggle: https://www.kaggle.com/drgilermo/face-images-with-marked-landmark-points

### Deep Learning Model
* The model is built using Keras 2.3.x
* I initially tried a FCN (Fully Convolutional Network) to directly estimate the Landmark points. But this model had poor performance as the landmarks even in a very clearn image and on the testing dataset were not consistent at all
* Finally, based on a few papers and some articles, I understood that is better to have the model learn to predict a Heatmap, or an area of the landmark location rather than the exact location of the landmark
* So, I used a Gaussian Kernel to covert each landmark into a small area and then the output data was basically converted from an array of numbers to an array of images
* All of these output images are of the same size as the input image, the only difference is the number of channels. The channels in the ouput represent the number of landmark points. Here, in this case, it is 15 landmark points, so 15 channels
* The model finally predicts these landmark heatmaps and these I use a weighted average technique to estimate the location of the Landmark

### Face Filter
* This particular blog post has been most helpful in creating the model that can put a face filter on a person's face: https://pysource.com/2019/03/25/pigs-nose-instagram-face-filter-opencv-with-python/
* I've used my own Keras model for landmark predictions and then used the modified code from the mentioed blog post to be able to put the emoji on the faces
