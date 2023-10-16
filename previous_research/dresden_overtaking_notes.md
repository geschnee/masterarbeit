
# Notizen zu A Platform-Agnostic Deep Reinforcement Learning Framework for Effective Sim2Real Transfer in Autonomous Driving

Die Autoren sehen full autonomous driving als eine Kombination mehrerer Subtasks:
- car following
- lane following- overtaking
- collision avoidance
- traffic sign recognition

Training in Simulation + Transfer zur echten Welt --> Sim2Real gap

addressing Sim2Real gap:
- domain randomization
- domain adaptation
- knowledge distillation
- meta reinforcement learning
- robust RL


Sim2Real methods already enable lane following and collision avoidance


authors build framework for lane following (Scenario 1) and safely overtaking slower vehicles (Scenario 2)

framework/agent consists of two modules:
- platform-dependent perception module
- universal DRL control module

## platform-dependent perception module

- abstraction layer
	- addresses the heterogeneity between different platforms
- enhances generalization by extracting task-relevant affordances from the traffic state

Is the Sim2Real gap supposedly addressed with this module alone? - Figure 1
It seems like it. This module ensures the generalization of the trained agent

## universal DRL control module

- uses information from perception module
- trained in simulator
- LSTM

They introduce a feature that scales action output to allow testing fast and slow driving modes.


Contributions
- separation of perception and control module allows for easy transfer between environments
- control agent is trained in simple env and transfered to more complex envs
- good results in lane following and overtaking



## Results

5 metrics for lane following
- survival time Ts
- traveled distance dt
- deviation from center of lane deltal
- orientation deviation from tangent of lane center deltao
- major infractions im (time outside of drivable zone)

Objective of lane following:
- drive within boundaries of right lane with minimal deviations from center and orientation
- evaluated as a weighted score of the 5 metrics (the reward function for training is different)

evaluating overtaking
- success rate of overtaking maneuvers

evaluation in real-world environments
- lateral deviation and orientation deviation are measured from the perception module
- average velocity
- infractions

### environments
training and real-world scenarios use a circular map (do they drive in both directions? left and right turns?)
evaluation uses 5 different diverse maps



### overtaking

overtaking mode is engaged when slower vehicle is in perception field


## Perception module

essentially a camera with a few filters
distance sensor as well

what is the output provided to the control module?
images or the deviation from middle of road and orientation?
yes middle road displacement and angle offset 

pipeline:
1. illumination correction
2. edge detection mit canny filters
3. HSV thresholding to extract the expected relevant sections (lines)
4. nonlinear non-parametric historgram filter to determine the center lane displacement and angle offset

## Control module

VFG as guidance states for optimal trajectory
during eval VFG is not available --> replaced by estimates of delta by perception module)

### Input

- lateral displacement
- angle offset (between current heading and heading in optimal trajectory VFG)
- time-to-collision with other vehicles (when applicable)
- vt velocity of ego vehicle

### Action space

- speed command
- steering angle

### Reward function

-1 if collide or out of boundary
weighted sum of 
- error from target path
- driving efficiency
- penalty for driving in opposite direction 











