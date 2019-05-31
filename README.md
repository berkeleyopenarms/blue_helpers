# blue_helpers
Helpful tools when using blue!



## Pose Commander Scripts

### Right Arm Only

> These scripts presume that you've already started up the arm in the startup position.

- `$ rosrun blue_helpers right_home_pose_commander`
  - Brings the arm back home to the startup position
- `$ rosrun blue_helpers right_pickup_ready_pose_commander`
  - Brings the arm to a ready position for picking up objects



## Pose Reporter Scripts

> These scripts provide a useful interface for checking out the state of the Blue arm.
>
> Though you can get this information using helpful tools like `tf_echo`