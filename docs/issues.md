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

- Residual time corrections [Done]: 
The residual time corrections are given at [here](https://1drv.ms/x/c/60208caf9367dbb1/EfLXlF7CeCFMmDkOpkA3Y0QBFnmtIpLucgg-exHN8Bi5hQ?e=j7zinw) with an accompanying readme copied below:

residual_td.csv contains the residual time offset corrections due to several bugs.
These bugs include the KISS-ICP timestamp, and the central Gaussian smoother.
Due to the KISS-ICP bug, the Hesai PandarXT-32 Point cloud timestamps should decrease by 0.05 sec to align with the other topics, e.g., X36D IMU. 
This is due to the fact that the KISS-ICP outputs motion at t + dt / 2 but stamps it with t and dt = 100 ms for PandarXT-32.
For sequence 20230920/data2, the point cloud timestamps should instead increase by 0.05 sec as its lidar time offset -0.07932 sec was identified as an outlier.
Oddly, for this sequence, the correlation algorithm result shows no problem by visual check.

Unlike time_corrections_set1 and set2.csv, these residual td are not applied to the sequence data yet.

**These corrections are to be applied to the sequence data (including both topics in rosbags and files in data folders)**.

Because the reference trajectories and the full trajectories are generated using the lidar timestamps before applying the residual td,
**for accurate benchmarking, we need to correct the reference trajectories and full trajectories timestamps by plus the residual td for /hesai/pandar given in residual_td.csv**

- The time offset estimates by swift_vio may not be reliable as it often produced divergent trajectories.

However, by comparing the time offsets estimated by using ORB-SLAM3 mono + zed2i IMU, and swift_vio for some sequences covering all three platforms, I found that their time offset estimates are pretty close.
The comparison table is at [here](https://1drv.ms/x/c/60208caf9367dbb1/EY5Ff1GmwJFNrx668dvzA_sBUpqhaVegH_BqPXxSlvgc-w?e=H6RzkV).


# Changelog

- 2025-4-6:
    * Provide the residual time offsets.
    * Publish the comparison of swift_vio and correlation of ORB-SLAM3 mono + zed2i IMU for time offset estimation.

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
- [x] Fix the Hesai PandarXT-32 Point cloud timestamps by publishing the time corrections.
- [ ] Update the Baidu Netdisk with the latest dataset on OneDrive
- [ ] Update swift_vio with learning-based feature matchers and recalibrate the image time offsets.


# Lessons Learned in Creating the Dataset

- Double check every detail before setting out large-scale data collection.
- Moving objects cause trouble for lidar-based localization to TLS maps.
- Moving objects and the SUV hood cause trouble for visual inertial odometry.

