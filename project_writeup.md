# **Finding Lane Lines on the Road** 

## Writeup Template

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of several steps. First, I converted the images to grayscale to seperate the brightness of each pixel in the image. By using Canny Edge Detection provided by the OpenCV package we can detect strong gradient pixels using a low threshold and high threshold. The threshold is the derivative between pixels (difference in values between pixel). I decided to use to use the recommended low to high ratio of 2:1 (50:150). Through this process, we were able to detect where the edges of our lanes will be. Second, I needed to find where the lines were based on all of the edges we found. In order to do this, I used Hough Transformation, specifically with the OpenCV function. After applying several parameters to constitute what made for a line, I was able to detect which of the edges were actually lines. Third, with the lines in places, I needed just the region of interest. By definining a quadrilateral shape masking on the image, I was able to define which area of the image we cared about. After doing this, I was left with just line segments that constituted our left and right lane. 

Finally, in order to draw a single line on the left and right lanes, I modified the draw_lines() function by seperating the lines that constituted the left and right lanes by slope. Once I had these line segments, I found the average positions of each of the locations to find the average slope which I was then able to extrapolate to the bottom of the image feed and the top point based on the highest point of the lines found respective to the left and right. 


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the camera alignment does not match the image throughout the feed. When this happens, the parameters that the pipeline are based on might not work. The entire pipeline is based on the relative location based on the camera. 

Another shortcoming could be when there are curves in the lane lines. Since our pipeline defines just lines, if there are curves along the lines, we will not able to extrapolate or pick up on them becuase of the limitation of this pipeline. In similar fashion, if there are other aspects of the road there are relevant to where the car should be driving, the pipeline will also not pick this up. Based on this, our pipeline is best used for a freeway. 

Finally, the biggest shortcoming would be if there are other objects in the feed that are picked up based on the gradient differences that are not necessarily relevant to our lane lines. An example of this would be if there is a white car in the distance. Because there are less pixels and we still want to pick up lines, this could be confused as part of a line. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to adjust for curves or other properties of a road that might not necessarily just constitute of straight lane lines. 

Another potential improvement could be to further define the region of interest to be dynamic in the case the image of the road changes. 
