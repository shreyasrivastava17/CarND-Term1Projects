# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg
[image2]: ./test_images_output/solidWhiteRight.jpg
[image3]: ./test_images_output/solidYellowCurve.jpg
[image4]: ./test_images_output/solidYellowCurve2.jpg
[image5]: ./test_images_output/solidYellowLeft.jpg
[image6]: ./test_images_output/whiteCarLaneSwitch.jpg

### Reflection
### 1. Pipeline Description:
  * **My pipeline consisted of 5 steps:**
    * **Step 1:** Converting the images to grayscale.
    * **Step 2:** Applying Gaussian Blur on gray scaled image to smoothen out the image given so that it eliminates the spurious gradients by averging
    * **Step 3:** Appliying canny edge detection to detect the edges in the image obtained after gussain blur.
    * **Step 4:** Masking the region of interest on the canny edge detected image. I have taken a polygon a the region of interest for the given set of images
    * **Step 5:** Applying hough transform on the canny edge detected image in the region of interest to find the lane lines
    * **Step 6:** Extrapolating the lines detected in the hough transform to draw continuous lane lines.
  * **In order to draw a single line on the left and right lanes, I modified the draw_lines() function in the below mentioned way:**
    * For extrapolating the lines obtained by hough transform I have taken the mid point of the image to segregate the left lane lines and the right lane lines. For each line in the lines obtained as a result of hough transform I have taken the x and y coordinates in an array and then passed it to the polyfit function of numpy to find the coeficints of the line fromed by the x and y coordinates. Then i have calculated the min and max values of the x coordinates and the substituted the values in the equation y = m*x+c to find the y coordinates. Now as we have the min and max value of the x and y coordinates I have drawn a line using cv2.lines function. elow are the images obtained after extrapolation of the lines.
    * If in case there is a frame in which no lane lines are identified after applying hough transform then i have taken the value of the just previous frame to draw the line in thhe current frame. For taking the value of the previous frame i have stored the values in global varibales and then used them to draw the lane lines if no lane liness are detected in a particular frame
  
![alt text][image1] ![alt text][image1]2![alt text][image3] ![alt text][image4] ![alt text][image5]


### 2. Identify potential shortcomings with your current pipeline
* One potential shortcoming is that i have takeninto consideration only the just previus frame to find the values to draw the lines in case no lines are detected in the frame. 
* Secondly the pipeline will only be able to detect the straight lane lines and not the curved lane lines. 

### 3. Suggest possible improvements to your pipeline
* A possible improvement would be to thake the average of about 5-10 prevoius frames in case no line is detected in a particular frame and the draw a line in that frame.
* Second possible improvement can be the use of other colur channnels apart from RGB so that the lane lines can be detected even if the are some bad frames where the colour of the lane lines is not same all along or there are some conditions due to which thecolour changes.
* Third possible improvement can be dynamically chossing the region of interest as and when the car is moving on the raod and not hardcoding the region of interest.
