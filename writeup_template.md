#**Finding Lane Lines on the Road** 
---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)
[image1]: ./test_images/solidYellowCurve.jpg "Yellow Curve"
[image2]: ./test_images/processed_solidYellowCurve.jpg "Yellow Curve Processed"
[video1]: ./white.mp4 "Processed White lanes video"
[video2]: ./yellow.mp4 "Processed Yellow lanes video"
[video3]: ./extra.mp4 "Difficult Conditions video"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of these steps:
1. Convert RGB image to HSV color space. This is apparently better for detecting yellow lanes. (reference: https://thesai.org/Downloads/Volume2No5/Paper%2012-A%20robust%20multi%20color%20lane%20marking%20detection%20approach%20for%20Indian%20scenario.pdf)
2. Apply Gaussian Smoothing to filter noise
3. Apply Canny Edge Detection to extract edges
4. Mask the image to exclude well knows areas that dont include relevant lane info
5. Apply Hough Transform to extract lines in masked image
6. Sort the lines into 2 groups by the slope and position
7. Fit the lines of same slope pair into a single line using liear regression
8. Using linear regression model, draw extracted lines on original image along with interesting Hough lines

## Example Results
![alt text][image1]
![alt text][image2]
![alt text][video1]
![alt text][video2]
![alt text][video3]


###2. Identify potential shortcomings with your current pipeline
- Generic Masking Layer - Identifying a masking layer suitable for different conditions. Especially a mask that include curved roads.
- Curved roads - Need a polynomial fitting instead of linear regression. But line data is too noisy or sparse for polynomial fit. 
- Identifying correct parameters for Hough Transfor and Canny edge extraction steps

###3. Suggest possible improvements to your pipeline
A possible improvement would be to segment the image vertically and process the near and far lanes via separate pipelines.
Near lanes tend to be straighter and more easier to detect.
Far lanes are sometimes filtered out by the common pipeline steps and tend to be curved in some cases.

Another potential improvement could be to have a color mask to filter out edges detected in foliage and road dirt.

Another imporvement would be to detect neighbouring lanes and filter them out from the current lane fitting.
