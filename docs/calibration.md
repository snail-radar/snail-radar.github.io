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

Initial relative positions between sensors are measured manually, and initial relative orientations are obtained from the CAD drawing. These parameters are then refined through several methods.

![coordinate-frames]({{ site.baseurl }}/assets/images/coordinate-frames.png){:width="90%"}
![coordinate-frame-mti3dk]({{ site.baseurl }}/assets/images/coordinate-frame-mti3dk.png){:width="90%"}


The coordinate frames' rough orientation relative to a platform, either a person, an e-bike, or an SUV, is given in the below table.
**The exact extrinsic parameters are given in the [matlab scripts](https://github.com/snail-radar/dataset_tools/tree/main/matlab) and the ROS1 launch files in every sequence's folder.**

<table>
  <thead>
    <tr>
      <th>Frame</th>
      <th>Comment</th>
    </tr>
  </thead>
  <tbody>
    {% assign frames = site.data.coord_frames %}
    {% for row in frames %}
    <tr>
      <td>{{ row.frame }}</td>
      <td>{{ row.comment }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>


```tip
The Oculii point clouds' xyz coordinates are in the forward left up frame,
whereas the Oculii's native frame is a right down forward frame.
The two frames are related by a constant rotation.
More info about the Oculii native frame and the definitions of azimuth and elevation angles can be found in 
[its manual](./manuals/Manual Edition 0.5.41 Dec2021 Eagle G7.pdf)

```