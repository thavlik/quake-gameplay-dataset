# Quake Gameplay Dataset
![Example Thumbnails](images/thumbnails.gif)

**UPDATE DEC 11, 2020: RAW VIDEOS POSTED, LOWER RESOLUTIONS ARE BEING CONVERTED**

This is a collection of Quake gameplay footage that has been preprocessed such that it is appropriate for use in as a deep learning dataset.

There are no class labels or ground truth; this dataset is primarily intended for unsupervised learning.

Custom maps and a few weapon/enemy mods made their way into dataset. Future efforts may be directed at "purifying" the data in ways such as omitting these custom weapons.

## Resolutions
| Resolution      | FPS | Size (GiB) | % Reduction | Download (.zip)
| --------------- | --- | ---------- | ----------- | --------
| 320x240         | 15  | -          | -           | TODO
| 640x480         | 15  | -          | -           | TODO
| Source*         | 30  | 233        | 0           | [Link](https://quake-gameplay-dataset.nyc3.digitaloceanspaces.com/raw.zip)

\* Most raw videos are at 1080p/720p but some are at lower resolutions

## S3 Hosting
The data can be downloaded with the [AWS Command Line Interface](https://aws.amazon.com/cli/) or compatible S3 API. Folders in the S3 bucket are named according to the resolution video they contain. Because the bucket contains all resolutions in both .mp4 and .zip format, syncing the entire bucket is highly redundant and discouraged. `s3 sync` is the recommended download method for slow or interruptible connections, as it can stopped and resumed without issue.

```bash
mkdir quake-gameplay-dataset
cd quake-gameplay-dataset

# The resolutions are available as both folders and zip files
# --no-sign-request allows use of awscli without credentials
aws s3 ls --endpoint https://nyc3.digitaloceanspaces.com --no-sign-request s3://quake-gameplay-dataset/

# Sync only the folder with the resolution you want
aws s3 sync --endpoint https://nyc3.digitaloceanspaces.com --no-sign-request s3://quake-gameplay-dataset/320x240 320x240
```

The hosting costs for this project are negligible, but an inconsiderately written download script could easily change this. I kindly ask that you be courteous w.r.t. redundant downloads, and cache locally where appropriate. If necessary, I will delist the .mp4 files from the bucket and only make the zip files available.

**If your goal is to copy the entire bucket for the purpose of hosting a duplicate copy for others to use, by all means download the entire bucket.**

## Compiling From Raw
The code for this project is maintained over in the [Doom Gameplay Dataset](https://github.com/thavlik/doom-gameplay-dataset) repository.

## Contributors
Gameplay videos are sourced from YouTube with permission. Special thanks to the following creators for their contributions to the community. They are good folk. 
- [Shambler/Team Shambler](https://www.youtube.com/user/FiendUK1)
- [dumptruck_ds](https://www.youtube.com/c/dumptruckds)
- [Spirit (Quaddicted)](https://quaddicted.com)
- [Daz (CustomGamer)](https://www.youtube.com/c/CustomGamer)
- [JCR 9001](https://www.youtube.com/c/JCR9001)
- [Greenwood](https://www.youtube.com/channel/UCMAKW4cqyo-7Xm_zHewDtTQ)
- [zigi](https://www.youtube.com/user/fibluzigi)

If you would like to contribute, please open an issue or submit a pull request with links to YouTube videos or playlists.

## License
All videos are property of their respective creators. Permission to transform and redistribute was granted in each case. This project makes no claims of ownership to the data.

This project's code is released under MIT / Apache 2.0 dual license, which is extremely permissive.

## Related Projects
- [Doom Gameplay Dataset](https://github.com/thavlik/doom-gameplay-dataset)
- [decord](https://github.com/dmlc/decord), for quickly loading frames
- [thavlik portfolio](https://github.com/thavlik/machine-learning-portfolio)
