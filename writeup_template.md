# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg "solidWhiteCurve"
[image2]: ./test_images_output/solidWhiteRight.jpg "solidWhiteRight"
[image3]: ./test_images_output/solidYellowCurve.jpg "solidYellowCurve"
[image4]: ./test_images_output/solidYellowCurve2.jpg "solidYellowCurve2"
[image5]: ./test_images_output/solidYellowLeft.jpg "solidYellowLeft"
[image6]: ./test_images_output/whiteCarLaneSwitch.jpg "whiteCarLaneSwitch"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

At the beginning, I prepared the image for Canny transformation by turning it to grayscale and using Gaussian filter to remove some unneeded details. My pipeline afterwards consisted of 3 major steps. First step was to use Canny transformation to detect the edges in the image. After applying Canny transformation, I used region masking. The edge image was masked using a four sided polygon. The third step was applying Hough transformation to detect left and right line segments.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by spliting line segments into the right and left set. All of the segments that have a slope bigger than zero belong to the left lane, while the segments with slope smaller than 0 belong to the right lane. In addition to calculating the slope of each section, I also calculated the intercept of each segment. At the end, I found mean values of all left slopes and left intercepts, as well as mean values of all right slopes and right intercepts. Using these values it is possible to draw left line and right line that mark the lane.

Below are the final results of my image processing.

![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the lane is not straight as in the given test images and videos, but instead more curvy, like in the additional "challenge" video. When the lane is curvier, line sections will have a wider range of slopes. If their absolute value is not in the range (0.5, 0.9) they will not be considered in the calculation. 

Another shortcoming could be that the slopes and intercepts of different sections detected by Hough transform can have a huge range as well. Some outliers can appear, which can tilt the calculation and cause the detected lines to be incorectly positioned.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to remove the outliers when calculating slopes and intercepts of the line segments. 

Another potential improvement could be to split the image into the right and left half and fit a line through the dots that define left segments and then another line through the dots that belong to the right segments. Using polyfit function could help in avoiding outliers.


