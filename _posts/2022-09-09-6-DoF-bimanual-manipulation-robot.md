---
title:  "6 DoF Bi-manual Manipulation"
mathjax: true
layout: post
categories: media
---

As a part of my master's thesis, for implementing the inverse dynamics algorithm to an upper-body bi-manual robot base on my supervisor [paper](https://www.researchgate.net/publication/320330613_Inverse_Dynamics_Control_of_Bimanual_Object_Manipulation_Using_Orthogonal_Decomposition_An_Analytic_Approach), Dr. [Mohammad Shahbazi](https://scholar.google.com/citations?user=bluC-SMAAAAJ&hl=en), in a 3D simulator, I had to work with __Gazebo__. First the [URDF](http://wiki.ros.org/urdf) model of the robot was prepared by the help of my teammate, Ms [Nooshin Kohli](https://github.com/nooshin-kohli), then other dependencies like torque controllers of joints, launch file, and etc attached, finally of courese the script of algorithm was written by a great deal of work. Actually the fundaments of algorithm for a 2D simulation was obtained beforehand by my supervisor and I developed it to 3D simulation in Gazebo.

<p style="text-align:center;">
  <img style="text-align:center;" width="755" height="199" src="/img/6dof_bimanual_manipulation/fig_123.png" alt="gazebo simulation">
</p>

Although the control approach is dynamic cancellation, It was cumbersome to adjust joints' `damping` and `friction` in URDF model.

<p style="text-align:center;">
  <img style="text-align:center;" width="651" height="269" src="/img/6dof_bimanual_manipulation/control_system_caption.png" alt="control system diagram">  
</p>

First the desired trajectory of the object (green box) is calculated, a triangular path in this case. After that, regrading dynamic equations of robot and object are derived in joint space, it is necessary to determine desired joint position, velocity and acceleration.
What is notable in this method is that, the effect of force and torque of object in hands' contacts (end-effectors) of robot, removes by a projector, obtained from __orthogonal decomposition__ of a specially defined jacobian. Therefore the total dynamics equation becomes free from the effect of the object, so it is possible to specify inverse dynamics of arms analytically.

<p style="text-align:center;">
  <img src="https://latex.codecogs.com/svg.image?\hat{M}\ddot{q}&plus;\hat{h}=S^{T}\tau=S^{T}\tau&space;&plus;&space;J_{g}^{T}\lambda_{a};\mathbf{(1)}&space;" title="equation of motion of bimanual robot and object" /> <br>
</p>

<p style="text-align:center;">
  <img src="https://latex.codecogs.com/svg.image?P(\hat{M}\ddot{q}&plus;\hat{h})=PS^{T}\tau;&space;\mathbf{(2)}" title="reduced equation" />
</p>

Some of the results are plotted below,

<p style="text-align:center;">
  <img style="text-align:center;" width="1266" height="390" src="/img/6dof_bimanual_manipulation/trajectory.png" alt="object trajectory">  
</p>

<p style="text-align:center;">
  <img style="text-align:center;" width="589" height="338" src="/img/6dof_bimanual_manipulation/right_arm_torque_profile.png" alt="right arm torque profile">  
</p>

I have uploaded the video of the simulation on my LinkedIn profile, [check here](https://www.linkedin.com/posts/hamid-manouchehri_manipulation-robotics-gazebo-activity-6978368963860733952-6Sh2?utm_source=share&utm_medium=member_desktop), please. Also, the source code is on my GitHub page, but I'm not allowed to reveal it yet.


