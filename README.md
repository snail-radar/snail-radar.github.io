# Snail Radar Dataset

<!-- ![CI](https://github.com/rundocs/jekyll-rtd-theme/workflows/CI/badge.svg?branch=develop) -->
<!-- ![jsDelivr](https://data.jsdelivr.com/v1/package/gh/rundocs/jekyll-rtd-theme/badge) -->

4D radars are increasingly favored for odometry and mapping of autonomous systems due to their robustness in harsh weather and dynamic environments. Existing datasets, however, often cover limited areas and are typically captured using a single platform. To address this gap, we present a diverse large-scale dataset specifically designed for 4D radar-based localization and mapping. This dataset was gathered using three different platforms: a handheld device, an e-bike, and an SUV, under a variety of environmental conditions, including clear days, nighttime, and heavy rain. 

## Brief description

A dataset collected by 4D radars, stereo cameras, and lidars.
The preprint paper describing the dataset is at [arXiv](https://arxiv.org/abs/2407.11705).

```bibtex
@misc{huai2024snailradar,
  title={Snail-Radar: A large-scale diverse dataset for the evaluation of 4D-radar-based SLAM systems},
  author={Jianzhu Huai and Binliang Wang and Yuan Zhuang and Yiwen Chen and Qipeng Li and Yulong Han},
  year={2024},
  eprint={2407.11705},
  archivePrefix={arXiv},
  primaryClass={cs.RO},
  url={https://arxiv.org/abs/2407.11705},
}
```

## Quick start

**The dataset can be downloaded from either 
[OneDrive](https://1drv.ms/f/c/60208caf9367dbb1/ErHbZ5OvjCAggGAHDQAAAAABCBUW1vutI7GYt95u7EB-Mg)
or [Baidu Netdisk(百度网盘)](https://pan.baidu.com/s/1wLjt2fIn5EDescEgf3D7gQ) 提取码: 3141**.

We provided zipped rosbags and zipped data folders.

The 44 sequences of our dataset are repeatedly collected at 8 places with three platforms in diverse weather/lighting conditions. The place shorthands bc=basketball court, sl=starlake, ss=software school, if=info faculty, iaf=info and arts faculty, iaef=info, arts, and engineering faculty, st=starlake tower, 81r=August 1 road. The platforms H=handheld, E=ebike, S=SUV. The weather and lighting condition is clear and daytime unless specified. Different to other sequences of the info and arts faculty, the 20240113/2 sequence's route is anticlockwise.

| Place Setup |     | Date/Run        | Dist.(m)/Dur.(sec) | Weather/lighting   |
|-------------|-----|-----------------|--------------------|--------------------|
| **bc**      | H   | 20230920/1      | 84/74              | light rain, night  |
|             | H   | 20230921/2      | 59/83              | mod. rain          |
|             | E   | 20231007/4      | 78/51              |                    |
|             | E   | 20231105/6      | 251/144            | mod. rain          |
|             | E   | 20231105_aft/2  | 167/104            | light rain         |
| **sl**      | H   | 20230920/2      | 2182/1839          | light rain, night  |
|             | H   | 20230921/3      | 2171/1857          | mod. rain          |
|             | H   | 20230921/5      | 2015/1731          | mod. rain          |
|             | E   | 20231007/2      | 1997/657           |                    |
|             | E   | 20231019/1      | 1919/460           | night              |
|             | E   | 20231105/2      | 2045/524           | heavy rain         |
|             | E   | 20231105/3      | 2069/537           | heavy rain         |
|             | E   | 20231105_aft/4  | 2019/698           | light rain         |
|             | E   | 20231109/3      | 1983/546           |                    |
| **ss**      | H   | 20230921/4      | 736/622            | light rain         |
|             | E   | 20231019/2      | 781/533            | night              |
|             | E   | 20231105/4      | 895/395            | heavy rain         |
|             | E   | 20231105/5      | 967/400            | mod. rain          |
|             | E   | 20231105_aft/5  | 826/534            | light rain         |
|             | E   | 20231109/4      | 795/533            |                    |
| **if**      | S   | 20231208/4      | 2228/515           |                    |
|             | S   | 20231213/4      | 2227/494           | light rain, night  |
|             | S   | 20231213/5      | 2225/475           | light rain, night  |
|             | S   | 20240115/3      | 2223/525           | dusk               |
|             | S   | 20240116/5      | 2228/514           | dusk               |
|             | S   | 20240116_eve/5  | 2224/462           | night              |
|             | S   | 20240123/3      | 2231/535           |                    |
| **iaf**     | S   | 20231201/2      | 4620/1042          |                    |
|             | S   | 20231201/3      | 4631/946           |                    |
|             | S   | 20231208/5      | 4616/870           |                    |
|             | S   | 20231213/2      | 4603/938           | light rain, night  |
|             | S   | 20231213/3      | 4613/875           | light rain, night  |
|             | S   | 20240113/2      | 4610/1005          | anticlockwise      |
|             | S   | 20240113/3      | 4613/962           |                    |
|             | S   | 20240116_eve/4  | 4609/868           | night              |
| **iaef**    | S   | 20240113/5      | 7283/1509          |                    |
|             | S   | 20240115/2      | 6641/1374          |                    |
|             | S   | 20240116/4      | 6648/1515          |                    |
| **st**      | S   | 20231208/1      | 275/147            |                    |
|             | S   | 20231213/1      | 276/126            | light rain, night  |
|             | S   | 20240113/1      | 541/214            |                    |
| **81r**     | S   | 20240116/2      | 8554/1433          | light rain         |
|             | S   | 20240116_eve/3  | 8521/1293          | night              |
|             | S   | 20240123/2      | 8539/1743          |                    |



## Usage

**The source code to create the rosbags from the raw data and vice versa and the calibration data are available at [here](https://github.com/snail-radar/dataset_tools)**.

## Docs
The details about the benchmark are at [the docs](./docs/).


## Issues
Please post the issues at [the github repo issue tracker for this website source repo](https://github.com/snail-radar/snail-radar.github.io/issues).
We are working like cattle and horses to keep up with you.


## License

This SNAIL radar dataset is made available under the [Open Database License](./assets/license/opendatacommons.org_licenses_odbl_odbl-10.txt). Any rights in individual contents of the dataset are licensed under the [Database Contents License](./assets/license/opendatacommons.org_licenses_dbcl_dbcl-10.txt).
