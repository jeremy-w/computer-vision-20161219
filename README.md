# Computer Vision
- Unclass: Week of 2016-12-19
- Jeremy W. Sherman

This repo is a dumping ground for notes taken during a week of studying computer vision. The initial charter for the week is the (private) [Unclass Proposal](https://docs.google.com/document/d/13MCtXiMF2NgKTjGpvNBzbgVnCuvsAP6-9niB_LAs9U0/).
This file is primarily a daily log.

## Contents
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Computer Vision](#computer-vision)
  - [Contents](#contents)
  - [Resources](#resources)
  - [2016-12-19 (Monday)](#2016-12-19-monday)
    - [The Chosen Textbooks](#the-chosen-textbooks)
      - [OSA](#osa)
      - [PCV](#pcv)
      - [CCV](#ccv)
    - [Mapping Out Concepts](#mapping-out-concepts)
    - [Setting Up Jupyter](#setting-up-jupyter)
  - [2016-12-20 (Tuesday)](#2016-12-20-tuesday)
    - [Histogram Discretization](#histogram-discretization)
  - [2016-12-21 (Wednesday)](#2016-12-21-wednesday)
    - [Chapter 2: Local Image Descriptors](#chapter-2-local-image-descriptors)
    - [Chapter 3: Image to Image Mappings](#chapter-3-image-to-image-mappings)
      - [Homographies](#homographies)
        - [Aside: Homogeneous Coordinates](#aside-homogeneous-coordinates)
      - [How We Transform](#how-we-transform)
      - [Corresponding Points Determine an Homography](#corresponding-points-determine-an-homography)
      - [Points Are Chosen to Minimize Error](#points-are-chosen-to-minimize-error)
      - [Applications: Image Registration, Panoramas](#applications-image-registration-panoramas)
  - [2016-12-22 (Thursday)](#2016-12-22-thursday)
    - [Chapter 4: Camera Models and Augmented Reality](#chapter-4-camera-models-and-augmented-reality)
      - [Pinhole Camera](#pinhole-camera)
      - [Working Backwards from P to K, R, t](#working-backwards-from-p-to-k-r-t)
      - [Working Backwards from P to the Camera's 3D Position](#working-backwards-from-p-to-the-cameras-3d-position)
      - [Camera Calibration](#camera-calibration)
      - [Pose Estimation](#pose-estimation)
      - [OpenGL Goop](#opengl-goop)
    - [My Reactions to Computer Vision So Far](#my-reactions-to-computer-vision-so-far)
  - [2016-12-23 (Friday)](#2016-12-23-friday)
    - [Chapter 5: Multiple View Geometry](#chapter-5-multiple-view-geometry)
      - [Epipolar Geometry](#epipolar-geometry)
      - [Cameras, 3D Structures, Oh Yes](#cameras-3d-structures-oh-yes)
      - [Multiple View Reconstruction: Structure from Motion](#multiple-view-reconstruction-structure-from-motion)
      - [Stereo Images and Stereo Reconstruction (AKA Dense Depth Reconstruction)](#stereo-images-and-stereo-reconstruction-aka-dense-depth-reconstruction)
    - [Chapter 6: Clustering Images](#chapter-6-clustering-images)
      - [K-Means Clustering](#k-means-clustering)
        - [Code: SciPy Clustering Library](#code-scipy-clustering-library)
        - [Images](#images)
      - [Principal Components Visualized](#principal-components-visualized)
      - [Hierarchical Clustering](#hierarchical-clustering)
  - [Chapter 7: Searching Images](#chapter-7-searching-images)
  - [Chapter 8: Classifying Image Content](#chapter-8-classifying-image-content)
    - [Visualizing](#visualizing)
    - [Classifier: K-Nearest Neighbors](#classifier-k-nearest-neighbors)
    - [Featurifying Images: Dense SIFT, AKA Histogram of Oriented Gradients](#featurifying-images-dense-sift-aka-histogram-of-oriented-gradients)
    - [Classifier: Bayes](#classifier-bayes)
    - [Classifier: Support Vector Machines (using libsvm)](#classifier-support-vector-machines-using-libsvm)
    - [Multi-Class Example: Sudoku OCR using libsvm](#multi-class-example-sudoku-ocr-using-libsvm)
  - [2016-12-24 (Saturday)](#2016-12-24-saturday)
  - [2017-01-02 (Monday)](#2017-01-02-monday)
    - [Chapter 9: Image Segmentation](#chapter-9-image-segmentation)
      - [Graph Cuts](#graph-cuts)
        - [User Input](#user-input)
      - [Finding Normalized Cuts and Clustering](#finding-normalized-cuts-and-clustering)
      - [Variational Methods](#variational-methods)
    - [Chapter 10: OpenCV](#chapter-10-opencv)
      - [Basics](#basics)
      - [Tracking](#tracking)
      - [Lucas-Kanade Tracking](#lucas-kanade-tracking)
      - [Grab Bag](#grab-bag)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->



## Resources
Useful resources I didn't know about before.

- [Anaconda package docs](https://docs.continuum.io/anaconda/pkg-docs)
- [NumPy Reference](https://numpy.readthedocs.io/en/latest/reference/index.html)
    - Basically its own little world. The F2Py docs' existence is pretty
      telling, I think!
- [Matplotlib Docs](http://matplotlib.org/contents.html)
- [Hypermedia Image Processing Reference](http://homepages.inf.ed.ac.uk/rbf/HIPR2/hipr_top.htm)


## 2016-12-19 (Monday)
- Created repo for the week: [jeremy-w/computer-vision-20161219](https://github.com/jeremy-w/computer-vision-20161219)
- Reviewed the texts I have on hand for the week.
    - Pivoted from *OpenCV for Secret Agents* as main driver to *Programming Computer Vision with Python* (mostly referred to as "PCV")
      - This change surprised me!
- Started mapping out some of the vocabulary and concepts of computer vision
- Set up a Jupyter notebook for experimenting with Python computer vision stuff
  in
- Started working through PCV chapter 1 using a notebook, but didn't get super
  far


### The Chosen Textbooks
Aside from *OpenCV for Secret Agents* ("OSA"), I'm also using:

- Jan Erik Solem's *Programming Computer Vision with Python* ("PCV")
- Reinhard Klette's *Concise Computer Vision: An Introduction into Theory and Algorithms* ("CCV")

The hope is that these three rather different approaches to the same topic will allow me to triangulate the discipline and get a decent feel for the actual ideas vs just a single presentation of them.


#### OSA
I skimmed through OSA when I first got it and marked up the TOC with topics and dependencies between chapters.

The book is very project-focused; instructional material is rather limited, and though the author does attempt to provide a commonsense explanation of how something works, it's mostly library calls. This is good for seeing tooling, standard glue, and what sorts of things one can do, though!

And high-level intuition sufficient to use existing library code is what I'm trying to build up, because realistically, I'm unlikely to be implementing computer vision primitives from scratch – that's not where my focus lies.

That said, the tooling I'd be likely to use would be a bit different, since I'm a primarily iOS developer. But I view making the conversion to that different environment as a very useful check of understanding.

Weak points:

- Variety of environments means more time spent on environment setup (all of
  chapter 1!) and other explanatory scaffolding. Unity/OpenGL, wxPython, RPis,
  oh my.
- Project focused over theory focused, possibly to a fault.

Chapter relationships:

- 1 is just reference - env setup/install
- 2 introduces classifiers and color histogram analysis, which feeds into
  3 doing supervised training and face detection & recognition, feeds into
  4 doing face gesture recognition (nod, shake) and optical flow
  - wxPython, SciPy, and OpenCV
  - Android apps
- 5 (blob detection, distance estimation, for headlight detection) is used by 7 (canny edges, Hough lines, more blobs, for simulating a pen/paper sketch)
  - RPi
  - Unity + OpenGL
- 6 (seeing a heartbeat - CV meets DSP - I/FFT, image pyramids) stands alone
  - Another Android app

I think the more interesting bits are:

- Face recognition and optical flow
- Turning a sketch of a ball-and-maze puzzle into something you can execute
  (SO COOL!)

I would be happy to pull both those off and maybe turn them into blog posts.

**Now that I have all the books in hand, and contrary to my original plan,
I think my main focus should actually be on PCV, though, with supplementation
from CCV, so as to better understand the field as a whole.**


#### PCV
Fancy that: Author used the same abbreviation.
See [code here](https://github.com/jesolem/PCV).

The author makes available a
[final pre-production draft of *Programming Computer Vision*](http://programmingcomputervision.com/) for free. You can get the 50 megs of project data from there, too.

The first chapter focuses on glue (reading in images, converting to and from numpy arrays) and some basic tools for image cleaning and prep (histogram equalization, averaging images, principal component analysis, etc). It goes a bit quickly in that I can't mentally model some of the array transforms yet, and the intermediate results aren't sketched out. Ran into this first with the histogram equalization example.

This book looks a lot less project-focused but a lot better at covering the breadth of the field and orienting you to it. This might be a better book to focus on.

The Image Datasets appendix looks pretty handy, too.

**Unlike OSA, chapters look mostly independent of each other.**


#### CCV
This is a legit textbook, rather than the kinda popular techpress stuff the other ones are. (Yeah Springer Verlag! Oh yeah.)

Exercises are intentionally not coupled to implementation details, and even allow for freedom in inputs and details of the problem (like, can you pick a region that hits an edge, or is it always a square region fully contained in the image?).

This aligns rather closely with PCV in topic selection and even ordering, though with a lot more detail, depth, and math, and a lot less focus on tooling and implementation.


### Mapping Out Concepts
This sounds like a job for MindNode.


### Setting Up Jupyter
Going to go the Anaconda route, because NumPy and SciPy and stuff are kind of
a pain.

https://www.continuum.io/downloads offers Py3.5 or Py2.7 versions as "home"
version. You can switch to the other as well. I know the book I have says to
use 2.x based on lack of availability of some of the stuff under 3.x at the
time.

Looks like it has everything I need. OpenCV builds look like they're moving to
3.x as well / already have. Ah, well - the book I was looking at was published
in 2012. So, there's that.

Anaconda uses Pillow (a fork) rather than PIL itself. Also has a variety of
other nifty libs likely worth looking at for scientific / numeric Pythoning.

And another half a gig of storage gone for the installer. Oh well!

Installs all the binaries under ~/anaconda/bin/. Can add to path, or not.

Running it from the directory in its own tmux window. Had to tweak
RequestPolicy and NoScript to let its JS run, but then it worked fine. Looks
like I can manage the Conda packages installed via Jupyter, too - nifty!

The notebook file format is JSON. Handy. The .ipynb_checkpoints folder looks to
contain old versions of the notebooks, presumably for undo support. All just plaintext, which is nice.

Similarly, Jupyter writes some stuff to ~/Library/AppSupport/Jupyter describing
where it's running and with what state (local directory), as well as a private
client cookie (base64, looks like a certificate or privkey).

Got confused for a bit - wrote some code depending on a change I'd made (but
not yet run!) in an earlier cell, and then got an error about that new name not
showing up. **Need to manually kick cells to re-evaluate - they aren't live.**

Run All is your friend - which probably suggests I want to break out one
notebook per chapter!



## 2016-12-20 (Tuesday)
- Worked through histogram equalization and visualized each step to understand
  the effect.
    - Confused by why result not flat. Turns out the issue is discretization.

- Finished reading chapter 1 of PCV
    - Didn't work the exercises yet, though.

- Found an interesting bit of history about one of the standard images used
  with image compression and other image-processing work, kinda like the
  field's version of the Utah teapot, the Lena image
    - https://www.cs.cmu.edu/~chuck/lennapg/lenna.shtml


### Histogram Discretization
Why is it not flat? I'm not the first person to ask that.

https://www.quora.com/Why-is-the-histogram-of-an-image-not-flat-after-applying-histogram-equalization

> In the continuous domain (used during the conceptual discussion of the
> process in most books), there is an infinite number of values in any
> interval.
>
> In reality (i.e., when working with digital images), the histogram is
> discrete which means there is a fixed number of values in a range. When this
> range is stretched, the number of values in it is maintained. The discrete
> equalization process merely remaps one intensity value to another; it does
> not redistribute the intensity values. This means pixels which have equal
> intensities will still have equal intensities after the process.
> (Girish Mallya, 19 Feb 2016)

http://www.math.uci.edu/icamp/courses/math77c/demos/hist_eq.pdf



## 2016-12-21 (Wednesday)
- Looked a bit more into convolution.
    - http://www.songho.ca/dsp/convolution/convolution.html
      - Notion of separable convolution looks useful for compactly noting many
        convolution matrices used in image processing. Also explains the
        frequent symmetry encountered, I think - speed hack!
    - https://en.wikipedia.org/wiki/Convolution

- Switched to skimming text after determining that the algorithmic details are
  not terribly portable (you tend to use optimized impls wherever already
  available), and it would be easy to spend a ton of time fumbling around with
  matrices (because everything is at arm's length - it's matrices all the way
  down).

- Skimmed chapter 2, Local Image Descriptors.

- Skimmed chapter 3, Image to Image Mappings.

- Skimmed chapter 4, Camera Models and Augmented Reality.
    - Will have to write notes tomorrow.

- TODO: Skimmed chapter 5, Multiple View Geometry.
    - Brief flip-through: Lets us drop need for planar object matching to be
      able to estimate camera position.


### Chapter 2: Local Image Descriptors
We often want to find "interesting" points/regions in an image. For this, we
use a feature detector. Examples are the Harris corner detector and the
Scale-Invariant Feature Transform (SIFT).

We also often want to _match_ features across images by finding corresponding
features. This gives us a basic building block towards answering questions
like:

- Which of these images were taken from the same point?
- Which of these images are the same image?
- How similar are these two images?
- Are these pictures of the same thing?

This matching is done by comparing _feature descriptors_ which capture
information about a feature. Generally a feature descriptor is paired with
a feature comparison. Examples:

- Gray levels in an image patch around the interest point, compared using normalized cross-correlation
    - The normalization cuts out the effects of image brightness.
- Difference of Gaussians (blurs and diffs) for position and scale combined
  with image gradient for rotation, compared using 8-bin histograms of image
  gradient orientations, both across the whole region and across 4x4
  subregions, all concatenated together
    - This fanciness comes from SIFT. Clever, eh?

As a quick "toss out the bad matches" approach, you can do a *symmetric match*:
compare from image A to B and also compare backwards from B to A, then only
keep the matches that agree when matching in both directions.

End of chapter teases we can do a better job of more robustly matching images
by using ideas developed in the next couple chapters, Image-to-Image Mappings
and Camera Models. Presumably, you can then assess whether the image *in toto*
matches, bearing in mind how cameras work.


### Chapter 3: Image to Image Mappings
How do we transform one image relative to another?
How do we compute a specific transformation?

#### Homographies
This chapter considers _homographies_ between planes. It uses *homogeneous
coordinates* to represent image samples, and matrices to represent
transformations.

##### Aside: Homogeneous Coordinates
Tacking on a homogeneous coordinate to each sample enables representing
projective transforms, not just affine (rotate, scale/reflect, and translate)
transforms, as a single matrix. But it also means that our "points" become
scale-independent. To allow talking about a single point again, we often
normalize a homogeneous point so that the perspective value *w* becomes 1.

#### How We Transform
These transformations support warping one image next to/over/on top of another.

But what transformation should we use? And how do we build that transformation
matrix, anyway?

#### Corresponding Points Determine an Homography
A projection matrix has eight degrees of freedom. So, we can specify one by
picking out four corresponding points in both images, and then computing the
transformation that will align those points.

(An affine matrix has six degrees of freedom, so we need only pick three
points. This is handy combined with a triangulation of feature points and
piecewise affine warping, AKA "paint it with a triangle mesh". Graphics cards
eat that stuff up.)

#### Points Are Chosen to Minimize Error
So we can go from "these points should line up" to "here's your homography".
But what points should line up?

We have the start of an answer from the last chapter, on local image
descriptors and feature detection. We can run SIFT to get a pile of
probably matching points. But then we only get to pick four to determine the
homography.

One approach is to pick the four that minimize the error between all the other
corresponding points. The chapter runs through two major approaches:

- Direct Linear Transformation: Squish the from and to points into a matrix
  in a certain way, run the matrix through the singular value decomposition,
  then strip off and reshape the bottom row of V. (Too many reasoning steps are
  elided to actually understand why this works.) But
  [Wikipedia agrees this
  works for least-squares](https://en.wikipedia.org/wiki/Singular_value_decomposition#Total_least_squares_minimization) -
  "The solution turns out to be the right-singular vector of A corresponding to
  the smallest singular value."
    - SVD is neat - it's a kind of generalized eigendecomposition that is
      apparently useful for all kinds of things. It spits out (U, S, V) = M,
      where U is mxm, V is nxn, and S is mxn, and M is also mxn. S is diagonal,
      and its diagonal values are the *singular values.* In a 2-D plane, it
      ends up being a rotate, scale, rotate again kinda thing, with the
      singular values corresponding to the major and minor axes of the ellipse.
    - Worth remarking on in the code is how it conditions and normalizes the
      inputs before running them through SVD, so as not to mess up its numeric
      stability, then undoes that transform on the resulting homography.

- Random Sample Consensus, more often called RANSAC: An iterative model fitting
  method that relies on an error estimate to try to single out inliers from
  outliers and fit against only the inliers. This is more robust to noise.
    - This is what the chapter actually uses for working out how to warp
      images together into a panorama.

#### Applications: Image Registration, Panoramas
One common use of homographies is _image registration_, which warps images to
share a common coordinate frame. (The warp might be rigid, or not.) This is
usually a data cleaning step prior to running some sort of statistical analysis
or other machine learning method against a training set, and the chapter shows
how much it improves the output of a simple mean image calculation as well as
a principal component analysis with a series of face images, even though the
starting images are pretty darn aligned to begin with.

You can also use homographies to glue a sequence of images together
in order to create a panorama.



## 2016-12-22 (Thursday)
- Wrote up notes on chapter 4, Camera Models and Augmented Reality.

- Read chapter 5, Multiple View Geometry.


### Chapter 4: Camera Models and Augmented Reality
Homographies handle 2-D mapping between images. But to deal with 3-D, we need
to also model how that 3-D reality becomes a 2-D image. It turns out that
a simple, pinhole (aka projective) camera model suffices for most needs, so
that's what's covered here.

Once we understand how to model projection, we can build on a homography
between two images to also map between the cameras used to take the two images,
which allows us to insert custom 3-D content into an image as if it had
actually been there. That's right: Augmented reality!

The augmented reality tactics in this chapter rely on starting with
a homography, and specifically, they rely on having a rectangular patch that
can be matched in both images, like a book cover or a window.


#### Pinhole Camera
Kind of funny - you can derive most of this from a clear sketch using similar
triangles, I think. But the way it's sliced up here differs from OpenGL in
meaningful ways.

Here, the camera matrix is split up as a matrix product of a calibration matrix
*K* and a horizontal stack of a rotation matrix *R* and a translation vector
**t**: *P* = *K* [ *R* | **t** ].

- P: projection matrix
- K: calibration matrix
- R: camera orientation
- t: center of camera position
- [ R | t ]: known as a whole as the camera's *pose*

The calibration matrix is upper triangular with support for modeling:

- skew of the sensor's pixel array (generally assumed to be 0)
- focal length, the distance between the image plane and camera center,
  apparently measured in pixels based on some later stuff
    - this depends on the image resolution, orientation, and specific camera!
    - the orientation only matters if you don't have square pixel elements,
      otherwise, you get to ignore that bit
- optical center aka principal point: where in the image the camera's optical
  axis intersects the image plane, again in pixels
    - this is generally the middle of the image, so the location just gets set
      to half the image's width and height


#### Working Backwards from P to K, R, t
- RQ-factorize the first three columns of P to get K and R
    - Confusing: The R in RQ is not the R in the KR associated with P,
      but is a Right upper-triangular matrix rather than a Rotation matrix.
- Get t by taking that last column *C* of *P* and undoing *K*'s effect on it,
  **t** = *K*<sup>-1</sup> *C*
- There's some cleverness here about forcing R to have positive determinant
  to avoid flipping the coordinate access by introducing a transform that's
  its own inverse and doing P = K T T [ R | t ].


#### Working Backwards from P to the Camera's 3D Position
We turn out to be hunting for a column vector **c** such that
*P* **c** = **0**. Some pushing around gives us
**c** = - *R<sup>T</sup>* **t**.


#### Camera Calibration
So, K. That depends on your camera. And you can measure it yourself!

This goes back to that similar triangles idea. You can measure the real-world
dimensions of a rectangle, measure the distance from your camera to the
rectangle, center it and set your camera parallel to it, snap a photo, then
measure the sides of the rectangle in the image in terms of pixels. Now you can
estimate the focal lengths by taking the pixel:actual length ratio for each
side and multiplying by the distance.

You can then make your life easier by taking the mean of fx and fy on the
assumption you messed something up and you really have square pixels in your
sensor. Your calibration still depends on the camera and image resolution then,
but not the camera's orientation any more.


#### Pose Estimation
Here's where we do that homography to camera position thing to let us
map a 3D object from from-space into to-space.

Knowing a homography H and calibration matrix K, we can gin up an arbitrary
projection for our from-space assuming no rotation and a translation that
sticks the camera above the marker (z = -1).

H already handles transforming points at z = 0 for us to to-space.
We can also apply it on top of our projection matrix to get us most of the way there - our new projection matrix P2 for to-space now handles z = 0.

To handle z, we can grab the KR chunk of P2, undo K to get us most of the way
to R2, then fix up its third column by setting it to a cross product of the
first two columns.

- NOTE: I didn't quite follow why the cross product, and the book doesn't
  explain. My best guess is that it ensures we get something perpendicular to
  the x and y rotation bits of R, and since R is unitary, we don't see any
  stretching (unit distances, unit volumes).

Anyway, we now have a projection for a camera in the to-space, and we can
take a 3D model, run it through the projection, and have it pop out in to-space
for rendering over our image. (We're still assuming everything in the image
is at Z=0, so this isn't mega sophisticated, but it's enough to land a toy
airplane on a book!)


#### OpenGL Goop
I'm not going to bother summarizing this. It's using older fixed-function pipeline OpenGL. Interesting bits:

- The projection matrix is basically the calibration matrix.
- OpenGL assumes the camera is at z=0, so the model-view transform needs to
  stick stuff at z > 0 to be seen.
- OBJ object files and MTL texture/material files are basically just text.
  Funky.



### My Reactions to Computer Vision So Far
Ouch, mush brain. Much technical. Very matrices.

What's amazing to me – and kind of obscured by the presentation here – is how
intuitive a lot of this is, given a relatively simple model of a camera and
scene.

The details get bogged down in numeric concerns on the one hand and coping with
imperfections and noise on the other. We prefer minimizing least-squares error
using SVD to solve Ax = 0 rather than any sort of analytic approach, and we
accept that we might not actually wrangle a 0 out. We have to worry about
numerical precision and error accumulation – though the mitigations are rule of
thumb added bookkeeping; we're not actually bounding the error term!

Then there's a further complication as algorithms get more elaborate.
We might layer steps and tune parameters - use a noisy disparity estimate and
then tack on a denoise step afterwards, so we get sharp edges without a bunch
of noise in each field.

I also failed to understand how tied together the chapters are. This first
sequence very much builds throughout. It looks like there's a Part 2 where we
look at clustering and search and similar machine learningy things, and then
a one-chapter Part 3 about OpenCV and applications to video frames.

But I'm not sure where the image segmentation chapter sits relative to the
rest, so, I could be wrong about that grouping!



## 2016-12-23 (Friday)
- Wrote up notes on Chapter 5, Multiple View Geometry.
- Read and wrote up notes on:
    - Chapter 6, Clustering Images
    - Chapter 7, Searching Images
    - Chapter 8, Classifying Image Content


### Chapter 5: Multiple View Geometry
Chapter 4's techniques let us work out where the camera was relative to an
image, but we were still left treating it as just a 2D image, with only the
camera (and anything we wanted to project into the scene à la AR) off in 3D.

This chapter gives us the tools needed to unflatten the image and reconstruct
features' locations in 3D.

*Multiple view geometry* looks at what you can work out about cameras and
features, given photos of the same scene from one or more cameras.

The heart of it is relating two views of the same scene. Once we can do that,
we can build up to working with more views of the same scene on the one hand,
or look at a simpler case of two views with mostly known relationships, in the
form of a stereo rig.


#### Epipolar Geometry
Epipolar geometry uses the epipolar constraint to derive the **fundamental
matrix** relating the two cameras and the points viewed through them.

From the fundamental matrix, we can recover the camera matrices.
This can only be done up to projective transformation, which means that not
even angles and such might be preserved.
If we know the calibrations, though, we can achieve a metric reconstruction,
which has correct distances and angles, though the scale remains unknown.

If you plug a feature point from one image into the epipolar constraint,
you get back the equation of a line, the *epipolar line*, corresponding to the
chosen point. We know that any corresponding feature in the other image must be
on this line, which we can use to simplify hunting for correspondences.

All epipolar lines intersect in a point called the *epipole*, which is actually
where the image plane intersects the line between the two cameras (and has
a good chance of actually being outside the frame of the image!).

We can compute the fundamental matrix F using the eight-point algorithm,
which relies on eight point correspondences. (This uses a neat trick where
we force F to be rank two by zeroing out the last singular value before
putting it back together by undoing the SVD with our newly rank-two S.)

We can plot epipolar lines once we have F.


#### Cameras, 3D Structures, Oh Yes
*Triangulation* uses known camera matrices and correspondences to compute
the 3D position of the corresponding points.

If you know the 3D position and correspondences but not the camera matrices,
you can work backwards to get them. Running triangulation backwards like this
is called _camera resectioning._

If you know the fundamental matrix, you can work backwards to get the camera
matrices. Ish. So, you actually just arbitrarily pick one to be unrotated and
at the origin, and then you can find the other matrix relative to that.
Ish, again - if you don't know a calibration, then any 3D reconstruction of
points is accurate only up to a projective transform, so angles and distances
aren't respected.

That isn't terribly interesting, but the calibrated case is:
we can get a metric reconstruction, which is accurate modulo a global scale
factor that we generally don't care about. We can apply the inverse of the
calibration matrix to all the image points to get calibration-normalized
coordinates. The fundamental matrix relative to this basis is called the
_essential matrix E_. Solving for camera matrices gives us four solutions,
but only one actually has the scene in front of _both_ cameras, so it's easy
to work out which one to pick. (In the messy IRL case, you pick whichever has
the most points in front of both.)


#### Multiple View Reconstruction: Structure from Motion
The apparent motion between the two views lets you recover the 3D structure.
Yay!

- Calibrate your camera
- Match feature points and normalize them
- Use those to estimate the essential matrix
    - RANSAC the 8-point algorithm
- Use that to estimate the other camera's matrix
- Triangulate inlier points
    - Ditch any not in front of both cameras.

There's some slop here. You can try to minimize it through "bundle adjustment",
which, uh, is a thing. That we don't talk about here.

Self-calibration: Also a thing. Depending on the info you have in the image
(parallel lines? planes?) and assumptions you can make about the cameras,
you can sometimes work out a calibration.

As you can imagine, some folks have a calibration worked out for a lot of
common cameras. And you can work backwards from EXIF data to get focal length.
So there's a script extract_focal.pl that the Bundler SfM system from
U Washington that puts that to work for you.


#### Stereo Images and Stereo Reconstruction (AKA Dense Depth Reconstruction)
This is a simpler case, with only horizontal displacement between images.
We have _rectified_ images where all the rows line up vertically.
This is what you get with binocular vision in robotics using a stereo rig.

Given a stereo camera setup, you can warp images to a common plane so that
epipolar line = image row. This is called _image rectification._ Handy.

As you can imagine, it's pretty straightforward to calculate a point's depth
once you have the corresponding points, the distance between the cameras'
centers (aka the _baseline_), and the displacement in pixel coordinates between
the two images. (It's just similar triangles! Again!) Z is to focal length as
baseline is to horizontal displacement.

If you know all the correspondences, you can plot out a depth map, or
equivalently, a _disparity map_. A bigger disparity means a nearer 3D point;
a lesser disparity means a further point. So you can shade 0 = black, max
= white and get basically a "lit scene" depth map.

The trick turns out to be finding those corresponding points automatically.
One quick and easy approach is to do _plane sweeping_, where we basically just
try every possible displacement for every possible point, and pick the one
that "looks" best, by maximizing the normalized cross-correlation on an image
patch around each pixel. Doing this using a uniform filter over the patch tends
to give you a bit noisier but also richer result than using a Gaussian filter.

This "so, uh, what do we _think_ the depth at this point is?" estimation
problem is stereo reconstruction, aka dense depth reconstruction. (Unlike our
usual "match the correspondences" with just a few features, here, we give
_every_ point a corresponding point, which I presume is why it's _dense_
depth.)

NOTE: The epipolar geometry bit felt kinda rushed and all over the place.
Partly because there's a lot of "if you have these things, you can get that
other thing" for several different things, so they're all very related; partly
because they didn't really walk through deriving the fundamental matrix that's
at the very heart of this all!


### Chapter 6: Clustering Images
*This was a relief after the triangulation and camera resectioning chapter.
Pretty straightforward, easy to visualize, and mostly fairly intuitive
algorithms, aside from the spectral clustering bit at the end.*

Clustering tries to group points together that belong together, in some sense.
This is a pretty generally useful tool for generalizing classification learned
from some training set. (This chapter is mostly setup for the next couple.)

Principal component analysis comes in handy for dimensionality reduction.
The chapter also uses multidimensional histograms to capture color content
for grouping sunset images, with 8 bins for each color channel, as generated
using [NumPy's `histogramdd`.](https://docs.scipy.org/doc/numpy/reference/generated/numpy.histogramdd.html)

We get a first taste of image segmentation (carving up an image into
meaningful components) by clustering pixels.

Hierarchical clustering (AKA agglomerative clustering) is introduced as well.
This builds a similarity tree by iteratively linking together a component with
a not-yet-grouped image that's nearest to it. This can be very neatly
visualized as a tree diagram.

Spectral clustering takes a similarity/distance matrix of pairwise similarity
scores (kinda like edge distances in a fully connected graph…), builds a
new matrix (the Laplacian matrix), grabs its eigenvectors, and projects your
data out onto that. This gives you dimensionality reduction (and vectors in the
first place, if you didn't have vectors as your data input used to generate the
similarity measure!) and lets you run k-means on that output.

You can also do hierarchical k-means clustering, which can be a handy way to
work with more features and classifier groups without getting bogged down in
projecting ALL the things to ALL the clusters. (See p. 166, the last exercise
in the Image Search chapter.)

A neat trick for picking *k* is shown at the end of the chapter, where
there are basically two groups but some junk images. Instead of doing k=2,
which would lump the junk in with one or both classes, it does k=10, which
leads to a bunch of singleton clusters, which it can then easily ignore
as junk.


#### K-Means Clustering
K-means finds k centroids (means). Every data point gets assigned to its
nearest centroid. The clustering algorithm is seeded with k initial centroids,
then iterated till quiescence by assigning points and then updating the
centroids to be the center of that new group of points.

Ultimately, this tries to minimize the total within-class variance.
Its ideal would be a bunch of data that is all stacked precisely on k points.

This algorithm tends to be sensitive to the initial points, so it's normal
to run it several times (say, 20) with different starting points, and then pick
the final batch of centroids with the lowest total error.

The clustering is in general sensitive to your choice of *k*. Having to pick
that up front is probably its biggest drawback. But it's easy, it parallelizes,
and it often works well without much tuning.

##### Code: SciPy Clustering Library
You can compute centroids using `scipy.cluster.vq.kmeans` and then label
new data relative to those centroids using `scipy.cluster.vq.vq`.
The "vq" bit stands for "vector quantization" - we're feeding it a vector,
and it's spitting out an integer (a quantization). How's that for data
compression?

##### Images
You could just feed in an array of all the image data as your feature vectors.
But you can also do dimensional compression by running PCA, grabbing the first
40 or 50 components, and then projecting out all your image data along those
vectors. This turns your thousands of points (a 1024x1024 image has a lot of
points! especially if you factor in RGB) into just 40 or 50.

You can ["whiten"](https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.vq.whiten.html#scipy.cluster.vq.whiten)
the data (normalize so each feature has unit variance),
then run k-means over that.

#### Principal Components Visualized
You can pick a couple principle component vectors, then plot your data
projected onto those vectors in 2D space. Fun!

The book uses PIL's ImageDraw system for this, rather than MatPlotLib,
presumably because it makes it easier to draw arbitrary lines and such?
Or just easier to save out to a huge PDF?

#### Hierarchical Clustering
Iteratively builds a tree based on "distances" between points.
Convert every point into a leaf node, then start linking the two nearest
together.

When we link nodes, we replace them with a synthetic node to represent that
whole tree for the next round of the algo. We also track the height and spread
(the distance between it and the thing we glommed onto it) at each node,
so we can easily break the tree up into clusters later.

Once we've got everything linked up, we can do a treewalk to spit out clusters
as "everything in a tree whose overall distance is below (some threshold value
you picked)". A good threshold can be, like, 30% of the total variation seen at
the root of the tree. If you don't need to split it up into clusters, just
looking at the similarity tree can be pretty handy, and you avoid the kinda
arbitrary thresholding bit.

Aside from the threshold bit, the algorithm can also be tweaked by using a
different metric to measure distance between points, as well as varying how
we decide which nodes to link together.

"Average-link (or group average) clustering is a compromise
between the sensitivity of complete-link clustering (which merges nodes to
minimize diameter, or the max distance between everything in the node) to
outliers and the tendency of single-link clustering (which merges nodes to
minimize distance, or the min distance between points in the potentially merged
node) to form long chains that do not correspond to the intuitive notion of
clusters as compact, spherical objects."
(http://nlp.stanford.edu/IR-book/completelink.html)


## Chapter 7: Searching Images
This applies text-mining techniques to image search ("content-based image
retrieval") via "visual words".

Visual words adapt the bag-of-words model used with text to visual features.
Project your images out into features (they use SIFT), create a "vocabulary"
(k-means centroids, say), project all the descriptors for each image onto that
vocabulary to create a "word histogram" (present / not present for each
vocabulary word, AKA "does this descriptor go in that cluster?"), and stash all
that info. That's your index database.

Now you can run the histogram process with a query image, yank all the images
that contain the same "words", and sort them by which have the most words in
common with your query image to dump out search results.

You can get more clever, of course! After you get that candidate set,
you can go and use RANSAC to compute a homography, and rank the images
with the most inliers down to least. Unlike SIFT features, this takes
where things show up in the image into account (geometry). Or factor in
color info alongside SIFT features.

Another approach to try to improve results is to discard the most common 10% or
so of visual words as stop words, and then weight the histogram using tf-idf
weighting (term frequency-inverse document frequency), which for a word in
a given document, weights a word higher if it shows up proportionally more
in that document (term frequency):

> tf(word, document) = document.count(of: word) / sum(document.count(of: word) for word in document.words)
>
and higher still if it's unique to that document (inverse document frequency)

> idf(word) = log(len(documents) / len(documents.containing(word)))

Search speed starts to matter as you increase vocabulary or index set size.
Maybe you only grab candidates for some of the words (the unique ones, per
idf), or you switch to a sparse array representation for the word histograms,
or you speed up clustering during indexing by using hierarchical k-means.

What's neat is how visual this all is - you can actually visualize a
visual word by grabbing a patch around every feature that projects out to it
and then dumping out all those image patches.


## Chapter 8: Classifying Image Content
So, with clusters, we already have a notion of how to classify stuff,
but this assumes we actually have training data with known labels
and test data with known labels, and then tries to work out a good way to
assign a label to test data so that we don't misclassify stuff.

### Visualizing
A convenient approach for trialing a clustering algorithm and visualizing how
it labels stuff is to generate random 2d-points in two clusters to begin with,
run the clustering algorithm across the data, and then plot the zero contour as
well as right/wrong label info for each point.

### Classifier: K-Nearest Neighbors
An easy clustering approach is k-nearest neighbors. You have to pick
k yourself, again, just as with k-means. Then, given a point to classify, you
pick the k nearest points from your training data, and label that point with
whichever class has a plurality (the most "votes") in that neighborhood.
"You're mostly standing by the red team, so you're probably part of the red
team, too."

### Featurifying Images: Dense SIFT, AKA Histogram of Oriented Gradients
Compute SIFT at each point on a mesh grid across an image. Concatenate all
those into one long vector. Now you have your feature vector.

Remember to resize your images to the same size, otherwise your feature vectors
won't be the same size, and everything will break on you.

You might also want to do PCA dimensionality reduction on those massive
feature vectors before clustering.

As before, the book shells out to a binary provided by VLFeat for SIFT,
using `sift foo.pgm --output=foo.sift --read-frames=foo.frame` and maybe
pitching in `--orientations` as well (otherwise everything just aims straight
up at each point, rather than orienting per local gradient). The frame file
is some sort of meshgrid of points written out using `%03.3f`.

You can visualize how things get messed up via a *confusion matrix*
which tells you how often something in class *i* got stuck in class *j*.
Ideally, you get numbers on the diagonals and zeroes elsewhere (we always said
an *i* was an *i*). This provides riches feedback about what your "spoilers"
are than just a "you got 87% correctly classified" summary.

### Classifier: Bayes
Lot smaller model than KNN - KNN requires you to hold onto all your training
data, while Bayes just reduces it all down to a mean and variance, and then
those get to say how likely a point is relative to that Gaussian distribution,
and the most likely one gets to label the point.


### Classifier: Support Vector Machines (using libsvm)
Normally these are just group A or group B. To do multi-class, you do K
one-against-all classifiers, "this is group N or not" for each class.


### Multi-Class Example: Sudoku OCR using libsvm
Also touches on *image rectification* using a homography warp and detecting
cells by finding lines in order to crop out the numbers for each cell so they
can be recognized.

This example is really cool. :)



## 2016-12-24 (Saturday)
I only did a half day on Thursday, so: let's finish this week out!

- Read chapter 9, Image Segmentation.
- Read chapter 10, OpenCV.

I got these read, but I didn't have time to do a write-up.
Hopefully I can snag a few hours a bit later and go through it.
The image segmentation chapter in particular was quite fun.



## 2017-01-02 (Monday)
- Wrote up notes on chapter 9, Image Segmentation.
- Wrote up notes on chapter 10, OpenCV.


### Chapter 9: Image Segmentation
Image segmentation is about carving up a single image into connected segments.
The aim is to group together similar pixels and separate dissimilar pixels,
with the idea that this represents objects or other meaningful distinctions in
the image, like foreground vs background.

#### Graph Cuts
We can treat the pixels as vertices in a digraph, and connect each to its
neighbor (either a 4-neighborhood, where we connect N-E-S-W, or 8-neighborhood,
where we add in NE-SE-SW-NW). We can weight the edges based on "similarity"
between pixels.

Then we can introduce fake source and sink nodes and use a max-flow/min-cut
algorithm like Edmonds–Karp to slice the graph into two components with minimal
connection (edge weight) between the two.

The source connects out to each pixel, and each pixel connects out to the sink.

How to weight the edges from source to pixel and from pixel to sink?
The book gives an example where two naïve Bayes classifiers are trained to
recognize foreground and background pixels based on one foreground and one
background region marked out by a human on the graph, then weights source
edges by how likely they are to be in the foreground and sink by how likely
in the background. The cut then ends up cutting foreground from background.

We can label the pixels with which cut component they end up in, and then
visualize that separation using a `contourf` plot.

An interesting tidbit here is that, because they're using a pure Python
graph algorithm kit, they have to resize the image to be a lot smaller so
the library can cope with running the min-cut algorithm in a reasonable amount
of time.

The exercises point out that you might see better results using something
other than concatenated RGB data for the pixels in the training regions
as your Bayes feature vectors - say, intensity, or maybe just the red channel,
or whatever. You could also detect foreground and background, retrain on
those, and then run the algorithm again with the new classifiers - iterated
graph cut segmentation. This "sharpens" the judgments made along the way,
walking a step further along the path of what the first classifier called
foreground vs background.

##### User Input
Notice how we trained the Bayes classifiers based on user input.
That kinda surprised me - I figured this would be a hands-off algorithm -
but it seems pretty common.

For example, the
[Grab Cut dataset provided by Microsoft Research](http://research.microsoft.com/en-us/um/cambridge/projects/visionimagevideoediting/segmentation/grabcut.htm)
actually has training labels for background and foreground as both rectangular
and lasso regions.

The background for this assumption seems to be interactive image editing -
think the Magic Wand tool (color-similarity selection) and Intelligent Scissors
tool (contrast-based edge detection). Having an algorithm to pick out an
object the user tells you is right about there-ish is useful!

#### Finding Normalized Cuts and Clustering
Simple graph cuts tend to pick out tiny regions, since they have fewer edges
to cut, period.

Normalizing the cut size by the association between each component and the
rest of the graph pushes it to prefer bigger regions, so you're not axing
every link that region has to the rest of the graph.

This gives a discrete minimization problem that turns out to be NP-complete,
but you can turn it into a real-valued minimization problem that can be
efficiently solved - it becomes an eigenvalue problem analogous to spectral
clustering.

The weighting used connects every pixel to every other using a weight that's
a product of factors based on pixel similarity and on pixel proximity.

(Remember: Whenever you can assign a value to each-to-each similarity,
you can employ spectral clustering!)

To go back from the real-value domain to the image, the book uses
*k*-means clustering on feature vectors made up of a stack of the first three
eigenvectors of the real-valued solution approximated by SVD.

An alternative approach would be to grab the second eigenvector and then
threshold to get two components, and then recurse on each component to break
it up further, if desired, till the min normalized cut exceeds a max value
(there aren't any more "good" cuts to make).

(For details, check out
[Shi & Malik's "Normalized Cuts and Image Segmentation"](https://people.eecs.berkeley.edu/~malik/papers/SM-ncut.pdf)
from Aug 2000.)

Some more real-world notes:

- The book again resizes the image down (to 50x50), this time to make SVD
  practicable.
- It resizes it down using bilinear interpolation, labels everything,
  and then resizes the label image back up for comparison using
  nearest-neighbor to avoid not-a-component-label values appearing in the
  larger image due to interpolation.

Note that this _is_ a hands-off approach, and it does better than simple
thresholding or clustering because it takes pixel "neighborhoods" into account.
(Though there are a couple tunables related to how much to weight proximity vs
similarity for the edge weight calculation.)

When I think of how pixel clustering has failed me in the past, I think of
using Magic Wand on an image, and how it might just pick out the highlight or
shadow on an object rather than the whole object, because it's dumb.

Exercises suggest you could use image gradients over the eigenvectors to
detect image contours of objects.

#### Variational Methods
*I really appreciated how the method used in this section is elegant, simple,
and visualizes well.*

An optimization problem over functions rather than values is called a
*variational problem.* An algorithm to solve such a problem is a
*variational method.*

The Chan-Vese segmentation model assumes you can carve the image up into
piecewise constant regions using curves. The "energy" of the segmentation to
minimize is a sum of the curve length (to penalize wiggly boundaries) and the
error relative to the constant value of the region.

You can turn this into a nice discrete problem for graylevels that happens
to look almost 100% like the ROF equation used for denoising! To restore the
piecewise constant bit, we throw in thresholding.

And now we have a quick and easy two-step process for image segmentation:

- Apply ROF de-noising
- Run the image through a threshold relative to the max image value

In practice, they tune down the ROF tolerance threshold really low so that
it runs long enough to split everything apart. This gives some really nice
results really fast.

The book only covers splitting into two components using this model, though;
not sure how you'd extend to more, except maybe by playing with thresholds
within components?

This is also a hands-off approach, though tuning the threshold and iterations
is probably kinda manual. To solve that, the exercises suggest running
a linear search over the threshold value and then picking the segmentation
with the lowest energy value. That should go fast, since the maybe lengthy
denoising gets run once, and then we just play around with tuning a threshold,
and the thresholded image is pretty fast to calculate.


### Chapter 10: OpenCV
OpenCV is a BSD-3–licensed C++ library with a grab bag of functionality for
working with still images and movies, extending even to cross-platform
windowing and display. It's seen work by Intel, NVDIA, and AMD.

It bakes in support for doing some things we've gone over doing manually,
particularly object detection, segmentation, and stereo camera magic that
goes beyond what we talked about so far. Oh, and more - that was based on
the OpenCV 2.4 cheatsheet, but it's now in the 3.2 range and does even more!

Most of this chapter is a tour of some of the bundled examples using the
Python bindings to the C++ library.

#### Basics
- OpenCV likes BGR channel order by default. Use cvtColor to change
  colorspaces, like to grayscale.
- OpenCV can write out images (it figures out the format based on the
  file extension)
- OpenCV can show a window (imshow) and wait to dismiss it (waitKey).
  It can also accept mouse input and show a trackbar.
- OpenCV provides a portable video processing API, including video capture
  from input devices (!).
    - You can read a frame out and append it to a NumPy array to get a series
      of images to work with.

#### Tracking
*Tracking* is following objects through a sequence of images (AKA video).

*Optical flow* (aka "optic flow", because English) is the image motion of
objects across two consecutive images. You basically layer a translation vector
atop each pixel in image 1 that shows where it went in image 2.

This works by assuming:

- Brightness constancy
- Temporal regularity: The consecutive images are "close enough" in time that
  differentials work
- Spatial consistency: Neighboring pixels have similar motion

This mostly holds for small motions and short time steps. You can then
say that a pixel at (x, y, t) is the same as one at (x + dx, y + dy, t + dt)
and differentiate to get the optical flow equation, which gives you a motion
vector at each point.

There are several different algorithms that OpenCV has for this:

- Old and not even available in the modern Python API under `cv2`:
  - Block Matching
  - Horn-Schunk, from 1981
- Pyramidal Lucas-Kanade, also from 1981
  - Good at following interest points like corners.
  - Next section gives a more in-depth example.
- Farneback, from 2003
  - Good at getting dense flow fields. AKA "imagine every pixel is an interest
    point".
  - Easy to deploy, easy to visualize.

#### Lucas-Kanade Tracking
There's actually a function called `goodFeaturesToTrack` that implements an
algorithm from the paper of the same name by Shi & Tomasi published in 1994.
(Corners are points with two large eigenvalues in the Harris structure tensor,
where both are above a threshold.)

If you stack all the optic flow equations together and work with the
good-features-to-track points, you get a system of
equations that actually has enough constraints on it and nice properties by
construction to be solveable.

The pyramidal bit is used as a hack to handle larger displacements - you run
the algorithm at coarse-to-fine versions of the image.

**NOTE: If you see "Pyr" in an OpenCV function, it's short for Pyramid or
Pyramidal.**

The example finds the features, refines them for subpixel positioning, then
tracks them using LK from frame to frame and visualizes them using matplotlib
by drawing where they moved over the frame. It handles removing dead (occluded)
features using the `status` return from the track call, which says if the
feature was found or not in the nextImg.

#### Grab Bag
- Inpainting: Reconstruction of lost or deteriorated parts of images.
  Think red-eye correction and object removal, as well as fixing corrupt
  bits. The example has you you mark corrupt image bits by drawing on the
  image, and then it tries to rebuild them.
- Watershed segmentation: "Flow" fill regions from seed pixels. Done on
  gradient image, so that edges become ridges. Example has you draw seed
  lines on the image, and then it floods it.
- Line detection: Uses the Hough transform. Finds lines, but they're infinite.
  You can use edge detection to try to truncate them. Or now there's a
  probabilistic Hough transform function that dumps line endpoints rather than
  (rho, theta) infinite lines the way the plain Hough transform does.
    - The
      [OpenCV docs](http://docs.opencv.org/2.4.13.2/modules/imgproc/doc/feature_detection.html#houghlines)
      point you to this
      [description of the Hough transform](http://homepages.inf.ed.ac.uk/rbf/HIPR2/hough.htm)
      at the [Hypermedia Image Processing Reference](http://homepages.inf.ed.ac.uk/rbf/HIPR2/hipr_top.htm),
      which retains the feel of the Web of the 1990s:

      > If you are viewing the hypermedia version of HIPR, then what you are
      > seeing now is the Welcome Page of HIPR. You are viewing it with the aid
      > of a piece of software called a hypermedia browser, probably one called
      > **Netscape** although others can be used just as easily.

*And that's it - the end! OpenCV looks like a very good toolkit to have on
hand, especially when Python isn't available. If you have Python in hand,
though, you probably want to give [SimpleCV](http://simplecv.org/) a look! It's
like the higher-level "just pick the right algorithm for me already" version of
OpenCV.
Though [SimpleCV appears to have petered out in April 2015 based on GitHub](https://github.com/sightmachine/SimpleCV).
[tpltnt's SimpleCV fork looks lively, though.](https://github.com/tpltnt/SimpleCV)*
