# CarND-Kidnapped-Vehicle-P3
This is the Term 3 project on Kidnapped Vehicle localization

# Overview

This project implements a [Particle Filter](https://bit.ly/2A8MHpJ) which was taught is Chapter 13 section of Term 2 class. A vehicle is simulated to be kidnnaped and it need to locate itslef using sensor and map data. A simulator is provided by Udacity ([ downloaded here](https://github.com/udacity/self-driving-car-sim/releases)). This simulator will generate noisy landmark observation from the kidnapped car to the Particle Filter using [WebSocket](https://en.wikipedia.org/wiki/WebSocket). The Particle Filter uses the [uWebSockets](https://github.com/uNetworking/uWebSockets) WebSocket implementation to respond to this observation with the estimated car position. Udacity provides a seed project to start from on this project ([here](https://github.com/udacity/CarND-Kidnapped-Vehicle-Project)).

# Prerequisites

The project has the following dependencies (from Udacity's seed project):

- cmake >= 3.5
- make >= 4.1
- gcc/g++ >= 5.4
- Udacity's simulator.

For instructions on how to install these components on different operating systems, please, visit [Udacity's seed project](https://github.com/udacity/CarND-Kidnapped-Vehicle-Project). This implementation was done Windows 10 OS using Ubuntu Shell. .


In order to install the necessary libraries, use the [install-mac.sh](./install-mac.sh).

# Compiling and executing the project

In this project, Udacity's seed repo provides scripts to clean, compile and run it. These are the following commands you need to run from this repo directory

```
> ./clean.sh
> ./build.sh
> ./run.sh
```
![See Screenshot](./images/ubuntu_shell.PNG)
You will see a message indicating the filter is listening:

```
> ./run.sh
Listening to port 4567

```
![See Screenshot](./images/ubuntu_shell_connected.PNG)

When you open the simulator the following screen appears:

![Simulator first screen](images/simulator_first_screen.png)

Using the right arrow, you need to go to the Kidnapped Vehicle project:

![Simulator Kidnapped Vehicle project](images/simulator_kidnapped_vehicle_project.png)

Clicking on "Select," the simulator for the Kidnapped project start and the Particle Filter informs it is connected:

![Simulator Kidnapped Vehicle project first screen](images/simulator_kidnapped_vehicle_first_screen.png)

Clicking on "Start" button, the vehicle starts moving, and the blue circle(the filter calculated position) moves with it. After a while, the simulator informs you if your Particle Filter passed or failed. Here is an example of the filter passing the test:

![Simulator Kidnapped Vehicle Passed](images/simulator_final_state.png)

# Code description

The Particle Filter is implemented in [src/particle_filter.cpp](./src/particle_filter.cpp):

- Initialization: Particle initialization is implemented at [ParticleFilter::init](./src/particle_filter.cpp#L24) from line 24 to line 62.

- Prediction: The prediction step is implemented at [ParticleFilter::prediction](./src/particle_filter.cpp#L64) from line 64 to line 100.

- Weight's update: This is the more important operation in my opinion. It is implemented at [ParticleFilter::updateWeights](./src/particle_filter.cpp#L64) from line 138 to line 217.

Almost the rest of the magic happens on [src/main.cpp](./src/main.cpp). The event handler declared at [line 49](./src/main.cpp#L49) parse the received message and call the above described Particle Filter methods.
