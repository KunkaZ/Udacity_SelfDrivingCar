# **Finding Lane Lines on the Road**

## Writeup 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[1_grey1]: ./test_image_output/1_grey1.png "Grayscale"
[2_blur]: ./test_image_output/2_blur.png "Grayscale"

[3_canny]: ./test_image_output/3_canny.png "Grayscale"

[4_maskedEdges]: ./test_image_output/4_maskedEdges.png "Grayscale"

[5_lineonBlankPic]: ./test_image_output/5_lineonBlankPic.png "Grayscale"

[6_lineImage]: ./test_image_output/6_lineImage.png "Grayscale"


[7_drawline]: ./test_image_output/7_drawline.png "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

Step 1: Convert the image to greyscale

![alt text][1_grey1]

Step 2: Apply Guassian Blue

![alt text][2_blur]

Step 3: Apply canny algorithm for edge detection to masked image zone

![alt text][3_canny]

Step 4: Use Hough transformation to detect line in mask zone and plot detected line to a blnk image

![alt text][4_maskedEdges]

Step 5: Use re-designed draw_line() function to draw lines on a blank image, can be skipped when processing video

![alt text][5_lineonBlankPic]

Step 6: Draw lines on original image

![alt text][6_lineImage]



### 2. New design for draw_lines()

The new design goal is to find four point(A,B,M,N) which composes two lines (AB,MN). All lines was divided into two group according to its location: left_half, right_half. draw_line function searches in left_half group for A,B point, and searches M,N in right_half group for M,N point. 

After finish iterating all lines, draw_line function will check if points B and M are at the bottom of the image. If not, draw_line function will get new B and N by extending AB and MN to bottom line of the image.

![alt text][7_drawline]


### 3. Identify potential shortcomings with your current pipeline


One potential shortcoming would be  line AB and MN is draw_line could not be perfectly align to the real lane lines when image has some noise near lane lines. 

The reason is when it searches point B or N, the algorithm is searching left most or right most points. Thus if there are some line segments outside of the real lane line then B and N may be updated to wrong points. 



### 4. Suggest possible improvements to your pipeline

A possible improvement would be to use slop check when update B and N to make sure they will not deviate too much.