# ACTANNO (v3) : Object annotation tool #

LIRIS Authors: Christian Wolf, Eric Lombardi, Julien Mille
Actanno V1 

ONERA Contributor : Joris Guerry (joris.guerry@onera.fr)

RICA Contributor: Viktor Schmuck (svmotric@gmail.com, viktor.schmuck@kcl.ac.uk)

*****************************************************************************

PLEASE ACKNOWLEDGE THE AUTHORS AND PUBLICATION ACCORDING TO THE
REPOSITORY https://github.com/d4rkspir1t/actanno-v3 OR IF NOT AVAILABLE:

RCNN RGBD pour la détection de personnes en conditions difficiles

J.Guerry and B. Le Saux and D. Filliat, Groupe d'Etudes du Traitement du Signal et des Images (GRETSI) 2017

and

Evaluation of video activity localizations integrating quality and quantity measurements

C Wolf, J. Mille, E. Lombardi, O. Celiktutan, M. Jiu, E. Dogan, G. Eren, M. Baccouche, E. Dellandrea, C.-E. Bichot, C. Garcia, B. Sankur, In Computer Vision and Image Understanding (127):14-30, 2014. 

and

RICA: Robocentric Indoor Crowd Analysis Dataset

Schmuck V., Celiktutan O., In Proceedings of UKRAS2020, 2020

*****************************************************************************

![](https://github.com/d4rkspir1t/actanno-v3/blob/master/sample_frames/bbox003646_censored.jpg)

*****************************************************************************
*****************************************************************************

## SETUP ## 
### Backend setup ###
1. Install OpenCV
1. Install TKinter
1. Set up an environment:
> 1. Set up a Python 3.7 base environment with `conda create --name aao python=3.7`
> 1. `pip install pyscreenshot pillow matplotlib easydict PyYAML numpy==1.19.3` 

### Configuration ###
The configuration files can be found in the respective supporting files folders (label- or indexassign).
The run commands are (when inside the `src` folder or an IDE):

`python actanno-v3-labelassign.py ../supporting_files/labelassign/ ../group_images/`

`python actanno-v3-indexassign.py ../supporting_files/indexassign/ ../group_to_human_images/` 

... where the first input points to the folder of the configuration file(s). And the second parameter should 
point to the input images. This folder will also be the location of the resulting XML file.

In addition, it is now possible to load previously created bounding box images and bounding box information purely
for relabelling purposes - This is useful when multiple annotators are required for increased validity, but the
bounding box placement should not be changed. The run command (inside `src`) is:

`python actanno-v3-labelling_only.py ./supporting_files/labelonlyassign/ /path/to/boundingbox/images/and/xml/`

### MySql setup ###
1. Install MySql and the python mysql connector.
1. Set up the MySql environment e.g. by:
>1. `CREATE USER 'admin'@'localhost' IDENTIFIED BY 'password';`
>1. `GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' IDENTIFIED BY 'password';`

*****************************************************************************
## CHANGELOG ##

14.12.20 vs:
- adjustments to work on Ubuntu 18.04
- excluded JMTracking due to incompatibility
- indexassign -> fixed errors with merged boxes between frames, duplicate output save in same frame into the xml file, 
  moving bbox no longer produces duplicates
- deletion of not highest index bbox does not ruin reliability of box saving and label tracking
- labelonlyassign -> label assignment based on dicts, fixed and simlified xml saving, adjusted layout, 
  reduced functionality e.g. no bounding box manipulation

29.04.20 vs
- 2 versions of actanno v3 created
- added label and index assignment versions (src/actanno-v3-labelassign.py, src/actanno-v3-indexassign.py)
- added user feedback pop-ups
- added annotated image saving with consistent naming
- index assignment requires mysql to run -> speed improvement
- code cleaned and corrected, made in a better OOP style
- code updated to run with a python 3.7 backend and the updated version of tkinter
- indexassign -- add keyboard shortcut : tab -> label assignment window pop-up

*****************************************************************************

12.04.17 jg:
- add PASCAL VOC format exportation
- add configuration file feature
 

09.09.16 jg:
- add gray image PNG compatibility
- add keyboard shortcut : q-> quit
- add keyboard shortcut : s-> save
- add keyboard shortcut : p-> force propagate only the bounding box hovered (with the focus). Allows to make a new bounding box from the beginning and propagate it without impacting the others.
- add scroll bar at bottom to visualise the movie
- change the export format : add the file name in XML (for external use)
- add RGBD features :
      * files must be at format numFrame_timestamp.ext
      * ./actanno.py <xml file> <rgb prefix> [optional: <depth prefix>]
      * add switch button to show the depth image closest to the current rgb image
		-
- rectangle can go at the edge of the window without disappear
- change tostring-> tobytes in src/minimal_ctypes_opencv.py (due update of opencv)

*****************************************************************************

10.09.14 el:
- Fix performance issue (slow-down when first rectangles are drawn).

03.09.14 el:
- Replace 'moving arrows' image by a circle around anchor points, to provide better visibility in small boxes ; change anchor points activation distance to allow smaller boxes.

03.09.14 el:
- Changing the classes is made easier: it only requires to modify the 'classnames' variable ; the class menu is now dynamically built from the content of the 'classnames' variable, and does'nt need anymore to be changed by hand.

14.12.11 cw:
- Bugfix in actreader version : remove imgTrash and imgMove and references to it

01.12.11 cw:
- Added comments allowing to extract a read only version of the tool

06.10.11 cw:
- Change the description of some objects
- Check if save went ok
- Jump only 25 frames
- The program does not stop when no objects are in an existing XML file
- A loaded file is not automatically considered as modified

05.10.11 cw:
-Check whether the XML frame numbers are larger than the number of frames in the input
- Remove most of the debugging output

03.10.11 cw:
- Added "D" (DELETE ALL) command
- Runid's can be entered with the keyboard
- Typing in a videoname will do keyboard short cuts (d,f etc.)
- Check for validity when saving a file
- Jump far with page keys
- Check for unsaved changes before quitting
- Add video length in the title

01.19.11 cw:
- Added "d" (DELETE) command
- Simulate right click with CTRL + left Click
- Bugfixes:
- All 4 corners can be used to resize a rectangle now

29.09.11 el: 
- Integration du module tracking de Julien Mille

07.09.11 cw: Bugfixes:
- no crash if XML does not exist
- correct update of class list;
- fixed: incomplete XML export
- fixed: Propagating with space after listbox usage will pop up the listbox again
- Short click on the image will create a rectangle with weird coordinates

30.08.11 cw:
- Add XML parser

02.07.11 cw:
- begin development

*****************************************************************************
