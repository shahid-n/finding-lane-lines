# **Finding Lane Lines on the Road** 

**Project Objectives**

The goals of this project are as follows.
* Make a pipeline that finds lane lines on the road and renders overlays after some post-processing
* Reflect on the shortcomings of the submitted work, and possible future improvements

[//]: # (Image References)

[marked_img]: ./test_images_output/whiteCarLaneSwitch.jpg "Image with highlighted lanes"

---

## Reflection

### 1. Description of Pipeline

The submitted pipeline comprises the following steps.

1. Conversion of the image to grayscale, followed by Gaussian deblurring
2. Implementation of the Canny edge detection procedure
3. Application of a polygonal mask to focus on the region of interest
4. Connecting the identified edges with Hough lines
5. Splitting the Hough lines into 'Left' and 'Right' groupings, and drawing extrapolated solid lane marker overlays

The `draw_lines()` function was modified to generate best-fit lines using the least squares method -- this can be easily extended in future projects to render curved lane markings by fitting cubic or higher degree polynomials to the Hough lines data instead of straight lines, for example.

The output image below shows an example of the results obtained from the pipeline described above. 

![alt text][marked_img]


### 2. Shortcomings of the Pipeline


It became quite apparent upon observing the output videos -- and especially whilst attempting to process the challenge video -- that the submitted algorithm has various pitfalls, some of which are elaborated here.

1. There is noticeable jitter in the highlighted lane overlays as the video frames advance
2. A polygon mask optimised for a specific video could nevertheless prove to be unsuitable for a different input video stream due to differences in camera location, angle, zoom, panning, etc.
3. This algorithm does not perform well when the lane markers or paths are curved
4. It is also apparent from the challenge video that areas of shadow, reflections -- such as from the bonnet (hood) which dominates the bottom 15 % of the challenge video frames -- or rapid changes in contrast can cause issues


### 3. Future Improvements

Based on personal observations and knowledge gained so far in this class, the following are some improvements that could be made.

* The Project 1 submission is already making use of the least squares curve fitting method, so this could be generalised to render cubic or higher degree polynomials in order to handle curvatures
* An adaptive technique might be employed to handle areas of sharp changes in contrast by varying the Canny threshold parameters
* Similarly, the vertices chosen for the polygon mask may need to be adjusted when progressing from one frame to another -- one way to do this might be to extrapolate the rate of change of curvature of the best fit curves, and if necessary, move the vertices in the next video frame accordingly
