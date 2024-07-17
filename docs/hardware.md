---
sort: 2
---

# Hardware Setup

Our dataset, dubbed snail-radar, is collected using three platforms, a handheld device, an e-bike, and an SUV. The three platforms share almost the same sensor rig as the data collection was carried out sequentially across these platforms.

The following are handheld, e-bike, and SUV data collection platforms respectively:

![handheld rig]({{ site.baseurl }}/assets/images/handheld-rig.png){:width="15%"}
![ebike rig]({{ site.baseurl }}/assets/images/ebike-rig.png){:width="34%"}
![suv rig]({{ site.baseurl }}/assets/images/suv-rig.png){:width="24%"}


# Sensor Setups
We assembled the sensors on a aluminum frame designed with CAD, ensuring it was waterproof.
The handheld rig consists of a Hesai Pandar XT32 lidar, an Oculii Eagle radar, a ZED2i stereo camera, and a Bynav X36D GNSS/INS system with a single antenna.
The rig mounted on the ebike or the SUV includes a Hesai Pandar XT32 lidar, a Continental ARS548 radar, an XSens MTi3DK IMU, an Oculii Eagle radar, a ZED2i stereo camera, and a Bynav X36D GNSS/INS system with dual antennas.
Specifically, sequences captured before Nov 1 2023 do not include data from the ARS548 radar and MTi-3DK IMU.
These sequences encompass all handheld sequences and some ebike sequences.

A ThinkPad P53 laptop running Ubuntu 20.04 with a 1TB solid-state drive is used for real-time data preprocessing and recording. 
The ARS548, Oculii, and XT32 are connected to the laptop by Ethernet cables, while the ZED2i and MTi3DK are connected via USB Type-C connectors.
The X36D connects to the computer through both a USB A connector and an RJ45 connector. 
The USB A connection (at COM1) is for receiving control commands, 
and the RJ45 connection is for sending INS solutions and raw data to the computer, as well as receiving RTCM messages relayed by the computer.
The X36D's PPS signals and GPGGA messages at COM1 are directly fed to the Hesai XT32 through a wired connection to its GPS port,ensuring that the lidar messages are synchronized to the GNSS time.

For the XT32, Eagle, MTi3DK, and ZED2i, data is captured as-is by their official ROS drivers.
The ARS548 and X36D UDP (User Datagram Protocol) packets are recorded on-site using the \texttt{tshark} utility.

During daytime data collection, the ZED2i's auto-exposure is enabled, usually adjusting the exposure time to less than 5 ms, often around 2 ms.
At dusk or night, auto-exposure is disabled, and the exposure time is locked at 5 ms to reduce motion blur.

All data collections start from an open area.
Every time the laptop and all sensors are powered up, we first ensure that the GNSS solution is fixed, then move the platform around to perform INS alignment until the INS solution converges.

The accelerometer noise and random walk are in units of m/s^2/√Hz and m/s^3/√Hz. The gyroscope noise and random walk are in units of rad/s/√Hz and rad/s^2/√Hz. FOV: field of view, BS: bias stability.

| **Type**           | **Sensor**         | **Rate** | **Characteristics**                                                                 |
|--------------------|--------------------|----------|--------------------------------------------------------------------------------------|
| 4D Radar           | Conti ARS548       | 15       | max range 300 m <br> Doppler [-400, 200] m/s <br> HFOV 120° VFOV 40° <br> range accuracy 0.3 m <br> az. accuracy 0.2° <br> elev. accuracy 0.1° <br> \#point/frame ~150 |
|                    | Oculii Eagle       | 15       | max range 400 m <br> Doppler ±86.8 m/s <br> HFOV 113° VFOV 45° <br> range accuracy 0.86 m <br> az. accuracy 0.44° <br> elev. accuracy 0.175° <br> \#point/frame ~7500 |
| GNSS/INS           | Bynav X36D         | 100      | real-time GNSS/INS <br> H 0.235 m RMS <br> V 0.14m RMS <br> in 10 s outage                                    |
| IMU                | ZED2i IMU          | 400      | accel. noise 1.6×10^-3, <br> random walk 2.5×10^-4; <br> gyro. noise 1.2×10^-4, <br> random walk 3.4×10^-5    |
|                    | MTi3DK             | 100      | roll/pitch 0.5° RMS <br> yaw 2° RMS <br> accel. noise 7×10^-4, <br> BS 4×10^-4 m/s²; <br> gyro. noise 5.236×10^-5, <br> BS 6°/hr |
|                    | X36D IMU           | 100      | accel. noise 5.833×10^-4, <br> BS 1.5×10^-4 m/s²; <br> gyro noise 2.91×10^-5, <br> BS 1.8°/hr             |
| Lidar              | Hesai Pandar XT32  | 10       | max range 120 m <br> range accuracy ±2 cm <br> FOV 360°×31° <br> \#point/frame ~90000                      |
| Stereo camera      | ZED2i              | 20       | 1280×720, grayscale, <br> HFOV 110°, VFOV 70°                                                        |



<!---
THIS IS TOO LONG, NEED UPDATE! HERE IS SOME IDEAS:

- https://primer.style/css/components/box
- https://primer.style/css/components/toasts

```note
## This is a note

Markdown is supported, Text can be **bold**, _italic_, or ~~strikethrough~~. [Links](https://github.com) should be blue with no underlines

`inline code`

[`inline code inside link`](./)
```

```note
This is note2
```

```note
This is note3
```

```tip
It’s bigger than a bread box.
```

```tip
It’s tip 2
```

```warning
Strong prose may provoke extreme mental exertion. Reader discretion is strongly advised.
```

```danger
Mad scientist at work!
```
--->
