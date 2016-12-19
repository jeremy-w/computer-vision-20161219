# Computer Vision
- Unclass: Week of 2016-12-19
- Jeremy W. Sherman

This repo is a dumping ground for notes taken during a week of studying computer vision. The initial charter for the week is the (private) [Unclass Proposal](https://docs.google.com/document/d/13MCtXiMF2NgKTjGpvNBzbgVnCuvsAP6-9niB_LAs9U0/).
This file is primarily a daily log.


## Jargon
Jargon encountered.



## Resources
Useful resources I didn't know about before.



## 2016-12-19 (Monday)
- Created repo for the week: [jeremy-w/computer-vision-20161219](https://github.com/jeremy-w/computer-vision-20161219)
- Reviewed the texts I have on hand for the week.
    - Pivoted from *OpenCV for Secret Agents* as main driver to *Programming Computer Vision with Python* (mostly referred to as "PCV")
      - This change surprised me!
- Started mapping out some of the vocabulary and concepts of computer vision
- Set up a Jupyter notebook for experimenting with Python computer vision stuff
  in


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
