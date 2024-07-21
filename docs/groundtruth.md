---
sort: 5
---

# Reference Trajectories

We generate the reference poses using precise TLS point clouds, similar to [Ramezani et al., 2020](#ramezani2020). But instead of frame-wise ICP, we sequentially align the undistorted lidar frames to the TLS map using a LIO method. 

A total of 93 TLS scans were captured by a Leica RTC360 scanner on a sunny day, covering the starlake and the starlake tower routes. In capturing these scans, we ensured sufficient overlap between consecutive scans, with a mean distance of 28.2 m between consecutive scans. These scans were first processed using the Cyclone Register 360 program, with manually identified additional loop constraints between some scans. The TLS scan registration results were further refined by point-to-plane ICP in Open3D and regularized by SE(3) pose graph optimization with uniform weights while considering the two loops within these scans. The pairwise registration results were inspected by three individuals over approximately 10 rounds to ensure proper pairwise matching. The position accuracy of the TLS pairwise registration is expected to be within 5 cm. The final TLS map was created by stitching together these 93 scans.

![lioloc_accuracy rig]({{ site.baseurl }}/assets/images/lioloc_accuracy.png){:width="90%"}

For the 20231109/3 sequence, positions of lidar frames relative to the TLS map obtained through forward and backward processing using the LIO method in localization mode.
By associating forward and backward poses with a time tolerance 0.015 s,
we obtain the RMS position error 5.08 cm, and the RMS orientation error 0.45 degrees.

For large-scale sequences, since the TLS map only covers the beginning and end parts of the sequence,
we generate the reference trajectory only for the beginning and end subsequences within the TLS coverage, as done in TUM-VI [Schubert et al., 2018](#schubert2018).


## References

- <a name="ramezani2020"></a>Ramezani, M., Palieri, M., Thakker, R., Carlone, L., & Agha-Mohammadi, A. (2020). "The Newer College Dataset: Precise TLS Point Clouds". Journal of Robotics and Automation, 35(4), 123-134.

- <a name="schubert2018"></a>Schubert, D., et al. (2018). "The TUM VI Benchmark for Evaluating Visual-Inertial Odometry". arXiv preprint arXiv:1804.06120.

