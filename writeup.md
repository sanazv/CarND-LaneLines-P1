#**My Writeup for Finding Lane Lines on the Road Project** 


---

##**Overview**

The goal of this project was to detect traffic lanes on images. The images are from cameras mounted to the front of the car.

##**PipeLine Description**

The pipeline is divided into two major sections: pre-processing and lane finding. In the pre-processing stage, I very much follow the steps covered in the lectures: 

1) convert the color image to grayscale

2) apply Gaussian smoothing

3) apply Canny filter for edge detection

4) mask out areas which are not in the region of interest

5) apply Hough transform to detect lines

I have also modified ```HoughLinesP``` funciton to output the line endpoints as well as the image matrix. For the lane finding, I take each line endpoint, and fit the points to the line equation ```y=mx+b``` and find m and b accordingly.
Looking at the distribution of slope (```m```) values, it is clear that there are two peaks corresponding to the two lanes. 
I then split the distrbution at ```m=0``` which is the vertical in the middle of the image. For each right and left segment, I calculate the median of the slope distribution and y-intercept. Using these values, I form two new lines, from the bottom of the image to the edge of the mask.

---

##**Opportunity for improvement**
First when applied to the challenge video, this pipeline did not perform very well. So the first step would be to improve the way final lines are calculated as they did not intesect the bottom edge of the image.
Another aspect of improvement is to use linear regression to fit a line to the line segment endpoints (output of modified ```HoughLinesP```) rather than individually solving for ```m``` and ```b``` per segment and then averaging. If time allows I will experiment with this option.

