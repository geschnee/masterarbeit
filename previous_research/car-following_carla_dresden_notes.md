

# use Carla and Robot Operating System

the vehicles in this paper exchange information between them using the ROS middleware
such as velocities, ...

leader-follower pair

Input to neural network consists of sensory information such as position and velocities of own and leader vehicle

interesting normalization of input space

output space are acceleration values (positive and negative)
reverse controller turns the acceleration into throttle/brake commands

reward function as a weighted sum of desired behaviour properties


DRL with real data:
-they first train with data exclusively from simulation (data collected using RL policy)
-then mix that data with real data and further update the policy based on that mixed data


## most interesting part - reverse controller - carla controller

the reverse controller converts the acceleration values into throttle/brake commands

reverse controller is a trained neural network

when changing the vehicle model, the reverse controller needs to be retrained, instead of the entire policy

this is very interesting and could be used to bridge the gap between simulation and real world 
(movement gap between robot and simulation)

## biggest critique

they just compute the rewards in the real dataset and then include these samples in the replay buffer

there is no analysis of the reward function in the real dataset:
- is the reward obtained in real dataset lower than in the self-play samples? 
    - that would mean the policy was better before the mixing

- possible correction: determine the weights of the reward function based on the real dataset

This is talked about in the conclusion section of the paper (inverse RL).