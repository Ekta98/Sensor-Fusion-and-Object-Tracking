# Writeup: Track 3D-Objects Over Time

Please use this starter template to answer the following questions:

### 1. Write a short recap of the four tracking steps and what you implemented there (filter, track management, association, camera fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?


### 2. Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)? 


### 3. Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?


### 4. Can you think of ways to improve your tracking results in the future?


# Self-Driving Car Engineer Nanodegree 

This is a submission for the  second course in the  [Udacity Self-Driving Car Engineer Nanodegree Program](https://www.udacity.com/course/c-plus-plus-nanodegree--nd213) : Sensor Fusion and Tracking. 


## Sensor Fusion and Object Tracking

We have used the Waymo Open Dataset's real-world data and applied an extended Kalman fusion filter for tracking several vehicles in this project. The following are the tasks completed:
- Implement an extended Kalman filter.
- Implement track management including track state and track score, track initialization and deletion.
- Implement single nearest neighbour data association and gating.
- Apply sensor fusion by implementing the nonlinear camera measurement model and a sensor visibility check. 

We create a fusion system that is able to track vehicles over time with real-world camera and lidar measurements!

The project can be run by following command: 

```
python loop_over_dataset.py
```
## Step-1: Extended Kalman Filter

First we implement EKF to track a single real-world target with lidar measurement input over time.     
EKF is implemented in the filter.py file     

# Requirements:   

![image](https://user-images.githubusercontent.com/28135189/216813772-97a8039b-a614-4686-8f83-bd6fd400e502.png)

# Result:   

![image](https://user-images.githubusercontent.com/28135189/216813853-6ba780b7-6db6-484f-a678-a5ca7c997ad1.png)

The RMSE plot shows a mean RMSE of 0.31 

![image](https://user-images.githubusercontent.com/28135189/216813865-d8d0225a-f62b-4690-83f0-82fc370d64dd.png)


## Step-2: Track Management   

Here we have implemented the track management to initialize and delete tracks, set a track state and a track score.      
Changes are made in student/trackmanagement.py     

# Requirements:   

In addition to step 1
![image](https://user-images.githubusercontent.com/28135189/216813977-4e276255-4160-400d-8e9d-dbe99375a024.png)


# Results:

![image](https://user-images.githubusercontent.com/28135189/216814047-ada0b719-ffac-49ae-9913-43646ba5d556.png)


## Step-3: Data Association

In this step, the closest neighbor association correctly matches several measurements to several tracks.     
Implementation is done in student/association.py

# Requirements:     

![image](https://user-images.githubusercontent.com/28135189/216814128-22164350-72c8-4ccf-b2da-690cb9e1fe2d.png)     


# Results:   

![image](https://user-images.githubusercontent.com/28135189/216814646-b21b8986-cea5-46f6-8614-37008852feac.png)    


![image](https://user-images.githubusercontent.com/28135189/216814660-e3eb462b-bb21-462b-99d2-a3ef0731318d.png)    


## Step-4: Camera Sensor fusion

Implementation is done in student/measurements.py


# Results:

The RMSE plot should shows three confirmed tracks. Two of the tracks are tracked from beginning to end of the sequence (0s - 200s) without track loss.

![image](https://user-images.githubusercontent.com/28135189/216814768-19edf05b-e44a-4d4a-86fa-9b5ebbd8831e.png)



## Difficulties Faced in Project

It was difficult to implement the camera- lidar fusion, as I had to implement the camera model and found it difficult to do the coordinate transforms from 3D to 2D image coordinates. Once the transformation was done however it was easy to do the sensor fusion with the help of class lectures.

## Benefits in Camera-Lidar Fusion tracking over Lidar-only tracking

Different sensors perform differently in varying conditions like weather, time of the day, etc. Also different sensors may provide information that some other sensors dont. For ex. Camera gives color/ brightness etc info and images from camera are great for object detection and also classification. On the other hand Lidar performs better in low brightness /visibility or in blurry conditions such as foggy/rainy weather conditions. Lidar measurements which have accurate depth information. So, the fusion of cameras and lidars compensate their weaknesses. For stabilized object tracking, sensor fusion should combine multiple sensors. So camera data combined with Lidar can provide better results. This is also seen in our results.

## Real-life challenges:

A sensor-fusion system could be confronted with a variety of real-world issues such as :

- Multiple tracks and measurements provide a precise correlation. The thresholds for gatting should be properly set to avoid un-necessary wrong correlations.    
- Sensor calibration is one area that would be challenging in real world, as in this project we are using a public dataset for this experiment, so it eliminates the need for sensor calibration as extrinsic parameters are already defined here.     


## Improvement opportunity:

- Adapt the Kalman filter to also estimate the object's width, length, and height, instead of simply using the unfiltered lidar detections as I did.
- Use a non-linear motion model, e.g. a bicycle model, which is more appropriate for vehicle movement than our linear motion model, since a vehicle can only move forward or backward, not in any direction.
- The project should carry out the Camera-LiDAR Fusion Monitoring.






