---
sort: 3
---

# Data Format

For each sequence, a monolithic rosbag as well as a folder containing separate messages as individual files is provided on OneDrive.

The ROS1 themes and message types in the published rosbags, as well as the corresponding folders in the published zip files, are as follows:

| **Sensor**        | **Topic**                                            | **ROS message**     | **Folder**         | **Format** |
|-------------------|------------------------------------------------------|---------------------|--------------------|------------|
| Conti ARS548      | /ars548                                              | PointCloud2         | ars548/points      | pcd        |
| Hesai XT32        | /hesai/pandar                                        | PointCloud2         | xt32               | pcd        |
| MTi3DK IMU        | /mti3dk/imu                                          | Imu                 | mti3dk             | txt        |
| Oculii Eagle      | /radar_enhanced_pcl2                                 | PointCloud2         | eagleg7/enhanced   | pcd        |
|                   | /radar_pcl2                                          | PointCloud2         | eagleg7/pcl        | pcd        |
|                   | /radar_trk                                           | PointCloud          | eagleg7/trk        | bin        |
| Bynav X36D        | /x36d/gnss                                           | NavSatFix           | x36d               | txt        |
|                   | /x36d/gnss_ins                                       | NavSatFix           | x36d               | txt        |
|                   | /x36d/imu_raw                                        | Imu                 | x36d               | txt        |
| ZED2i             | /zed2i/zed_node/imu/data                             | Imu                 | zed2i              | txt        |
|                   | /zed2i/zed_node/left_raw/image_raw_gray/compressed   | CompressedImage     | zed2i/left         | jpg        |
|                   | /zed2i/zed_node/right_raw/image_raw_gray/compressed  | CompressedImage     | zed2i/right        | jpg        |
|                   | /zed2i/zed_node/odom                                 | Odometry            | zed2i              | txt        |

# Ground truth
We generate the reference poses using precise TLS point clouds, similar to [Ramezani et al., 2020](#ramezani2020). But instead of frame-wise ICP, we sequentially align the undistorted lidar frames to the TLS map using a LIO method. 

A total of 93 TLS scans were captured by a Leica RTC360 scanner on a sunny day, covering the starlake and the starlake tower routes. In capturing these scans, we ensured sufficient overlap between consecutive scans, with a mean distance of 28.2 m between consecutive scans. These scans were first processed using the Cyclone Register 360 program, with manually identified additional loop constraints between some scans. The TLS scan registration results were further refined by point-to-plane ICP in Open3D and regularized by SE(3) pose graph optimization with uniform weights while considering the two loops within these scans. The pairwise registration results were inspected by three individuals over approximately 10 rounds to ensure proper pairwise matching. The position accuracy of the TLS pairwise registration is expected to be within 5 cm. The final TLS map was created by stitching together these 93 scans.

![lioloc_accuracy rig]({{ site.baseurl }}/assets/images/lioloc_accuracy.jpg){:width="50%"}

For the 20231105/6 sequence, positions of lidar frames relative to the TLS map obtained through forward and backward processing using the LIO method in localization mode.

For large-scale sequences, since the TLS map only covers the beginning and end parts of the sequence,
we generate the reference trajectory only for the beginning and end subsequences within the TLS coverage, as done in TUM-VI [Schubert et al., 2018](#schubert2018).


## References

- <a name="ramezani2020"></a>Ramezani, M., Palieri, M., Thakker, R., Carlone, L., & Agha-Mohammadi, A. (2020). "The Newer College Dataset: Precise TLS Point Clouds". Journal of Robotics and Automation, 35(4), 123-134.

- <a name="schubert2018"></a>Schubert, D., et al. (2018). "The TUM VI Benchmark for Evaluating Visual-Inertial Odometry". arXiv preprint arXiv:1804.06120.



<!---
`inline code`

[`inline code inside link`](./)

```
:root {
  @for $level from 1 through 12 {
    @if $level % 4 == 0 {
      --toc-#{$level}: #{darken($theme-white, 4 * 8.8%)};
    } @else {
      --toc-#{$level}: #{darken($theme-white, $level % 4 * 8.8%)};
    }
  }
}
```

**Highlight:**

```scss
:root {
  @for $level from 1 through 12 {
    @if $level % 4 == 0 {
      --toc-#{$level}: #{darken($theme-white, 4 * 8.8%)};
    } @else {
      --toc-#{$level}: #{darken($theme-white, $level % 4 * 8.8%)};
    }
  }
}
```
--->
