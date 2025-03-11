<div align="center">
    <img src="https://github.com/user-attachments/assets/509197d7-4ae3-4f43-bad2-7acd970c8017" height="370px">
</div>

Developed an algorithm for predicting RC car steering angles using cone detection for autonomous navigation, built with Docker and CMake for testing and pipeline integration, as part of the DIT639 Cyber-Physical Systems project.

## Acknowledgments
Special thanks to our professor [@chrberger](https://github.com/chrberger) for his contributions to the foundational libraries used in our project, including OpenDLV, libcluon, and the opencvv template file, which have been instrumental in the development of our cyber-physical systems project.

## Installation

1. Clone this repository into your preferred directory:
   
   ```bash
   git clone git@github.com:danielvdh24/cphysical-systems.git
   ```

2. Navigate to the project directory and build the Docker image:
   ```bash
   cd cpp-opencv
   docker build -f Dockerfile -t anglecalculator .
   ```

3. Run the microservices
> For each of the following steps, open a new terminal window (Ctrl+Alt+T) or a new tab (Ctrl+Shift+T) to run the services in parallel. Ensure you are in the recordings directory before running the commands.

   - Start OpenDLV Vehicle View  
     This service visualizes vehicle data.
     ```bash
     docker run --rm -i --init --net=host --name=opendlv-vehicle-view \
       -v $PWD:/opt/vehicle-view/recordings \
       -v /var/run/docker.sock:/var/run/docker.sock \
       -p 8081:8081 chrberger/opendlv-vehicle-view:v0.0.64
     ```

   - Start H264 Decoder  
     This service decodes the video feed.
     ```bash
     docker run --rm -ti --net=host --ipc=host -e DISPLAY=$DISPLAY \
       -v /tmp:/tmp h264decoder:v0.0.5 --cid=253 --name=img
     ```

   - Start the Steering Wheel Angle Calculator  
     This is the main microservice for calculating the steering wheel angle.
     ```bash
     xhost +
     docker run --rm -ti --net=host --ipc=host -e DISPLAY=$DISPLAY \
       -v /tmp:/tmp anglecalculator:latest --cid=253 --name=img \
       --width=640 --height=480 --verbose
     ```

## Contributers
<table>
  <tr>
    <td align="center"><img src="https://secure.gravatar.com/avatar/3056b6827d3d959ea87306c4d2dd0c6a?s=800&d=identicon" width="100px;"/><br/><sub><b>Daniel Van Den Heuvel</b></sub><br>@danielvh24</td>
    <td align="center"><img src="https://secure.gravatar.com/avatar/3271ba4e481b7c393b650b96a17344d0?s=800&d=identicon" width="100px;"/><br/><sub><b>Kai Rowley</b></sub><br>@rowley</td>
    <td align="center"><img src="https://secure.gravatar.com/avatar/82899676cb5f15c859ed9bd18921b3033716285c1331ed8406c725e91f95bd80?s=800&d=identicon" width="100px;"/><br/><sub><b>Sam Hardingham</b></sub><br>@samha</td>
    <td align="center"><img src="https://git.chalmers.se/uploads/-/system/user/avatar/3455/avatar.png?width=400" width="100px;"/><br/><sub><b>Nasit Vurgun</b></sub><br>@nasit</td>
  </tr>
 </table> 
