#**Finding Lane Lines on the Road** 



**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/solidWhiteCurve-gray.jpg "Grayscale"
[image2]: ./examples/solidWhiteCurve-canny.jpg "Canny"
[image3]: ./examples/solidWhiteCurve-masked.jpg "Masked"
[image4]: ./examples/solidWhiteCurve-hough.jpg "Hough"
[image5]: ./examples/solidWhiteCurve-dashed.jpg "Dashed"
[image6]: ./examples/solidWhiteCurve-final.jpg "Final"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale and applied Gaussian smoothing.

![alt text][image1]

In the next step, I applied the Canny Edge Detection to identify the boundaries in the image.

![alt text][image2]

In order to remove edges that are not part of the region of interest, I applied a mask to the image.

![alt text][image3]

The masked image was used for the Hough Transformation in order to identify lines and retrieve their coordinates, which were drawn onto a black background.

![alt text][image4]

As a final step of the first part, the image with the drawn lines was merged with the photo.

![alt text][image5]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 

- calculating the slope of each line
- determining if left (positive slope) or right (negative slope) line 
- dismissing lines if there slope is outside of < 0.4 and > 1.0
- calculating intercept and length of each passed line
- using the numpy.average() function to calculate an average slope/intercept of all left/right lines using their lengths as weights
- determining the coordinates for the left/right line
- drawing the lines

![alt text][image6]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when a large truck is in front of the vehicle.

Other shortcomings could be a very curved road or driving in the dark.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to identify the line color. Only let white/yellow lines pass the pipeline.

Another potential improvement for videos could be to use the slope/intercept of the previous frame as a starting point in order to remove flickering.