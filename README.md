![Example Thumbnails](images/thumbnails.gif)
# Quake Gameplay Dataset
[<img src="https://img.shields.io/badge/maintenance%20status-actively%20developed-brightgreen">](https://github.com/thavlik/quake-gameplay-dataset)
[<img src="https://img.shields.io/badge/License-Apache_2.0-orange.svg">](./LICENSE-Apache)
[<img src="https://img.shields.io/badge/License-MIT-lightblue.svg">](./LICENSE-MIT)
[<img src="https://img.shields.io/badge/Language-python-FFD43B.svg">](https://www.python.org/)

> **UPDATE DEC 15, 2020: ALL RESOLUTIONS RELEASED**

This is a collection of [Quake 1](https://en.wikipedia.org/wiki/Quake_(video_game)) gameplay footage that has been preprocessed such that it is appropriate for use as a deep learning dataset.

There are no class labels or ground truth; this dataset is primarily intended for unsupervised learning.

A few videos containing weapon/enemy mods made their way into dataset. Future efforts may be directed at "purifying" the data in ways such as omitting these custom weapons.

## Download Links
| Resolution      | FPS | Size (GiB) | % Reduction | Download (.zip)
| --------------- | --- | ---------- | ----------- | --------
| 320x240         | 15  | 29         | 88          | [Link](https://quake-gameplay-dataset.nyc3.digitaloceanspaces.com/320x240.zip)
| 640x480         | 15  | 87         | 63          | [Link](https://quake-gameplay-dataset.nyc3.digitaloceanspaces.com/640x480.zip)
| Source*         | 30  | 233        | 0 (raw)     | [Link](https://quake-gameplay-dataset.nyc3.digitaloceanspaces.com/raw.zip)

> \* Most raw videos are at 1080p/720p but some are at lower resolutions

## S3 Hosting
The data can be downloaded with the [AWS Command Line Interface](https://aws.amazon.com/cli/) or compatible S3 API. Folders in the S3 bucket are named according to the resolution video they contain. Because the bucket contains all resolutions in both .mp4 and .zip format, syncing the entire bucket is highly redundant and discouraged. `s3 sync` is the recommended download method for slow or interruptible connections, as it can stopped and resumed without issue.

```bash
$ mkdir quake-gameplay-dataset
$ cd quake-gameplay-dataset

# The resolutions are available as both folders and zip files
# --no-sign-request allows use of awscli without credentials
$ aws s3 ls \
    --endpoint https://nyc3.digitaloceanspaces.com \
    --no-sign-request \
    s3://quake-gameplay-dataset/

# Sync only the folder with the resolution you want
$ aws s3 sync \
    --endpoint https://nyc3.digitaloceanspaces.com \
    --no-sign-request \
    s3://quake-gameplay-dataset/320x240 \
    320x240
```

The hosting costs for this project are negligible, but an inconsiderately written download script could easily change this. I kindly ask that you be courteous with redundant downloads, and cache locally where appropriate. If necessary, I will delist the .mp4 files from the bucket and only make the zip files available.

**If your goal is to copy the entire bucket for the purpose of hosting a duplicate copy for others to use, by all means download the entire bucket.**


## How To Use
There are several existing Python solutions for loading frames from a directory of videos. [decord](https://github.com/dmlc/decord) is currently the most promising, given its narrowly tailored focus of machine learning. Generally, the API entails pointing the loader at a directory containing video files:
```python
import os
import torch
import decord
from decord import VideoLoader, cpu

# Configure decord to output torch.Tensor
# You can also do this for Tensorflow, etc...
decord.bridge.set_bridge('torch')

width = 320
height = 240
dir = f'/data/quake-gameplay-dataset/{width}x{height}'
video_files = [os.path.join(dir, f)
               for f in os.listdir(dir)
               if f.endswith('.mp4')]
num_frames = 1  # Likely (but not always) synonymous with batch_size
batch_shape = (num_frames, width, height, 3)
vl = VideoLoader(video_files,
                 ctx=[cpu(0)],
                 shape=batch_shape,
                 interval=0,
                 skip=0,
                 shuffle=1)
frame_data, indices = vl.next()
# `frame_data` contains the decoded frames
assert type(frame_data) == torch.Tensor
assert frame_data.shape == batch_shape
# `indices` is the (video_num, frame_num) for each frame
assert indices.shape == (num_frames, 2)
``` 

## Compiling From Raw
The code for this project is maintained over in the [Doom Gameplay Dataset](https://github.com/thavlik/doom-gameplay-dataset) repository. It's much simpler to maintain only one repository for the compiler code.

## Contributors
Gameplay videos are sourced from YouTube with permission. Special thanks to the following creators for their contributions to the community. They are good folk. 
- [Shambler/Team Shambler](https://www.youtube.com/user/FiendUK1)
- [dumptruck_ds](https://www.youtube.com/c/dumptruckds)
- [Spirit (Quaddicted)](https://quaddicted.com)
- [Daz (CustomGamer)](https://www.youtube.com/c/CustomGamer)
- [JCR 9001](https://www.youtube.com/c/JCR9001)
- [Greenwood](https://www.youtube.com/channel/UCMAKW4cqyo-7Xm_zHewDtTQ)
- [zigi](https://www.youtube.com/user/fibluzigi)

If you would like to contribute, please open an issue or submit a pull request with links to YouTube videos or playlists. The complete list of videos and playlists is [`raw/quake.txt`](raw/quake.txt).

## Donate
Over the years, hosting costs have amounted to hundreds of dollars. Crypto donations are greatly appreciated.

**BTC (Bitcoin):** 14uBA4iNCihkY1ukUdk4U5TWr9m57wCEQ8

**XMR (Monero):** 88N1srXmywTErgwp7V5RwqdbGwMpH4CH6KCws1nd1N8rBNxdzsQLDyaDoTgYKExLnvVcka2PiXR2EetiokVkzhwTQH3e5pW

**ADA (Cardano):** addr1q8c5xzhmx6a9gtvcf4mst86ntv9y4q7plgtge387yazgxwzlklp4lkgtzk6z2fwpaww3jqmczz0hltaxsc09zdxz7mcsucsqqk

**ETH (Ethereum):** 0x316f753d58D91640E5Cd3010F821e1CD464e2d3C

## License
All videos are property of their respective creators. Permission to transform and redistribute was granted in each case. This project makes no claims of ownership to the data.

This project's code is released under [MIT](LICENSE-MIT) / [Apache 2.0](LICENSE-Apache) 2.0 dual license, which is extremely permissive.

## Related Projects
- [Doom Gameplay Dataset](https://github.com/thavlik/doom-gameplay-dataset)
- [decord](https://github.com/dmlc/decord), for quickly loading frames
- [thavlik portfolio](https://github.com/thavlik/machine-learning-portfolio)
