# 2022Fall_CS470_FinalProject

## Task Purpose:
  Integrate Mini-DARPA modeling into scene recognition based on SLAM algorithm to reduce the repetition rate and improve the recognition accuracy of difficult maps. Our project aims to use Turtlebot Burger to realize automatic scanning and mapping of scenes, path planning and automatic cruise (full coverage).
  
## Video Demo
  Since the focus of this project is to use TurtleBot to achieve the established tasks, we have integrated multiple open source algorithms and data packages, which is time-consuming in environment establishment and early debugging. **In order to save your time, we have recorded a demonstration video:** <br/>
  Autonomous SLAM Mapping: https://www.youtube.com/watch?v=CHH_Y6_o5RA<br/>
  Mapping (Real machine demonstration): https://www.youtube.com/watch?v=rr8u_8UJrLU<br/>
  Dynamic Path Planning: https://www.youtube.com/watch?v=bYGZfkeKLG8

## Prerequisites
  * The whole process is realized based on the indoor environment and manual layout of the ***E3-2110 laboratory room*** assigned by this course. Therefore, all experimental operations and results are generated and used based on the structural layout in the E3-2110 room. 
  * The ```mappp.yaml``` in ```minidarpa/maps/``` is the map we constructed during the experiment for E3-2110 laboratory room. The real experiment result videos are demonstrated as Youtube videos showed in the last section. Below are the guide to run the codes in simulation environment for demonstration.
  * The codes include two parts. The ```minidarpa``` includes an open source package for full coverage path generation based on Backtracking Spiral Algorithm. There are also some launch files to start the simulations or conduct the experiments in real environment. The ```explore_lite``` includes an open source package for robot exploration and SLAM in unknown environment. 

## Dependencies
  Please install the turtlebot3 dependencies used in the turtlebot tutorial in our course.
```
sudo apt install ros-${ROS_DISTRO}-turtlebot3 ros-${ROS_DISTRO}-navigation ros-${ROS_DISTRO}-dwa-local-planner ros-${ROS_DISTRO}-slam-karto
```

## Implementation Process
  * Step 1: Environment Construction
  * Step 2: Independent Exploration and Mapping
  * Step 3: Path Planning
  * Step 4: Autonomous Cruise
  
### Environment Construction
  ![image](https://user-images.githubusercontent.com/81891626/206839541-847de621-690e-4d49-a9f4-16baa2256ffe.png)
  
  ![image](https://user-images.githubusercontent.com/81891626/206839545-bfda39ad-27d3-43a8-bde8-d31b7f89ca33.png)

### Independent Exploration and Mapping
  To begin with:
  ```
  mkdir mini_DARPA_ws
  cd mini_DARPA_ws
  mkdir src
  Clone the ???minidarpa??? and ???explore_lite??? in ???src???
  catkin_make
  ```
  We can begin the map exploration test first (You can skip it if you just want to test the coverage mapping).
  Then open another terminal:
  ```
  cd mini_DARPA_ws
  source devel/setup.bash
  export TURTLEBOT3_MODEL=burger 
  roslaunch minidarpa Map_explore.launch
  ```
  You can see a robot begins to move in an environment (It may take sometime (2-3 min) to start the movement):
  
  ![image](https://user-images.githubusercontent.com/81891626/206838416-6ef84114-b91d-4620-b7fe-a5c9b170f3f9.png)
  
  The robot will continue to move untill explore the full environment:
  
  ![image](https://user-images.githubusercontent.com/81891626/206838437-923e92b7-cf4f-4b04-afe5-55204c4b0a4e.png)
  
  After that, we can save the map.
  
  Then open a new terminal (Don???t close the old terminal)
  ```
  rosrun map_server map_saver -f ~/mini_DARPA_ws/src/minidarpa/maps/house11
  ```
  The map generation mission is then done.
  
  ***Known issue:*** During the exploration, robot may stuck in the environment, because the navigation goal is set in the unkown environment by the algorithm. It needs time to find another navigation goal in the environment. However, the robot can find a exploration path in the end eventually.

  After the map is obtained, the coverage path is generated and the robot can follow the path.
  
  ***Take the example of E3-2110 Room, the final result you see looks like this:***
  
  Self-discovery process:
  
  ![image](https://user-images.githubusercontent.com/81891626/206839553-363e7f4d-a1f0-46b5-9b57-644ed64d53cb.png)
  
  <img width="800" alt="????????????_20221130163447" src="https://user-images.githubusercontent.com/81891626/204734913-15801071-41a1-49c4-a818-aa417c043bce.png">

  Final floor plan of room E3-2110:
  <img width="800" alt="????????????_20221130163615" src="https://user-images.githubusercontent.com/81891626/204735152-19de379b-ffba-4e56-bf76-5582e83bbac2.png">
  
  
### Path Planning
  If you conduct the map saving code in the last Step:
  
  Close the previous terminals, then modify the generated   ```house11.yaml``` under the   ```/mini_DARPA_ws/src/minidarpa/maps/``` from   ```image: /home/XXX/mini_DARPA_ws/src/minidarpa/maps/house11.pgm``` to  ```image: house11.pgm``` save and close the file.

  Then open another terminal:
  ```
  cd mini_DARPA_ws
  source devel/setup.bash
  export TURTLEBOT3_MODEL=burger 
  roslaunch minidarpa Start_cleaning.launch
  ```
  
  You can see a path generated by the algorithm, and robot follows the path:
  
  ![image](https://user-images.githubusercontent.com/81891626/206839313-2f2f9e77-7385-4d8f-8cda-9ac33b7f5232.png)

  ***Take the example of E3-2110 Room, the final result you see looks like this:***
  
  <img width="800" alt="????????????_20221201130431" src="https://user-images.githubusercontent.com/81891626/204963225-f59c3eaf-309f-49ac-a3d2-c8086fd40c06.png">
  
  ***Known issue:*** Since the simulated environment is all built by ourselves, there are gaps in the barriers, which makes the radar think that it is a feasible route, but the actual situation is not passable, which is an acceptable error.

### Autonomous Cruise
  Divide the original map obstacle-free area according to the size of the robot, and traverse all the divided areas directly after division. Traversing directly according to certain rules does not guarantee the optimal path, but can achieve relatively optimal and complete basic functions.
  ![????????????_20221201131011](https://user-images.githubusercontent.com/81891626/204963853-ba671da0-95a9-4d50-a0a8-0a4e8996f6e4.jpg)
