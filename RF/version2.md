
### This reward function has been inspired by [Scott Pletcher's reward function (Do checkout his awesome repo on DeepRacer!)](https://github.com/scottpletcher/deepracer/blob/master/iterations/v4-SelfMotivator.md). I kept the reward function but made changes in the action space. 

### Action Space
____

Steering Angle of 30 degrees with Steering granularity of 5.
Maximum speed of 3 m/s and speed granularity of 3. 

I increased the speed here to try and fasten the process of track completion. I kept the default hyperparameters and trained the model for 5 hours. 

### Testing in Virtual Environment.
____

Although, the car was slow in completing the track, it always managed to do so without going out of bounds. I am curious to know if training the same for more and having a better incentive for speed would reduce the completion time without compromising on the consistency of track completion.

### Reward Function.
____
    
    if params["all_wheels_on_track"] and params["steps"] > 0:
        reward = ((params["progress"] / params["steps"]) * 100) + (params["speed"]**2)
    else:
        reward = 0.01
        
    return float(reward)


```python

```


```python

```
