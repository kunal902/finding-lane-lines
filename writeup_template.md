# **Finding Lane Lines on the Road** 

### Reflection

My current pipeline is as follows :

1. First, I filtered the yellow and white colrs from the image by keeping only these colors and blacken out other pixels
2. Then I apply gaussian blur to reduce noise with a kernel size of 5 on the image got in step 1
3. Then I detected the edges by canny edge detection algo with a lower threshold of 120 and upper threshold of 240 on the image got in step 2
4. Then I applied a polygonal mask to extract the region of interest from the image got in step 3. In this case I took the bottom width of the polygonal mask to be 90% of the total image width, top width to be 1% and height to be 40% of the image height.
5. Then I applied probabilistic hough transorm to extract the line segments from the image got in step 4
6. Finally I added the initial image and the image got from step 5

Note: I also modified the draw_lines() function to draw the left and right lane lines got from step 5(i.e probabilistic hough transform). Below are the steps for the same:
1. First I got all the lines in an array of tuples of points using hough transform
2. Then I defined a slope threshold of 0.5 and considered only those lines whose absolute slope value is greater than 0.5
3. Then I classified the lines array got from step 2 into left lines array and right lines array depending on their slope values. +ve slope means the right line and -ve slope means the left line
4. Then I ran linear regression on the set of right and left lines array got in step 3 to find the slope(m) and constant(b) values for the right and left line
5. Finally after I got the m and b values for the left and right lines I drew the lines by taking the initial y value to be the bottom the image and the final y value to be 40% of the image height


### Potential Shortcomings

One potential shortcoming would be when the car is getting driven in varying weather and daylight conditions or even in heavy traffic where the lane lines will not be clearly visible

Another shortcoming could be what happens when the road curves sharply as it draws only straight lines for the left and right lanes. In such cases extrapolating straight lines might not work

Another shortcoming would be since I am filtering only the yellow and white region from the image in step 1 considering that the lane lines would always be of these two colors so the algo will fail if the lane lines is of some different color

Another shortcoming would be since I am using a polygonal mask to extract the region of interest with fixed assumptions so the camera position is important and should not fluctuate


### Possible Improvements

A possible improvement would be to have more datasets to work on by considering various parameters such as weather, lighting conditions, land forms, traffic, speed of the car and then improve further as current implementation is overfitting the datasets
