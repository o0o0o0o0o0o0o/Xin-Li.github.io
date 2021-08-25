---
title: Xin Li
layout: default
---

# About Me
&nbsp; &nbsp; Welcome to my site! My name is Xin Li, I'm currently a computer science graduate student at UCSD. I received my Bachelor's Degree in Computer Science from Sichuan University, China in June 2020. At Sichuan University, I took part in several research activities of image processing and medical image denoising. It was during this time that I discovered my interests in image algorithms and graphics.  
&nbsp; &nbsp; I'm super excited about all the visual effects and illusions, the idea of being able to create an interacting vitual new world from bottom up fascinates me, the elegance and sophistication in the design of all the image algorithms makes me obsessed, the applications and enhancements of these algorithms astonishes me.

# Projects
This section shows results of some of my projects, implementation for most of them can be found in my github repository.

## *Physics Simulation*
In this project, I simulate the kinematics of some classic physics models including fluids, rigid body, finite elements, and rendering using OpenGL.  


* ### Finite Elements

For this part, 5 tetrahedrons(each has 4 corner particles) are used to build a cube, and the cubes are then used to build cuboids.  
<figure>
	<center>
		<img src="./images/TetrahedronCube.png" alt="how are the tetrahedrons organized" width="50%" height="50%"/>
  		<figcaption>organize tetrahedrons to build cuboids</figcaption>
  	</center>
</figure>

And then the movements of all the particles are integrated by calculating the forces applied on them using strain and stress tensor. See the following GIF of how a cuboid object will bounce when it hits the ground.  

<figure>
	<center>
  		<img src="./images/finite-element.gif" alt="Tetrahedron cube bounces" width="50%" height="50%"/>
  		<figcaption>Tetrahedron Cube bounces</figcaption>
  	</center>
</figure>

It will bounce because it deforms, and the inner pressure of the solid object trys to resist the deformation and so pushes it up. Eventually it will come to rest because of loss of energy.


* ### Fluid

The fluid system in this simulation is particle based(smooth particle hydrodynamics), Navier-Stokes Equation is used to derive the acceleration of the particles, taking into account of convection, viscosity, and pressure of the fluid, and then the movements of the particles are integrated.

<figure>
	<center>
  		<img src="./images/fluid.gif" alt="Tetrahedron cube bounces" width="50%" height="50%"/>
  		<figcaption>SPH simulation</figcaption>
  	</center>
</figure>
<!-- ![](./images/fluid.gif){:height="50%" width="50%"}   -->

A continuous version of fluid simulation can be rendered using methods like Marching Cubes.

  

* ### Rigid Bodies

<!-- ![](./images/rb1.gif){:height="50%" width="50%"}![](./images/rb2.gif){:height="50%" width="50%"}  
![](./images/rb3.gif){:height="50%" width="50%"}![](./images/rb4.gif){:height="50%" width="50%"}  -->

<!-- <style>
	div{float: left;}
</style> -->

The position of the points of a rigid body are fixed related to a reference point. In the simulation of rigid bodies, just keep track of the linear and angular momentum of the reference point, and calculate the volecity for all the points in each frame using these momentums and the Rotational Inertia.

<div style="float:left">
	<figure>
		<center>
		  	<img src="./images/rb1.gif" alt="rigid body 1" width="45%" height="45%"/>
		  	<img src="./images/rb2.gif" alt="rigid body 2" width="45%" height="45%"/>
		  	<img src="./images/rb3.gif" alt="rigid body 3" width="45%" height="45%"/>
		  	<img src="./images/rb4.gif" alt="rigid body 4" width="45%" height="45%"/>
		  	<figcaption>kinematics of flat, slim, rotating and cubic rigid bodies</figcaption>
	  	</center>
	</figure>
</div>



The rigid bodies will not deform, so technically they won't bounce. Here I'm using a method called Collision Impulse with Friction from “Nonconvex Rigid Bodies with Stacking”, Guendelman, Bridson, Fedkiw.


## *Image processing from scratch*

This project contains dozens of classic image processing algorithms that are written from scratch.

* ### Feature point extraction and image stitching


Some famous feature point algorithms are implemented from scratch, including SIFT, SURF and ORB, they all have their own pros and cons. SIFT and SURF extract feature points in an image pyramid to achieve certain degree of scale invariant, whereas ORB simply does that on the original image. By carefully designing their descriptors, all the feature points from these algorithms are rotation invariant to some extent.

<figure>
		<center>
		  	<img src="./images/castle_match.jpg" alt="match" width="100%" height="100%"/>
		  	<figcaption>SIFT feature point extraction and matching</figcaption>
	  	</center>
</figure>

Image stitching can be done using the match pairs of feature points, basically we need to solve a linear equation system to get a homogeneous matrix, which can transform points from one coordinate system to another, combined with some algorithms like RANSAC to remove outliers, and some image fusion techniques, we can now stitch the images together.

