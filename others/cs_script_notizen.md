# Explanation of the scripts

## AIEngine.cs

* Controls the CarObject via its 4 wheels
* takes the output of the NN via the SetInput function
* can return the CarObject's velocity

Serves as the "Driving Engine" for the CarAgent.cs Script

Why does the CarObject have 4 wheels if the JetBot has 3?

## CameraFollow.cs

* sets the camera's position equal to the body plus an offset

Included in the Camera attached to the JetBot Clone's camera. (in fixed update/every frame)

Why is this script needed?
Is it needed since the JetBot clone is a prefab?

## CarAgent.cs

* receives the output of the neural network and passes it forward to AIEngine.cs
* records stats using DataFrame.cs, e.g. avg velocity
* gives reward for velocity
* checks for episode timeout -> negative reward and end of episode
* has a method included for calculating distance to FinishLine for additional reward but is not used
    * reward for distance to next goal would be good as well
* takes pictures using camera and call Image Recognition pipeline
    * keeps memory of obstacles if in that mode
    * pipeline call: GetCooridnatesNClosestObstacles + TraceObstcalePosition
* respawn using GameManager.cs
    * fixed (start) position
    * random position


## CheckpointManager.cs

* detects collisions of the CarObject
    * gives reward accordingly
    * ends episodes when colliding with obstacles, border and point on the line outside of goals
    * extends episode when goal hit

Is included in the CarObject
CarAgent.cs also gives out rewards

## DataFrame.cs

* Saves Data to CSV

## DrivingEngine.cs

* similar to AIEngine.cs
* takes output of NN with SetInput
* controls the wheels / motors

## GameManager.cs

* spawns objects on the Map
* uses ObstacleMap.cs heavily

according to comments this class can also spawn a human player but I don't see the option yet

## ObstacleMap.cs

* generates fixed and random obstacle maps
* generates fixed and random spawn locations for JetBot
* JetBot random spawn rotation is between -45 and +45 Degrees






