# 2022Fall_CS470_FinalProject

## Task Purpose:
  Integrate Mini-DARPA modeling into scene recognition based on SLAM algorithm to reduce the repetition rate and improve the recognition accuracy of difficult maps. Our project aims to use Turtlebot Waffle to realize automatic scanning and mapping of scenes, path planning and automatic cruise (full coverage).
  
## Video Demo
  Since the focus of this project is to use TurtleBot to achieve the established tasks, we have integrated multiple open source algorithms and data packages, which is time-consuming in environment establishment and early debugging. **In order to save your time, we have recorded a demonstration video:** <br/>
  Dynamic Path Planning: https://www.youtube.com/watch?v=bYGZfkeKLG8<br/>
  Autonomous SLAM Mapping: https://www.youtube.com/watch?v=CHH_Y6_o5RA

## File Structure

## Prerequisites
  The whole process is realized based on the indoor environment and manual layout of the ***E3-2110 laboratory*** assigned by this course. Therefore, all experimental operations and results are generated and used based on the structural layout in the E3-2110 room. In order to save time, please **directly use the E3-2110 room map** that we scanned and saved: **mappp.pgm**

## Implementation Process
  * Step 1: Environment Construction
  * Step 2: Independent Exploration and Mapping
  * Step 3: Path Planning
  * Step 4: Autonomous Cruise
  
### Environment Construction
  ![微信图片_20221130161451](https://user-images.githubusercontent.com/81891626/204731592-125b096a-6c56-4019-a836-9d89bc8ac3f3.jpg)
  ![微信图片_20221130161454](https://user-images.githubusercontent.com/81891626/204731600-c4da904f-f978-4f0f-9af3-50c161732cc9.jpg)
  
### Independent Exploration and Mapping
  Self-discovery process:
  ![微信图片_20221130163054](https://user-images.githubusercontent.com/81891626/204734246-126d5749-9947-4f44-82c7-243f5247d6c2.jpg)
  <img width="800" alt="微信图片_20221130163447" src="https://user-images.githubusercontent.com/81891626/204734913-15801071-41a1-49c4-a818-aa417c043bce.png">

  Final floor plan of room E3-2110:
  <img width="800" alt="微信图片_20221130163615" src="https://user-images.githubusercontent.com/81891626/204735152-19de379b-ffba-4e56-bf76-5582e83bbac2.png">
  
### Path Planning
  <img width="800" alt="微信图片_20221201130431" src="https://user-images.githubusercontent.com/81891626/204963225-f59c3eaf-309f-49ac-a3d2-c8086fd40c06.png">
  
  ***Problems that still exist:*** Since the simulated environment is all built by ourselves, there are gaps in the barriers, which makes the radar think that it is a feasible route, but the actual situation is not passable, which is an acceptable error.

### Autonomous Cruise
  Divide the original map obstacle-free area according to the size of the robot, and traverse all the divided areas directly after division. Traversing directly according to certain rules does not guarantee the optimal path, but can achieve relatively optimal and complete basic functions.
  ![微信图片_20221201131011](https://user-images.githubusercontent.com/81891626/204963853-ba671da0-95a9-4d50-a0a8-0a4e8996f6e4.jpg)
