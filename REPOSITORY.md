# Revo2 Retarget — Joint Thumb

This repository is the `joint_thumb` variant of the MANUS-to-Revo2 ROS 2
retargeting pipeline. Its default configuration is fixed to direct joint
semantics mapping.

## Algorithm

- Index, middle, ring and pinky use weighted MANUS ergonomics mapping.
- `ThumbMCPSpread` controls the Revo2 thumb metacarpal joint.
- A weighted combination of thumb MCP/PIP/DIP stretch controls the Revo2 thumb
  proximal joint.
- No inverse-kinematics result is used for the final thumb command, avoiding IK
  branch changes and improving runtime predictability.

Default configuration:

```text
src/brainco_capabilities/manus_revo2_retarget/config/retarget.yaml
```

The effective default is `algorithm: joint_thumb`.

## Quick start

```bash
conda create -n manusglove python=3.10 -y
conda activate manusglove
python -m pip install -r requirements.txt
source /opt/ros/humble/setup.bash
python -m colcon build --symlink-install --packages-select \
  manus_ros2_msgs manus_ros2 revo2_description revo2_driver \
  manus_revo2_retarget
source install/setup.bash
ros2 launch manus_revo2_retarget real_hand_pipeline_launch.py \
  hand_mode:=right controller_backend:=ros2_control
```

The proprietary MANUS runtime libraries and BrainCo Stark SDK binaries are not
included. Follow the main README before building on a new machine.

