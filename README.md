# **Finding Lane Lines** 

## Project goals

Identifying lane lines with respect to the vehicle using Computer vision approach

## Project steps

Project approach is based on manipulation of a mounted camera (on the front of the vehicle) video input, dealing with each video frame as an image. 

Main idea is the detection of lines as main features of input video using **Hough Transform**, using the following steps:
1 - Converting images to grayscale.
<img src="./imgs/grayscale.jpg" alt="Grayscale Image" width="300" height="170">
2 - Bluring images using **Gaussian blur** to reduce the noise.
3 - Applying **Canny edge** detection to find the Lanes' edges.
4 - Using **Hough Transform** to find the set of points forming Lane edges lines.
<img src="./imgs/line-segments.jpg" alt="Hough Transform" width="300" height="170">
5 - **Averaging/Extrapolation** of two Lane lines segments (Right/Left)
6 - Distinguishing and detection of Lanes by highliting them with Red lines. 
<img src="./imgs/laneLines.jpg" alt="Lane lines" width="300" height="170">

## Pipeline description

pipeline `images_pipeline(image)` returns `lines_img` containing the original Camera video frame blended with detected Lane lines, following sequence of: 
1 - Converting original image to gray scale image using `grayscale(image)`
2 - Detecting lanes edges using `canny(blur_gray, lo_th, hi_th)`
3 - Defining the ROI using vertices declartion and _region_of_interest_
4 - Applying Hough transform using `hough_lines()`
5 - Mixing detected Lane Lines with Initial video frame using `weighted_img()`

### `draw_lines()`

`draw_lines()` function is used to differentiate between left lane and line lane segments based on their slope. Slope of `hough_lines()` points is calculated then stored in positive/negative slope arrays _(pos_x, pos_y)_, _(neg_x, neg_y)_. `np.polyfit` is used to fit a line passing through positive _pos_lane_poly_ and negative _neg_lane_poly_ slope points. Extrapolation is done using `cv2.line` to apply the averaged line through desired ends of the lanes.

### Basic Build Instructions
The jupyter notebook _main.ipynb_ is containing necessary routines. The camera output is located in path _./test_vids_  and output will be generated in path _./test_vids_out_.