<figure>
		<center>
		  	<img src="./images/castle_stitch.jpg" alt="stitch" width="100%" height="100%"/>
		  	<figcaption>image stitching</figcaption>
	  	</center>
</figure>

* ### Image matting

Image Matting is a big topic in computer vision, generally an alpha matte is considered to be the output and a scribble image or a trimap as the input. The following is the result of my reimplementation version of the famous "a closed-form solution to natural image matting".

<div style="float:left">
	<figure>
		<center>
		  	<img src="./images/image_matting/azu.jpeg" alt="Daniel Wu" width="45%" height="45%"/>
		  	<img src="./images/image_matting/azu.png" alt="Daniel Wu alpha matte" width="45%" height="45%"/>
		  	<figcaption>Picture of Daniel Wu and its alpha matte</figcaption>
	  	</center>
	</figure>
</div>

After getting the alpha matte, We can easily pull the figure out, and put it else where we want. The following is a picture with a transparent background, generated using the alpha matte above.

<figure>
	<center>
	  	<img src="./images/image_matting/azu_trans.png" alt="Daniel Wu matting" width="45%" height="45%"/>
	  	<figcaption>Daniel Wu Matting</figcaption>
	</center>
</figure>


Closed-form matting is great, but it suffers from its extremely long processing time, because it needs to solve a huge sparse linear system. There are also many other matting algorithms, here are the results of one of my own:

<div style="float:left">
	<figure>
		<center>
		  	<img src="./images/image_matting/2.jpg" alt="Girl" width="45%" height="45%"/>
		  	<img src="./images/image_matting/2.png" alt="Girl matte" width="45%" height="45%"/>
		  	<figcaption>Girl</figcaption>
		</center>	
	</figure>
</div>


<div style="float:left">
	<figure>
		<center>
		  	<img src="./images/image_matting/641.png" alt="Dancing" width="45%" height="45%"/>
		  	<img src="./images/image_matting/641_res.png" alt="Dancing matte" width="45%" height="45%"/>
		  	<figcaption>Dancing</figcaption>
		</center>
	</figure>
</div>


<div style="float:left">
	<figure>
		<center>
			<img src="./images/image_matting/ts.jpeg" alt="angel" width="45%" height="45%"/>
			<img src="./images/image_matting/ts_res.png" alt="angel matte" width="45%" height="45%"/>
			<figcaption>Angel</figcaption>
		</center>
	</figure> 
</div>  

different objects are marked in different colors.

* ### Haze removal  

This is a reimplementation of "Single Image Haze Removal Using Dark Channel Prior", using fast guided filter for the matting part.

<div style="float:left">
	<figure>
		<center>
		  	<img src="./images/HazeRemoval/canon.jpg" alt="city" width="45%" height="45%"/>
		  	<img src="./images/HazeRemoval/dehazed_canon.jpg" alt="dehazed city" width="45%" height="45%"/>
		  	<figcaption>City</figcaption>
	  	</center>
	</figure>
</div>

<div style="float:left">
	<figure>
		<center>
		  	<img src="./images/HazeRemoval/2.jpg" alt="tree" width="45%" height="45%"/>
		  	<img src="./images/HazeRemoval/dehazed_2.jpg" alt="dehazed tree" width="45%" height="45%"/>
		  	<figcaption>Tree</figcaption>
	  	</center>
	</figure>
</div>

The result is overwhelmingly good, and fast as well, since fast guided filter is used. The algorithm uses the dark channel as the approximate transmission map, and uses matting algorithms or guided filter to refine the approximate transmission map, and finally, reconstruct a haze-free image using the refined transmission map.

* ### Template Match

What template match do is to search an image for a template pattern and mark them, like use the bat below as the template, we can locate all the bats in another image.

<figure>
	<center>
	  	<img src="./images/template_match/bat.png" alt="bat" width="45%" height="45%"/>
	  	<figcaption>bat template</figcaption>
	</center>
</figure>


<figure>
	<center>
	  	<img src="./images/template_match/match.png" alt="match" width="100%" height="100%"/>
	  	<figcaption>match</figcaption>
	</center>
</figure>

This is the result of an algorithm called Generalized Hough Transform, the algorithm basically builds a R-table first, and vote for the position, scale and rotation of the template according to the R-table.

* ### Corner Detection

Harris corner detection takes advantage of the fact that the intensity of a corner varys drastically in all directions. So it converts the detection task into a task to maximize the change of intensity in a window for all directions. After some mathematic manipulation, an elegant conclusion shows that we need only to calculate the determinant and trace for some 2x2 matrices.

<figure>
	<center>
	  	<img src="./images/corner_detection/harris.jpg" alt="harris corner" width="100%" height="100%"/>
	  	<figcaption>harris corner</figcaption>
	</center>
</figure>







