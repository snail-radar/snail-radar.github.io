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
