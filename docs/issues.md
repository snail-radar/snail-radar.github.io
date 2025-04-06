---
sort: 7
---

# Tracking Issues

Please submit your issues to the [dataset_tools repository](https://github.com/snail-radar/dataset_tools/issues).

In the past, some issues were posted on the [source repository for this website](https://github.com/snail-radar/snail-radar.github.io/issues). Although these issues have been fixed and closed, they may serve as a useful reference.


# Known Issues

We have identified several issues in the dataset.

- To save storage space, the resolution of the ZED2i stereo images has been reduced to 640×360 in resolution since Dec 8 2023.
- In some sequences, the ZED2i images and IMU data have lower rates than the nominal values, likely due to low power voltage.
- The Hesai PandarXT-32 Point cloud timestamps should decrease by 0.05 sec to align with the other topics, e.g., X36D IMU. 
This is due to the fact that the KISS-ICP outputs motion at t + dt / 2 but stamps it with t and dt = 100 ms for PandarXT-32.
For sequence 20230920/data2, the point cloud timestamps should instead increase by 0.05 sec as its lidar time offset -0.07932 sec was identified as an outlier.
Oddly, for this sequence, the correlation algorithm result shows no problem by visual check.
We will update the lidar messages in the bags and folders on the cloud drives soon. But please be mindful of this problem for now.

# Changelog

- 2024-12-28:
    * Blur the faces and license plates with egoblur, 
    * add static transform tf files into each zipped sequence folder,
    * add metadata descriptions on the website.

- 2024-08-08: 
    * Publishes all sequences, the website, and the dataset paper.


# Roadmap

- [x] Sync all motion related messages
- [x] Calibrate all sensor extrinsic parameters
- [x] Recalibrate the ars548 radar extrinsics for the 20231105 morning sequences, and update the zipped folders
- [x] Fix the Hesai PandarXT-32 Point cloud timestamps by publishing the time corrections
- [ ] Update the Baidu Netdisk with the latest dataset on OneDrive
- [ ] Update swift_vio with learning-based feature matchers and recalibrate the image time offsets


# Lessons Learned in Creating the Dataset

- Double check every detail before setting out large-scale data collection.
- Moving objects cause trouble for lidar-based localization to TLS maps.
- Moving objects and the SUV hood cause trouble for visual inertial odometry.

