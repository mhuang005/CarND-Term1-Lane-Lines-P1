# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1.  The pipeline for identifying the left and right lanes. 

My pipeline consisted of 5 steps:

* Covert the images to grayscale
* Apply the optional Gaussian smoothing and the Canny edge dector to the grayscale images
* Define a region of interest (e.g., polygon) and use it as mask to remove image pixels
* Conduct the Hough transform on masked edges to obtain the line image with line segments. 
* Generate a weighted image from the line image and the original image

An improvement on drawing the lanes was made by modifying the the draw_lines() function. That is, we separate
the line segements in two groups by the (postive and negative) slope values. Then, we average the slops and centers
of the line segements over each group to obtain a slope and a point (i.e., center) for each group. Since a line can be
uniquely determined by a point and a slop (through the point), we obtain the left lane and right lane by simply giving a
lower bound and a upper bound on y.  Note that we can use the regression model to fit the centers and then obtain two lines
as well. 


Here is an image with two solid lines after the draw_lines() function was modified:

![alt text][image2]

[image2]: ./test_images_output/solidYellowLeft.jpg


### 2.  Potential shortcomings with the current pipeline

One potential shortcoming would be that the hyperparameters (e.g., Canny thresholds, Hough line parameters) in the pipeline are fixed.
As I've noticed, the hyperparameters (after fine-tunning) worked well most time on the test videos, and there were a few frames that
the algorithm didn't generate the reasonable lines on.  


### 3. Possible improvements on the current pipeline

A possible improvement would be to use an adaptive algorithm to adjust the hyperparameters. That being said, it is not easy to
come up with an algorithm.  A simple way may be adjust the slope (e.g., by a threshold) during the image streaming.


