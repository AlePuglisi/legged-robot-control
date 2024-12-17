# legged-robot-control
MATLAB | Simulink | robotics-toolbox | Legged Robot | Modeling and Control | URDF to DH 

This Repository contains the MATLAB code and Simulink scheme for modeling and control of LIMBERO+GRIEEL (legged robot prototype of Space Robotics Lab (SRL), Tohoku University ).<br/>

This is a "sequel" of my work there as a research student, for my Master's thesis at Politecnico di Milano. <br/>
At SRL I updated the ROS 2 software and implemented stability algorithms. <br/>
Now I'm working on modeling and performance analysis of an alternative control structure. 

## Objectives

### In the previous episode:
The software I used at SRL is written in C++ and is based on ROS 2 for communication and control.<br/>
The robot joint controllers are implemented using ros2_control, and the simulation is based on Gazebo Classic.<br/>
For the tuning of the joint_trajectory_controller and the refinement of robot [URDF](https://docs.ros.org/en/humble/Tutorials/Intermediate/URDF/URDF-Main.html), I take an iterative tuning approach.<br/>

Some of my tasks as a member of SRL Rover Team have been: 
- Update the software with 3 additional joints in each limb (new end-effector transformable module)
- Adjust URDF to make the simulation more reliable
- Update ros2_control configuration and retune the joint controller PID gains
- According to support polygon stability theory, implement an algorithm for base positioning and end-effector module transformation.
- Make experiments on the real Hardware
  
### In the next episode: 
Because of the lack of a model-based rigorous control tuning, I took a different approach to the control of the robot leg.<br/> 
Also, to provide better insight into the algorithm performances, a different modeling approach based on DH is taken. <br/>
With this model, I attempt to define new useful performance indices.

Given the robot URDF:
- Convert URDF into Denvit Hartemberg model, and define it in the robotics-toolbox as a [SerialLink](https://www.petercorke.com/RTB/r9/html/SerialLink.html) <br/>
  (Notice, I didn't use the MATLAB [Robotics System Toolbox](https://it.mathworks.com/products/robotics.html), but the previous version of Peter Corke [toolbox](https://petercorke.com/toolboxes/robotics-toolbox/).
  I took this choice because using rigidBodyTree for dynamic simulation is computationally demanding)
- Single limb dynamic model identification 
- Tune independent joint controllers for the robot leg
- Performance analysis of the model-based controller gains, and gain correction if needed.
- Implement a gravity compensation algorithm (then include it in ROS 2). 
- Expand to 4-legs simulation and control
- Define new performance index for legged-robots
- Analyze the quality of some base postures, using defined indices
- Implement the new joint controllers in the original ROS 2 code, and simulate using Gazebo.

## Description 
To better handle the robot joint controllers and model identification, I take the xacro file, convert it in a single URDF
