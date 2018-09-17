# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./test_images_output/solidWhiteCurve_Image.jpg "Original Image"
[image3]: ./test_images_output/solidWhiteCurve_Grayscale.jpg "Grayscale Image"
[image4]: ./test_images_output/solidWhiteCurve_Gaussian_Blur.jpg "Blurred Image"
[image5]: ./test_images_output/solidWhiteCurve_Canney_Edge.jpg "Canny Edges Detected"
[image6]: ./test_images_output/solidWhiteCurve_Masked_Edges.jpg "Mask Applied"
[image7]: ./test_images_output/solidWhiteCurve_lines_highlighted.jpg "Detected Lane Lines Highlighed Over Original Image"
[image8]: ./test_images_output/solidWhiteCurve_extrapolated_lines_highlighted.jpg "Extrapolated Lane Lines Over Original Image"




---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale; second, I applied gaussian smoothing filter; third, I detected the canny edges; fourth, I applied a mask to isolate the region of interest in the image; fifth, I applied a hough transform to isolate lines in the image; and sixth, I extrapolated the left and right lane lines. 

With the following image, I applied the pipeline.
![alt text][image2]

Starting with converting the image to grayscale at step one, and finally extrapolating the left and right lane lines, the pipeline steps are shown in the following images.
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]
![alt text][image7]
![alt text][image8]


In order to draw a single line on the left and right lanes, I created a new modified the draw_lines() function. This function took the following inputs: the vector of lines created from the hough transform function as well as the masked image from pipline step 5. The function seperated lines belonging to the left and right lanes by slope (negative slope -> right lane, positive slope -> left lane). Then using each lane line was approximated using a least squares polynomial fit function on the grouped left and right lines. Lastly each lane line was scaled to fit within an appropriate region in the image. The image corresponding to step 6 in the pipeline shows the approximated line result. 


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when images with varrying lighting conditions are put through the pipeline. This can be seen if the current pipeline is run through the challenge video. Additionally this pipeline assumes the car is centered in the lane when determening the lane line. If the car were to swith lanes, the pipeline would not accurately determine the lane lines. Furthermore, lanelines are approximated to be straight here, when in reality they can be curved. 

Another shortcoming could be that the pipeline only works well if the medium between the lane lines is a consistant color. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use HSV instead of grayscale for detecting canny edges. This would help account for changes in lighting on the road.

Another potential improvement could be to incorporate probability to the location of the lane lines for each camera frame. This could help elimnate contributins from noise or random inconsistances due to the image or elsewhere. 

Hopefully, I will learn how to improve this pipeline in the next lesson. 
