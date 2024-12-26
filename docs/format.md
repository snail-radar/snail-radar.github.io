---
sort: 3
---

# Data Format

We organize these sequences in cloud storage based on the day they were captured. If there are multiple sequences from different times of the day—such as morning, afternoon, or evening—on the same day, we differentiate the afternoon and evening sequences by appending a suffix to the group folder name. For example, the groups might be named 20231105 for the morning sequence and 20231105_aft or 20231105_eve for the afternoon and evening sequences, respectively.

For each sequence, a monolithic rosbag as well as a folder containing separate messages as individual files is provided on OneDrive.

## Folder Structure

The folder structure is described below with the example sequence 20240123/data3

- **data3/**: a sequence
  - **ars548/points/**: Continental ARS548 radar
    - `1706001762.429354169.pcd`: a point cloud frame in binary PCD
    - `...`: so on
    - `1706002295.000634410.pcd`
    - `times.txt`: times of these pcd files
  - **eagleg7/**: Oculli Eagle radar
    - **enhanced/**: enhanced point cloud frames by some proprietary aggregation technique
      - `1706001766.577286344.pcd`: a binary PCD point cloud frame
      - `...`
      - `1706002294.532391887.pcd`
      - `times.txt`
    - **pcl/**: point cloud frames
      - `1706001766.376780611.pcd`
      - `...`
      - `1706002294.370977741.pcd`
      - `times.txt`
    - **trk/**: point tracks
      - `1706001766.376839977.pcd`
      - `...`
      - `1706002294.371001344.pcd`
      - `times.txt`
  - `frame_ids.txt`: list of frame_id s of the sensor messages as in their headers.
  - **mti3dk/**: mti3dk IMU data
    - `imu.txt`: each line: time(sec), ax(m/s^2), ay(m/s^2), az(m/s^2), gx(rad/s), gy(rad/s), gz(rad/s), qx, qy, qz, qw
  - `tf_static.launch`: ROS1 launch file for static transforms between sensors
  - **x36d/**: x36d GNSS/INS module
    - `gnss_ins.txt`: each line: time(sec), lat(deg), lon(deg), ellipsoidal height(m), position_cov(0,0), position_cov(1,1), position_cov(2,2), status, service, position_cov_type.
    - `gnss.txt`: similar to gnss_ins.txt
    - `imu.txt`: each line: time(sec), ax(m/s^2), ay(m/s^2), az(m/s^2), gx(rad/s), gy(rad/s), gz(rad/s), qx, qy, qz, qw
  - **xt32/**": Hesai Pandar XT32 lidar
    - `1706001766.715735580.pcd`
    - `...`
    - `1706002294.616695580.pcd`
    - `times.txt`
  - **zed2i/**: Zed2i stereo camera
    - `imu.txt`: each line: time(sec), ax(m/s^2), ay(m/s^2), az(m/s^2), gx(rad/s), gy(rad/s), gz(rad/s), qx, qy, qz, qw
    - **left/**: left camera images
      - `1706001766.829899196.jpg`
      - `...`
      - `1706002294.627339486.jpg`
      - `times.txt`
    - `odom.txt`: Zed2i odometry data, each line time(sec), px (m), py (m), pz (m), qx, qy, qz, qw
    - **right/**: right camera images
      - `1706001766.829899196.jpg`
      - `...`
      - `1706002294.634015165.jpg`
      - `times.txt`


For the gnss_ins and gnss data, the status, service, position_cov_type follows the [ROS NavSatFix message definition](https://docs.ros.org/en/noetic/api/sensor_msgs/html/msg/NavSatFix.html).
The code we use for getting service and status values are given below
```python

def parseService(gps_glonass, galileo_beidou):
    service = 0
    if gps_glonass % 16 > 0:
        service += 1
    if gps_glonass / 16 > 0:
        service += 2
    if galileo_beidou % 16 > 0:
        service += 8
    if galileo_beidou / 16 > 0:
        service += 4
    return service


def parseSolutionStatus(pos_type):
    status = 0
    if 'INT' in pos_type or 'FIX' in pos_type:
        status = 0
    elif 'SBAS' in pos_type or 'WAAS' in pos_type:
        status = 1
    else:
        status = -1
    return status
```

## ROS1 Messages to Files in a Folder

The ROS1 themes and message types in the published rosbags, as well as the corresponding folders in the published zip files, are as follows:

| **Sensor**        | **Topic**                                            | **ROS message**     | **Folder**         | **Format** |
|-------------------|------------------------------------------------------|---------------------|--------------------|------------|
| Conti ARS548      | /ars548                                              | PointCloud2         | ars548/points      | pcd        |
| Hesai XT32        | /hesai/pandar                                        | PointCloud2         | xt32               | pcd        |
| MTi3DK IMU        | /mti3dk/imu                                          | Imu                 | mti3dk             | txt        |
| Oculii Eagle      | /radar_enhanced_pcl2                                 | PointCloud2         | eagleg7/enhanced   | pcd        |
|                   | /radar_pcl2                                          | PointCloud2         | eagleg7/pcl        | pcd        |
|                   | /radar_trk                                           | PointCloud          | eagleg7/trk        | pcd        |
| Bynav X36D        | /x36d/gnss                                           | NavSatFix           | x36d               | txt        |
|                   | /x36d/gnss_ins                                       | NavSatFix           | x36d               | txt        |
|                   | /x36d/imu_raw                                        | Imu                 | x36d               | txt        |
| ZED2i             | /zed2i/zed_node/imu/data                             | Imu                 | zed2i              | txt        |
|                   | /zed2i/zed_node/left_raw/image_raw_gray/compressed   | CompressedImage     | zed2i/left         | jpg        |
|                   | /zed2i/zed_node/right_raw/image_raw_gray/compressed  | CompressedImage     | zed2i/right        | jpg        |
|                   | /zed2i/zed_node/odom                                 | Odometry            | zed2i              | txt        |


## Sequence Attributes

We list the basic attributes of each sequence of our dataset in the below table.

<table>
    <thead>
        <tr>
            <th>Idx</th>
            <th>Sequence Path</th>
            <th>Start Unix Time</th>
            <th>End Unix Time</th>
            <th>Start Local Time</th>
            <th>End Local Time</th>
            <th>Weather Station Query Time</th>
            <th>Temperature (℃)</th>
            <th>Relative Humidity (%)</th>
            <th>Wind Speed (m/s)</th>
            <th>Hourly Precipitation (mm)</th>
            <th>Route</th>
            <th>Platform</th>
            <th>Traveled Distance (m)</th>
            <th>Duration (sec)</th>
            <th>Weather</th>
            <th>Lighting</th>
        </tr>
    </thead>
    <tbody>
        {% for row in site.data.general %}
        <tr>
            <td>{{ row["idx"] }}</td>
            <td>{{ row["seq path"] }}</td>
            <td>{{ row["start unix time"] }}</td>
            <td>{{ row["end unix time"] }}</td>
            <td>{{ row["start local time"] }}</td>
            <td>{{ row["end local time"] }}</td>
            <td>{{ row["weather station query time"] }}</td>
            <td>{{ row["temperature(℃)"] }}</td>
            <td>{{ row["relative humidity(%)"] }}</td>
            <td>{{ row["wind speed(m/s)"] }}</td>
            <td>{{ row["hourly precipitation (mm)"] }}</td>
            <td>{{ row["route"] }}</td>
            <td>{{ row["platform"] }}</td>
            <td>{{ row["traveled distance(m)"] }}</td>
            <td>{{ row["duration(sec)"] }}</td>
            <td>{{ row["weather"] }}</td>
            <td>{{ row["lighting"] }}</td>
        </tr>
        {% endfor %}
    </tbody>
</table>

## Field Descriptions of Key Sensor Messages

### ARS548

<table>
  <thead>
    <tr>
      <th>Topic</th>
      <th>Field</th>
      <th>Comment</th>
    </tr>
  </thead>
  <tbody>
    {% assign csv_data = site.data.ars548 %}
    {% for row in csv_data %}
    <tr>
      <td>{{ row.topic }}</td>
      <td>{{ row.field }}</td>
      <td>{{ row.comment }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>

### Hesai PandarXT-32

<table>
  <thead>
    <tr>
      <th>Topic</th>
      <th>Field</th>
      <th>Comment</th>
    </tr>
  </thead>
  <tbody>
    {% assign csv_data = site.data.hesai_pandar %}
    {% for row in csv_data %}
    <tr>
      <td>{{ row.topic }}</td>
      <td>{{ row.field }}</td>
      <td>{{ row.comment }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>

### Oculii Enhanced


<table>
  <thead>
    <tr>
      <th>Topic</th>
      <th>Field</th>
      <th>Comment</th>
    </tr>
  </thead>
  <tbody>
    {% assign csv_data = site.data.radar_enhanced_pcl2 %}
    {% for row in csv_data %}
    <tr>
      <td>{{ row.topic }}</td>
      <td>{{ row.field }}</td>
      <td>{{ row.comment }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>

### Oculii Tracks

<table>
  <thead>
    <tr>
      <th>Topic</th>
      <th>Field</th>
      <th>Comment</th>
    </tr>
  </thead>
  <tbody>
    {% assign csv_data = site.data.radar_trk %}
    {% for row in csv_data %}
    <tr>
      <td>{{ row.topic }}</td>
      <td>{{ row.field }}</td>
      <td>{{ row.comment }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>
