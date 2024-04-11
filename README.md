# Multi-Object_Tracking_Cars

The problem:
Given a video of many moving objects, and (highly incomplete) information about object locations at each frame, how can you associate objects with locations between frames? In other words, how can you know a measured location in one frame is the same object as a measured location in a later frame? 

The solution:
A recursive bayesion filter, e.g. the Kalman filter, is used to estimate the true trajectory of each car. The process noise and measurement covariance coefficients are determined partially experimentally, but influenced by analytical computations. This reduces the measurement noise as well as allowing the prediction of each object's location even when the object was unrecognized (causing lapses of location data for many frames).

Then, the hungarian algorithm is used to associate predicted locations with locations in the current frame, using a unique identifier (UID). It attempts to assign previously known objects to the new location. The cost matrix is computed with eulerian distance between predicted and current locations. Because the Hungarian algorithm may look for a complete matching, (particularly when the cost matrix is square,) the cost matrix and assignment calculations are modified to exclude cases where the distance is too large. If a matching cannot be found, the current location is assigned a new UID and Kalman filtering instance, and therefore treated as a new object.



RESULT: (Compressed to 6mb, slight alteration to blue text thickness for visibility)

https://github.com/leprucon/MOT-Cars/assets/29313866/7b4a2622-6141-4638-bdcd-da78bf12ecd1



(Green squares represent measured locations. Blue numbers are the assigned UID.)
Through the demo video, the solution is observed to be nearly perfect. Indeed, barring extreme cases, this solution correctly predicts trajectories and associates objects with surprising accuracy.

