---
sort: 7
---

# Known Issues

We have identified several issues in the dataset.

- To save storage space, the resolution of the ZED2i stereo images has been reduced to 640×360 in resolution since Dec 8 2023.
- In some sequences, the ZED2i images and IMU data have lower rates than the nominal values, likely due to low power voltage.
- The Hesai PandarXT-32 Point cloud timestamps should decrease by 0.05 sec to align with the other topics, e.g., X36D IMU. 
This is due to the fact that the KISS-ICP outputs motion at t + dt / 2 but stamps it with t and dt = 100 ms for PandarXT-32.
For sequence 20230920/data2, the point cloud timestamps should instead increase by 0.05 sec as its lidar time offset -0.07932 sec was identified as an outlier.
Oddly, for this sequence, the correlation algorithm result shows no problem by visual check.
We will update the lidar messages in the bags and folders on the cloud drives soon. But please be mindful of this problem for now.

