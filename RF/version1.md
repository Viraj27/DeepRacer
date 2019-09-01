
Version 1 was my first attempt at creating a reward function after going through the course. I tried combining the multiple sample models that were given already and tried rewarding the model based on the situation it found itself in. This is a very crude reward function and I came up with this after multiple failed attempts of trying to finish the track using a few parameters but then decided to combining all of them and see what transpires :)


### Action Space
____

Steering Angle of 30 degrees with Steering granularity of 7.
Maximum speed of 6 m/s and speed granularity of 3.

### Hyperparameter tuning

I opted for a batch size of 256 images for gradient descent as I wanted the model to work on a lot many images over a long period of time. I started off with the loss type of Mean Squared Error because running this same model once before gave me positive convergence results so I could afford to train faster by taking bigger increments with each update. I kept the learning rate as 0.0002 just to be a bit safer even though I obtained good convergence previously. Finally, I kept the number of experience episodes at 30 so that my model could factor in a variety of experiences before the next iteration.

### Testing in Virtual Environment.
____

This model passed 2 of the 3 tests successfully and the time was not bad also!. The fastest lap was 19.758 seconds

### Reward Function.
____
    
    # Read input parameters
    track_width          = params['track_width']
    distance_from_center = params['distance_from_center']
    all_wheels_on_track  = params['all_wheels_on_track']
    progress             = params['progress']
    speed                = params['speed'] 
    # initial reward - range of assignment of reward is [-1,1]
    reward = 0 
    
    # Calculate 3 markers that are at varying distances away from the center line
    marker_1 = 0.1 * track_width
    marker_2 = 0.25 * track_width
    marker_3 = 0.5 * track_width
    
    # Give higher reward if the car is closer to center line and vice versa
    if distance_from_center <= marker_1:
        reward += 1.0
    elif distance_from_center <= marker_2:
        reward += 0.5
    elif distance_from_center <= marker_3:
        reward += 0.1
    else:
        reward += -1  # likely crashed/ close to off track
        
    # If all wheels are on track then reward, else give a penalty.
    
    if all_wheels_on_track:
        reward += 1
    else:
        reward += -1
    
    # Based on progress, award reward points
    
    if progress < 25:
        reward += 0.25
    if progress > 25 and progress < 50:
        reward += 0.50
    if progress > 50 and progress < 75:
        reward += 0.75
    if progress > 75 and progress < 99:    
        reward += 0.90
    if progress == 100:
        reward += 1.0
        
    # Rewarding high speeds
    if speed == 2:
        reward+= 0.1
    elif speed == 4:
        reward+= 1.0
    else:
        reward +=0.5
        
    return float(reward)


```python

```


```python

```
