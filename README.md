# SDC_Notebook_005_HoughTransform
This notebook is the second notebook corresponding to the "Computer Vision Fundamentals" of Udacity's Self-Driving Car Nanodegree, in which we begin exploring the concepts of image processing and computer vision.

When dealing with images, location (x=0,y=0) is in the top left corner of the image (this makes sense when considering the image as a matrix) with y-values increasing downward and x-values increasing to the right. Thus, when considering the image as an x,y-coordinate plane, we can consider the equation of a line on an image (known as "image space") to be the same as we would a typical coordinate plane -- y=mx+b.

With Hough transforms, we translate this line to what is known as "Hough Space", wherein we replace the x and y axis with m and b respectively, leaving us with a single point in Hough Space for every line in an Image Space.

![Hough Space](/images/Hough_Space.png)

Using such as the basis of your intuition, how would we represent two parallel image space lines in Hough Space?

![Parallel Lines](/images/001_Hough.png)

How would we represent a single image space point in Hough Space? (Note that, being a single dot/point, it would have a vast myriad of lines that could traverse through it.)

![Image Space Point](/images/002_Hough.png)

And, two points along the same image space line?

![Two Points](/images/003_Hough.png)

Finally; how would we represent two image space intersecting lines in Hough Space?

![Intersecting Lines](/images/004_Hough.png)

Thus, our strategy to find lines within the image space is to look for intersecting lines within Hough Space. This is done by dividing our Hough Space into a grid and define intersecting lines as all lines passing through a given grid cell. To do this, we first run the canny edge detection algorithm to find all points associated with edges in our image. Then, we can consider every point in the edge-detected image as a line in Hough Space; and, where many lines in Hough Space intersect, we can declare that we have found a collection of points that describe a line in Image Space.

However, we have an issue: vertical lines have infinite slope in m,b representation. Thus, we reparameterize our line to be defined in polar coordinates where Rho is the perpendicular distance of the line from the origin and Theta is the angel away from horizontal.

![Polor Coordinates](/images/sine_Hough.png)

Now, each point in image space correspond to a sine curve in Hough Space.. 

![Image Space Line](/images/sine_Hough_002.png)

If we take an entire line in Image Space, it translates to a myriad of sine curves in Theta-Rho Space with the intersection of the sine curves give the parameterization of the line.

What would the Hough Transform of a square look like?

![Hough Square](/images/sine_Hough_translation.png)

To understand how to code the Hough Transform from scratch, please consider the following [link](https://alyssaq.github.io/2014/understanding-hough-transform/)
