# Documentation Of NTOP-Project
NTop pipeline workflow have used three type of datasets which includes-
+ ["Human3.6m"](http://vision.imar.ro/human3.6m/description.php)
+ [“GeneBody”](https://generalizable-neural-performer.github.io/genebody.html) 
+ [“Zju-Mocap”](https://chingswy.github.io/Dataset-Demo/)
  ![IMG-20240226-WA0118](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/99593957-2f9c-483e-95fc-54824e4841c5)

### Human3.6m:
##### Properties:
+ 3.6 million 3D human poses and corresponding images
+ 11 professional actors (6 male, 5 female)
+ 17 scenarios (discussion, smoking, taking photo, talking on the phone...)
+ High-resolution 50Hz video from 4 calibrated cameras
+ Accurate 3D joint positions and joint angles from high-speed motion capture system
+ Pixel-level 24 body part labels for each configuration
+ Time-of-flight range data
+ 3D laser scans of the actors
+ Accurate background subtraction, person bounding boxes
## Subjects & Scenarios:
##### Subjects:  
![human3 6](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/16db7a07-3751-4f47-a495-3b6af2c3c43b) ![human3 6 dataset](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/1c3b9de8-8bfd-4836-9a40-a2502f46bc33) ![human3,6 2](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/c5948fbd-09d2-483b-8eef-215a41806032) ![Human 3 6 dataset3](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/e1eb294c-e143-4ecb-9d27-9d20df5ba8e8) ![human 3 6 dataset5](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/e42583f3-77a3-4566-a922-e06364e165d1) ![4](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/88e8222f-725e-4c63-a0cf-ecd4fc5b83a1)

The motions were performed by 6 professional actors, 4 male and 2 female, chosen to span a body mass index (BMI) from 17 to 29. This provides a moderate amount of body shape variability as well as different ranges of mobility. The subjects wore their own regular clothing, as opposed to special motion capture costumes, to maintain as much realism as possible. 
##### Scenarios:
![activities while seated](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/cbc0a7e9-8835-4b2d-8d31-810c0b3d0958) ![smoking](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/03a97184-4c04-4dd1-a160-58621a6764bb) ![talking on the phone](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/f6b70cec-abc0-422e-ab0a-1e89493f5761) ![taking photo](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/9515734c-092f-4496-92c9-357240ed8f91) ![greeting](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/9d34f23b-dd62-4513-ad69-52333f068902) ![purchases](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/4bf26acb-fd7f-4688-a371-3a592175695f) ![posing](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/3f54152d-189b-4277-a880-f2ff3d7032d4)

The dataset consists of 3.6 million different human poses collected with 4 digital cameras. Our data is organized into 4 training motions containing walking with many types of asymmetrie(e.g: Smoking, Taking photo), sitting and laying down poses, various types of waiting poses and other types of poses. The actors were given detailed tasks with examples in order to help them plan a stable set of poses between repetitions for the creation of training, validation and test sets. In the execution of these tasks the actors were however given quite a bit of freedom in moving naturally over a strict, rigid interpretation of the tasks.
## Data: 
![camera_arrangement2](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/402a026e-561c-4920-b77d-8655289d53b3)
Our laboratory setup is schematically representated in the figure. It allows us to capture data from 15 sensors (4 digital video cameras, 1 time-of-flight sensor, 10 motion cameras), using hardware and software synchronization. The capture area was about 6m x 5m, and within it we had roughly 4m x 3m of effective capture space, where subjects were fully visible in all video cameras. Digital video (DV) cameras (4 units) are placed in the corners of the capture space. A time-of-flight sensor (TOF) is also placed next to one of the digital cameras. A set of 10 motion capture (MX) cameras are rigged on the walls to maximize the effective experimentation volume, 4 on each left and right edge and 2 roughly mid-way on the bottom horizontal edge. Detailed specifications of the system are given in table 1. A 3D laser body scanner from Human Solutions (Vitus Smart LC3) was used to obtain accurate 3d volumetric models for each of the subject actors participating in experiments.
### Image Data:
![human3 6](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/81d8302f-63f8-4309-9cf0-3f3796b81141)
 We use 4 basler high-resolution progressive scan cameras to acquire video data at 50 Hz. They are on same clock and trigger as the motion capture system which ensures perfect synchronization between the video and pose data. The system's default calibration procedure is very simple to perform but the camera model does not contain radial and tangential distortion parameters. Since we strive for exceptionally high quality pose information we have performed a more complex and more robust procedure that fits all these parameters as well. The total number of video frames for the entire dataset is over 3.6 Million.
### Pose data:
  Pose data is given with respect to a skeleton. For consistency and convenience we use the same skeleton of 32 joints for all of our parametrizations. In testing we reduce the number of joints the relevant ones e.g. leaving only one joint for each hand and each foot.

Common pose parametrizations considered in the literature include relative 3D joint positions (R3DJP) and kinematic representation (KR). Our dataset provides data in both parametrizations with a full skeletons containing the same joints in both cases. It also provides 2D joint positions since some methods may require this data.

+ In the first case (R3DJP), the joint positions in 3D space are provided. They are obtained from the joint angles provided by the Vicon skeleton fitting procedure by applying forward kinematics on the subject skeleton. R3DJP is challenging because it is very hard to estimate the size of the person. This problem is obviated in practice by providing the same skeleton (limb lenght) information for all subjects,including those in testing, if needed. The parametrization is called relative because there is a joint, usually called root joint (roughly corresponding to the human pelvis bone position), which is taken as the center of the prediction coordinate system and the other joints are estimated relatively to it.
+ The kinematic representation (KR), considers the relative joint angles between limbs and is more convenient because it is invariant to both scale and body proportions. The dependencies between variables are however much more complex making estimation more difficult. The process of obtaining joint angle values involves a complex constrained non-linear optimization process. We devoted significant effort to ensure that data is clean and the fitting process is accurate.
+ We use the camera parameters to project the 3D joint positions and obtain very accurate 2D pose information.
Outputs were visually inspected multiple times, during different processing phases, to ensure accuracy. These representations can be directly used in independent monocular predictions or in multi camera settings. The monocular prediction dataset can be increased 4-fold by globally rotating and translating the pose coordinates as to move the 4 DV cameras in a unique coordinate system (code is provided for this data manipulation). Poses are available at four-fold faster rates than images from DV cameras. The code provided can also be used to double both image and pose data by considering their mirror symmetric versions.
### Time-Of-Flight-Data:
![TOF_range](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/0c6bf46a-68d4-46a7-b06b-e8bd02e80ebf)Time of flight information is obtained using MESA Imaging SR4000 from SwissRanger at a 25Hz rate. This is a relatively standard Time-of-flight sensor on the market. One sensor was placed near one of the video cameras and captured the entire set of motions. Synchronization with the system is done by a software trigger. The camera itself has an internal clock at which data acquisition is performed. Time-stamps were taken for each acquisition to maintain synchronization. Analyzing the time-stamp information we found the acquisition to work at the desired framerate in a great majority of cases and code is provided to correct desynchronizations.
### Scanner Data:
All of the actors were scanned using a 3 sensor 3D scanner from Human Solutions called Vitus Smart LC3. The meshes obtained are preprocessed by Human Solution ScanWorks software and some manual intervention to repair the mesh was done by our staff. The mesh is available in Wavefront OBJ format and Matlab code is provided for loading the mesh.
![1](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/e144a88f-5c48-4d15-abf1-de5984b01f8b) ![2](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/d5a79199-9e21-4927-9340-79092f774f6b) ![3](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/de4a8020-a89f-40a4-9e03-3dbf971bd954) ![4](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/5e79a6a7-3548-44bc-9485-87d020b48c04) ![5](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/550cc5aa-5fb6-458a-9c3a-243b88110d46) ![6](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/461bd930-a617-47c9-a21b-f65816d16b04) ![7](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/99bcc0bd-5b35-41c6-9917-8a8e4c792f94) ![9](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/e4408bd3-6dc9-4fd1-8740-38e957f1ba50) ![10](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/78231d5a-f7df-4429-bdb3-011b2eab28a0) ![11](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/ed507f20-e349-46bc-99a8-7ade48794cee)
#### Support for Development:
+ Precomputed image descriptors
+ Software for visualization and discriminative human pose prediction
+ Performance evaluation on withheld test set
### GeneBody:
##### Properties:
+ Deformable Neural Radiance Fields creates free-viewpoint portraits (nerfies) from casually captured videos
+ Genes are a set of instructions passed down from parents to offspring. They contain the information that determines a person’s specific physical and biological traits, like hair color, eye color, and blood type.
+ Most genes code for specific proteins which have different functions throughout the body and allow humans to live, grow, and reproduce.
+ Genes are made of sections of DNA. DNA is made of chemical building blocks called nucleotides. A gene consists of four different nucleotide bases, which can be sequenced in different ways.
+ Different sequences of bases determine different instructions, which account for various physical traits, like having blue eyes or brown eyes.
+ Changes in genes can lead to incorrectly formed proteins that can’t function correctly. These are called gene mutations and may lead to genetic disorders.
+ Researchers are studying genetic testing to be able to identify changes in a person’s DNA that may show if they are at risk for developing a disease or passing down a disease to their offspring.
### Zju-Mocap:
##### Properties:
LightStage is a multi-view dataset, which is proposed in NeuralBody. This dataset captures multiple dynamic human videos using a multi-camera system that has 20+ synchronized cameras. The humans perform complex motions, including twirling, Taichi, arm swings, warmup, punching, and kicking. We provide the SMPL-X parameters recovered with EasyMocap, which contain the motions of body, hand and face. Please download the dataset from [here](https://github.com/zju3dv/neuralbody/blob/master/INSTALL.md#zju-mocap-dataset).

-------------------
+ **Parameters of Human3.6m**:
+ Camera parameters 
+ 2D GroundTruth Joints
+ Images
   
+ **Parameters of GeneBody**:
+  Camera parameters
+ 2D predicted Joints **(Yolo+HRNet)**
+ Images

+ **Parameters of Zju Mocap**:
+ camera parameters,
+ 2D GroundTruth Joints,
+ Images.
### These parameters of three datasets has been used over here.

------------------------------------------
## STEPS:
>By using **EasyMocap software** , created 3D Mesh **(SMPL+H)** model.
### SMPL:
[SMPL](https://smpl.is.tue.mpg.de/) SMPL is a realistic 3D model of the human body that is based on skinning and blend shapes and is learned from thousands of 3D body scans. This site provides resources to learn about SMPL, including example FBX files with animated SMPL models, and code for using SMPL in Python, Maya and Unity.
>Now using **Camera parameters, Alpha mask** ( Background of a human body is black and the structure of that person is white to identify that person) and images to make HumanNeRF model.
### Alpha Mask:
[Alpha Mask](https://br24.com/en/all-about-alpha-maskings/) There are several ways to create alpha maskings. The prerequisite is an image editing program that enables the editing of the individual colour channels of an image, an experienced eye and skill.
#### An overview of the basic work steps:
+ **Selection of the most contrasting colour channel**: by comparing the colour channels red, green and blue (RGB image).

+ **Copy channel**: so as not to change the original image when editing.

+ **Enhance contras**t: e.g. via brightness and contrast, curves or levels to capture all important details of the object.

+ **Paint over inner and outer areas**: Paint outside black and inside white (or other high-contrast colour combination). As close as possible to the edge of the object, without translucent areas.

+ **Manual work for details**: Manual tracing to capture fine details on the edge of the object, e.g. individual hair.

+ **Black and white image**: As a result, the white object stands on a black background.

+ **Load selection**: Load the layer with the edited channel as a selection, which outlines the object perfectly.

+ **Create layer mask**: Add the active selection to the background layer as a layer mask, invert the mask and delete the content. The masked object stands on a transparent background.

+ **Corrections**: Further corrections and adjustments if necessary.

+ **Convert to alpha channel**: Save the edited selection and convert it into an alpha channel. The object (white) is perfectly separated from the background (black). By activating the colour channels the original object becomes visible.
 > Adjust the **camera parameter** to capture Top View of **HumanNeRF model**. By this I have received two types of images –

     + “Top View images”
    
     + “Top View Skeleton Data”
>Now, Under **Top View Images**, captured-
     + **Fisheye View RGB image**
     + **Generic Top-View**
     + **Fisheye Alpha image**
### Fisheye View RGB image:

 ![Barn_grand_tetons_rgb_separation](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/39e57e87-5cae-4c21-b261-69c7ee56b26c) ![Fisheye](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/aa826f57-f8dc-4e75-82b1-126148accb8c)


**An RGB image, sometimes referred to as a truecolor image, is stored as an m-by-n-by-3 data array that defines red, green, and blue color components for each individual pixel. 
 RGB images do not use a palette.**
 
### Generic Top-View:

![Generic top view](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/fdad07d1-b392-4e6a-847b-a7f1be7a4fda)

> There are two types in **Top View Skeleton Data**-
![IMG-20240226-WA0118](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/c6603792-13e1-4a6a-8f89-36a8b1f57145)


+ **SMPL(24 Joints)** :
 SMPL is a realistic 3D model of the human body that is based on skinning and blend shapes and is learned from thousands of 3D body scans. This site provides resources to learn about SMPL, including example FBX files with animated SMPL models, and code for using SMPL in Python, Maya and Unity.

Please register to download SMPL and related tools for using SMPL in different animation environments. After registration you will be able to access the Downloads menu at the top menubar.
        
+ **COCO(17 Joints)** :  
  COCO is a large-scale object detection, segmentation, and captioning dataset. COCO has several features:
       
+ Object segmentation
        
+ Recognition in context
        
+ Superpixel stuff segmentation
        
+ images (>200K labeled)
       
+ 1.5 million object instances
        
+ 80 object categories
        
+ 91 stuff categories 
        
+ 5 captions per image

+ 250,000 people with keypoints

**These two datasets(SMPL, COCO) are included**
> For both Datasets(SMPL & COCO) we have used 2D & 3D Keypoints which is shown below.

   .**Fitting SMPL(24 Joints) parameters by 2D-pose key-points**:
![SMPL 2D](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/3bbc8223-59cd-48c4-8482-4db5b4ce6421)
      
.**Fitting SMPL(24 Joints) Parameters by 3D-pose Key-points**:

The repository provides a tool to fit SMPL parameters from 3D-pose datasets that contain key-points of human body.

The SMPL human body layer for Pytorch is from the [smplpytorch](https://github.com/gulvarol/smplpytorch) repository.
![fit](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/0e883bfa-5886-4934-96ed-ec7b98862968)

<p align="center">
<img src="assets/fit.gif" width="350"/>
</p>

![gt](https://github.com/Dipankar1997161/NTOP-Project/assets/104356405/623b660d-3471-49e9-97d2-c9354a8e0646)
<p align="center">
<img src="assets/gt.gif" width="350"/>
</p>
> Here, we are getting 3D, 2D keypoints, Fisheye view, Generic view by using NToP570K Dataset. Which is shown below..
 Here, I am attaching the dataset.


Please register to download SMPL and related tools for using SMPL in different animation environments. After registration you will be able to access the Downloads menu at the top menubar.
