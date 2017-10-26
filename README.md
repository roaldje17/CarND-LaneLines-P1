# **Finding Lane Lines on the Road** 


---

##  Objectives

This document presents a brief report on the project which consists on finding lane lines on the road.


[//]: # (Image References)

[image1]: ./test_images_output/grayscaled_image.jpg "Grayscale"
[image2]: ./test_images_output/edged_image.jpg "edge"
[image3]: ./test_images_output/masked_image.jpg "masked"
[image4]: ./test_images_output/weighted_image.jpg "lane line"
[video]: ./test_videos_output/solidWhiteRight.mp4 "video"
---


##  Project pipelines
My pipelines involves 5 steps which are listed below:

1. Image conversion to grayscale


2. Image denoising

3. Edge detection

4. Image masking

5. Lane lines extraction and drawing

### Image coversion to grayscale
 I converted the rgb image into grayscale for further processing. This processing make important edges more visible as edges are essential for lane detections. 

![alt text][image1]

### Image denoising

The grayscale image is then smoothed by a Gaussian function. Smoothing reduces noise in the image, rendering edges more apparent for edge detection algorithm. I set a Kernel size of 3 in the provided gaussian_blur() function. 
### Edge detection

 Then Canny edge detection algorithm is applied on the smoothed image. I used lower and upper threshold of 210 and 350 respectively in the provided canny() function. 
 
![alt text][image2]


### Image  masking
Then a region that is likely to contain line marking is selected. I set hard values for vertices of the region. This is a major shortcoming of my approaches as these regions might change from image to image and, as a result my overall lane drawing algorithm may be affected. I could changes the vertices dynamically but I have not found a correct approach to do this. 

![alt text][image3]

### Lane line extraction  and drawing
 Then the Hough algorithm is applied to extract lines segments in the image. 
In order to draw single lane on left and right lanes, the function draw_line() is modified to extract left and right lanes line segments by computing their slopes. The left lane lines segments are fed into a degree 1 polynomial fitting function. The same is done for the right lane line segments. This part is the most challenging in the projects, as the start and end points of the line need to be appropriately selected. And sometimes one lane are not entirely filled with points as it is the case in the image above. Currently the algorithm work fine with degree 1 polynomial, however this cannot solve the optional challenge. Many attempts to use higher degree polynomial or other interpolation functions were unsuccessful, mainly due not effectively selecting the start and end points for line
drawing. 

![alt text][image4]

![alt text][video]

The effective selection of the start end points for lane line drawing and a dynamic selection of the region of interest are my suggestions to obtain good results in the challenge question.






