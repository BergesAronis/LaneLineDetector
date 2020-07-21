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

### 1. draw_lines() modifications

My pipeline consisted of 5 steps. First, 
1. I converted the images to grayscale
1. I applied a gaussian blur
1. I applied a canny transform
1. I selected a region of interest
1. I identified hough line interesections from the cannied image
1. I refocused on the same region of interest to keep the lines in place



In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first finding the slope of the lines and catagorizing them into either a left (negative) line or right (positive) line. Once each line is catagorized, for each left and right, I found the minimum and maximum x and y values. Using this I calculated the line between this min and max and then extended the line beyond these 2 points.


### 2. Potential shortcomings


One potential shortcoming would be what would happen when there exists lines on the road that are not part of the lane lines, this could include intentional lines like warnings, bike lane indicators, carpool lane signs or unintentional ones like road crack and pothole filings. My modification would still use this and it would skew the lane lines to the center of the road.

Another shortcoming could be images on vehicles in front of us, imagine a truck with the image of a road on its back panel. my algorithm would likely include this in our road line identification.


### 3. Possible improvements

A possible improvement would be to first run the image through a segmentation net. Allowing us to seperate the road itself from other objects like the horizon, vehicles and other obstructions. Then given the road, I would like to identify to points of where the camera expects roadlanes to be. Once we have this in place, instead of doing a min/max calculation, we can do a weighted average of slope relative to the expected points. So lines closer to the points have larger importance when determining slope. The we can extend this slope as usual and have accurate road lines.
