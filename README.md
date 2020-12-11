# Quake Gameplay Dataset
![Example Thumbnails](images/thumbnails.gif)

**UPDATE DEC 8, 2020: VIDEO LIST IS ASSEMBLED, PENDING COMPILATION**

This is a collection of Quake gameplay footage that has been preprocessed such that it is appropriate for use in as a deep learning dataset.

There are no class labels or ground truth; this dataset is primarily intended for unsupervised learning.

Custom maps and a few weapon/enemy mods made their way into dataset. Future efforts may be directed at "purifying" the data in ways such as omitting these custom weapons.

## Resolutions

| Resolution      | FPS | Size (GiB) | % Reduction | Download (.zip)
| --------------- | --- | ---------- | ----------- | --------
| 320x240         | 15  | -          | -           | TODO
| 640x480         | 15  | -          | -           | TODO
| Source*         | 30  | 233        | 0           | TODO

\* Most raw videos are at 1080p/720p but some are at lower resolutions

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
