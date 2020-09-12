# **Finding Lane Lines on the Road** 


**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

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
