# Snail Radar Dataset

<!---This comments out sections of content.
![CI](https://github.com/rundocs/jekyll-rtd-theme/workflows/CI/badge.svg?branch=develop)
![jsDelivr](https://data.jsdelivr.com/v1/package/gh/rundocs/jekyll-rtd-theme/badge)
-->

A large scale dataset for benchmarking 4D radar-based odometry, mapping, and place recognition.

## Brief description

A dataset collected by 4D radars, stereo cameras, and lidars.
The preprint paper describing the dataset is at [arXiv](https://arxiv.org/abs/2407.11705).

```bibtex
@misc{huai2024snailradar,
  title={Snail-Radar: A large-scale diverse dataset for the evaluation of 4D-radar-based SLAM systems},
  author={Jianzhu Huai and Binliang Wang and Yuan Zhuang and Yiwen Chen and Qipeng Li and Yulong Han and Charles Toth},
  year={2024},
  eprint={2407.11705},
  archivePrefix={arXiv},
  primaryClass={cs.RO},
  url={https://arxiv.org/abs/2407.11705},
}
```

## Quick start

**The dataset can be downloaded from [OneDrive](https://1drv.ms/f/c/60208caf9367dbb1/ErHbZ5OvjCAggGAHDQAAAAABCBUW1vutI7GYt95u7EB-Mg)**.

We provided zipped rosbags and zipped data folders.

The list of data sequences are

|Sequence Date | Run | Weather |
|--- | --- | --- |
|20231101 | 2 | Clear day |
|20231101 | 3 | Light rain |
|20231101 | 4 | Clear day |


## Usage

**The source code to create the rosbags from the raw data and vice versa and the calibration data are available at [here](https://github.com/snail-radar/dataset_tools)**.

## Docs
The details about the benchmark are at [the docs](./docs/).
