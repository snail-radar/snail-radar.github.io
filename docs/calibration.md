---
sort: 4
---

# Synchronization and Calibration

Since it is challenging to sync all sensors in hardware, we propose a scheme to ensure that their messages are stamped by the same virtual clock.
The scheme first uses the lidar data as a bridge to map all sensor message timestamps to the GNSS time.
Then, the constant time offset between message topics is estimated by odometry and correlation algorithms.
The sync accuracy is expected to be better than 10 ms.
Please refer to our dataset paper for details.

## Sensor Calibration
For the dataset, we define the body frame to have the same origin as the XT32 lidar, but with an orientation such that its x-axis points forward, y-axis points left, and z-axis points up. Thus, the body frame relates to the XT32 frame by a known rotation. The extrinsic parameters of all sensors are provided relative to the body frame.

**The calibration data are available [here](https://github.com/snail-radar/dataset_tools/tree/main/matlab)**.

Initial relative positions between sensors are measured manually, and initial relative orientations are obtained from the CAD drawing. These parameters are then refined through several methods.

![coordinate-frames]({{ site.baseurl }}/assets/images/coordinate-frames.png){:width="90%"}
![coordinate-frame-mti3dk]({{ site.baseurl }}/assets/images/coordinate-frame-mti3dk.png){:width="90%"}
