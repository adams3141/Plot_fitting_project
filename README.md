# Plot_fitting_project

************************************************
The main program is main.py. This is the program launcher that adjusts the function when the sample image is loaded.

The next programs are Axis_looker.py with axillary rotate_bound.py. The secondary
program for further analysis is data_read.py.

**Axis_looker** takes as an argument path to an image and returns an array
of four arrays each containing image, x coordinate of central point of
the plot, y coordinate of centre of plot. The programme finds all lines
(using Hough lines transformation) on the image and selects
the longest perpendicular as an axis then propagates the image and found axes to
rotate_bound which output of rotated images is then returned.

**Rotate_bound** find crossing points of axes and angle of rotation from vertical
-horizontal position. The crossing point of axes is a point around which the image
is then rotated using an appropriate rotation matrix. Rotate_bound returns
an array of four arrays containing rotated images and central points
(with already rotated coordinates).

**data_read** takes 3 arguments image, x and y coordinates of the crossing point
of axes and returns image and coordinates of plot function points. Program converts copy of the image to grey scale then masks all points
in specific grey scale (get rid of bright colour points). Then reads all
remaining points position apart of points around axes. Later it dots
the original image at all found points blue and then returns an array consisting
of an image and a list of plot points.
*****************************************************************
-----------------------------------------------------------------
How to use the program?

1. Go to the main folder,
2. Run main.py in python (./main.py),
3. Load a picture from the examples folder,
4. Enjoy the program and its results.

----------------------------------------------------------------

DataRead
=========


Packages
--------
We are using:

NumPy <https://numpy.org/>

OpenCv <https://docs.opencv.org/4.x/d6/d00/tutorial_py_root.html>

math <https://docs.python.org/3/library/math.html>.

Convertion to gray and masking
------------------------
Image is converted to gray scale and then using OpenCv bitwise_and <https://docs.opencv.org/4.x/d0/d86/tutorial_py_image_arithmetics.html>,
program show only points from certain gray scale.


Coordinates of data points
--------------------------
Then remaining points coordinates are then saved using OpenCv findNonZero, but points
close to axes are excluded.
Then the rotated image is ploted with blue dotes in position of saved coordinates.



RotateBound
==========


Packages
--------
We are using:

NumPy <https://numpy.org/>

OpenCv <https://docs.opencv.org/4.x/d6/d00/tutorial_py_root.html>

math <https://docs.python.org/3/library/math.html>.

Find the cross point of the axes
------------------------
Using edge points of lines program determines if axes need rotation (check if one is vertical)
 and finds crossing point of axes and angle of rotation.


Rotation of image
-----------------
New width, height and center point are calculated. Finally using OpenCV
getRotationMatrix2D  and warpAffine <https://docs.opencv.org/3.4/d4/d61/tutorial_warp_affine.html>
rotation is made. Note that there are 4 possibilities of correct rotation each of them
is tilted by multiplicity of 90 degres from another. Function returns array of four array
each containing image and point of axes crossing after rotation.


Axis looker
==========


Packages
--------
We are using:

NumPy <https://numpy.org/>

OpenCv <https://docs.opencv.org/4.x/d6/d00/tutorial_py_root.html>

math <https://docs.python.org/3/library/math.html>.

HoughLinesP
-----------
The program load an iamge, then detects edges and convert it to a gray scale
using cv2.Canny<https://docs.opencv.org/4.x/da/d22/tutorial_py_canny.html>.
Then using OpenCv HoughLinesP <https://docs.opencv.org/3.4/d9/db0/tutorial_hough_lines.html>
program detects and stores lines. (Note that program uses probabilistic Hough transform)
For machine resources resons algoritm only work if HoughLinesP didn't detect
too many lines. If this happend You may manually change treshold for detection
in HoughLinesP or increase accepted number of lines.

Search for perpendicular lines
------------------------------
In teh next step program checks the lines, looking for pair of perpendicular
lines and simulanously chacking if the line isn't image boundary. The perpendicularity is
checked using scalar product. Axes are chosen as longest (sum of lenghts of lines)
perpendicular line pair. Then the lines with original image are forwarded to rotate bound.
