# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project you will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.  

To complete the project, two files will be submitted: a file containing project code and a file containing a brief write up explaining your solution. We have included template files to be used both for the [code](https://github.com/udacity/CarND-LaneLines-P1/blob/master/P1.ipynb) and the [writeup](https://github.com/udacity/CarND-LaneLines-P1/blob/master/writeup_template.md).The code file is called P1.ipynb and the writeup template is writeup_template.md 

To meet specifications in the project, take a look at the requirements in the [project rubric](https://review.udacity.com/#!/rubrics/322/view)


**GOAL**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I use Gassuain_blur function with factor of 5 to reduction image noise. Third, the canny function find the all edges of image. Fourth, after marking the wanted region by Region_of_interest function, the hough transform find the lines. Last, I draw the lines onto original image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by a slope factor(s). if s>0, then it's defined to the right lane. if s<0, then it's defined to the left lane. I neglect the very small and very large slope factor in this case.
Finally, using the classified x,y datas extrapolate the lines to draw for left and right lanes separately.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the marked region is settled not unproperly, the judgement would be unstable.

Another shortcoming could be the hough transform parameters, especially happening in the switched pipelines, the guilding line sometimes can't direct the line long enough to the distance. 


### 3. Suggest possible improvements to your pipeline

A possible improvement for the first shortcoming would be to using judgements automatically. In the case this time, we manually tune the area of region. In specific, we still need to set a well-initial parameters, but the parameters can be modified and convergent to a best paramenters though a certain judgements such as the amount of s factor. 

Another potential improvement could be to cut the image to two or three frame to adapt different parameters, which can be able to endure the switched pipelines. Furthermore, by doing so, I may could challenge the "challenge case". In the near distance, the pipelines would be linear. In the far distance, the pipelines would be curve. I can utilize the different frames to adapt the different situation. 

