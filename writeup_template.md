# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of several steps:
1.I applied gaussian bluring to the images and converted them to grayscale
[image1]: ./examples/grayscale.jpg "Grayscale"
2.Then I applied canny edge detector in order to find edges.
[image2]: ./examples/canny.png "Canny edges"
3.Then manually defind points limiting the region of ineterst in the image: the part of the image containing part of road and lane markers along which the car is driving to.
4.Then I obtained masked images after masking pixels below the trashold inside the roi.
5.Then I applied  Hough transform to the edge image in order to detect straight lines inside the roi.
[image3]: ./examples/hough.png "Hough lines inside ROI"
6.Then I used draw_lines() funcion. It's initial version allowed to draw all detected lines on the initial image. However I've improved the function with the following steps: 
- I separated detected lines into to groups: left and right, according to their slopes.
- I collected all X-s and Y-s in each group, dropping the lines whici would cross the center of the roi.
- Then I calculated min and max X and Y in for each group. These points can be used to draw only two lines: left and right. But such lines wouldn't always start from the bottom of the image, and then I found line equations in order to find points which would belong to the line, but lie on the bottom. As the result, I use final version of draw_lines() in order to draw only two lines - left and right - both starting from the bottom of the image.

[image4]: ./examples/left_right.png "Result (after improving draw_lines)"


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the car would pass the turn, and lane markers would be mostly curved, not straight.

Another shortcoming could emerge during the night, bad weather or cases when lanes are old and partially absent: all situations when they're hard to be detected by camera.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use dome algorothm to deterime not only straight lines, but also curved.

Another potential improvement could be to use additional information from sensord like LIDAR or from digital maps.
