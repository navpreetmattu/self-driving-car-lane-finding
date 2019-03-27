# **Finding Lane Lines on the Road** 

## Writeup Document

### This is a writeup document to describe the working of pipeline created for lane detection with with opencv.

---

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./examples/canny_image.jpg "Canny"
[image3]: ./examples/mask.jpg "Mask"
[image4]: ./examples/clipped_image.jpg "Clipped"
[image5]: ./examples/lines.jpg "Hough Lines"
[image6]: ./examples/weighted_img.jpg "Weighted Image"
[image7]: ./examples/final_img.jpg "Final Image"

---

### Reflection

### 1. Description of pipeline:

My pipeline consisted of 5 steps. First, I am creating the copy of the images, then I converted the images to grayscale. After grayscaling, I am appling Gaussian Blur on the images to reduce the noise factor. Next setp in my pipeline is to apply the canny algorithm on the images to extract all the edges in the images. Then I clipped the desired area by appling a polygon mask on the images. At the end, I applied the Hough Lines algorithm to extract all the points which are detected as the lane lines, highlighted them as red lines and imposed them on the real images. 

In order to draw a single line on the left and right lanes, **I modified the draw_lines() function** by calculating the slope and intercept of all the lines formed by hough lines method, then storing them in different lists based on the sign of the slope (i.e. If slope is negative, the line is on the left side and vice versa). I, then, calculated the mean of both slope and intercept for both left and right lane lines. At the end, to get the co-ordinates of single lines on both sides, I have used the height (or bottom) of the image as *y1* coordinate for starting point and calculated its corresponding *x1* coordinate using equation of line i.e. **y = mx + b**. For the co-ordinates of the ending points, I have used a position 35% before from the starting point to calculate *y2* and calculated the value of *x2* using the above equation. At last, I have created left and right lane lines using the calculated co-ordinates and line parameters (slope and intercept).

### Images to show how the pipeline works:

Converted colored image to grayscale:

![alt text][image1]

Applied Canny Algorithm to extract the edges in the image

![alt text][image2]

The mask image used to get only the required area

![alt text][image3]

Clipped image with only the required lane area

![alt text][image4]

Generated straight lane lines using hough transformation

![alt text][image5]

Fused the lane lines generated using hough transformation with the original image

![alt text][image6]

At last, used average slopes and intercepts to generate single lines for left and right lane.

![alt text][image7]


### 2. Potential shortcomings with current pipeline:


One potential shortcoming of my current pipeline is, it is not able to generate correct lane lines when there road is curved i.e. there is some curvature in the lane. 

Another shortcoming of the pipeline is, it is not able to generate lane lines when the brightness of the image changes radically.


### 3. Possible improvements to pipeline:

There are places where I have used literal pixel values in my pipeline like to get the region of interest. A possible improvement would be to dynamically capture the pixels in the image to generate the lane lines.

Also, If it ignore the change in brightness while generating the lane lines. That would be another potential improvement in the pipeline.
