# Path Planning Project
---
## Project Description
In this project, we attempted to navigate a vehicle around a track without colliding with other vehicles, leaving the road surface or exceeding the speed limit.

### Trajectory Planning

Most of the trajectory planning code was taken from the walkthrough video.  The spline library was used to plot a path of 50 points that was fed to the simulator.  This path was updated every .02 seconds, taking into account other vehicles and desired lane changes.

### Lane Change Decision Making

A small finite state machine was used to decide when to change lanes, and when to stay in the current lane (KEEP LANE).  The state machine had four states: KEEP LANE, PREPARE LANE CHANGE, LANE CHANGE LEFT and LANE CHANGE RIGHT.  When a vehicle was detected in our vehicle's path, a test was done to see if the other lanes were open for a lane change, and then how far and how fast the other lane's vehicles were traveling.  A cost function computes the cost of changing lanes or staying in the current lane, and chooses the path with the least cost.  The spline path is then recomputed for any lane change.
There are several state variables that keep track of lane speeds, distances, and safe distances for lane changing and collision avoidance.
We also include a small delay when changing lanes so that the finite state machine doesn't execute another lane change before the first one is completed.

#### Shortcomings and Improvements
There are still some problems with this implementation.  Occasionally, another vehicle would change lanes into our car and cause a collision.  Additional code could be added to try to fix this problem.
When a car is detected in front of the ego car, our car slows considerably if the front car is blocking us for a long amount of time.  We could account for this by slowing to the front car's speed, instead of continuing to slow until the front car has gained appropriate distance.
