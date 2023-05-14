# csprite-format-specs
Specifcation For .csprite File Format

---
## Specification

### About

the csprite file format is more like an "archive format", since csprite files are basically [`tar` archives or a `tarball`](https://en.wikipedia.org/wiki/Tar_(computing)), the tarball has a particular structure, this structure is how any encoder/decoder knows where to put files or read files from.

a csprite image is made up of 2 components, layers & frames. when multiple layers are put into a order a single frame is produced, optionally if multiple frames are put into order a animation is produced.

### Structure

the root of the tarball **must** have a `Info.ini` file, this file has all sorts of metadata about the file, like the resolution, number of frames, frame rate, image format, author, description, copyright information, license.

#### Frame structure

since a frame can have a single or multiple layers it is stored in a directory, the directory name follows the following convention: `F0` where `0` is to be replaced by the frame number you're referring to.

#### Layer structure

a single frame has single or multiple layers which **must** be ordered since that's how it will be ordered in the editor & when rendering the layers into 1 frame.

the name of the layer(s) follows the following convention: `0.LayerName` where `0` is to be replaced the index that layer is on, following with a separator `.` after which everything is treated as the name of that layer.

each layer consists of pixel data and storing the pixel data depends on the image format that is specified in the `Info.ini` file, for example if the image format is `image/png` then a png decoder is needed to decode that layer & read the pixel data.

the same is done when encoding, if your image format is `image/png` then you need a png encoder to encode the data & then store it.

### Conclusion

and that's how you store pixel art consisting of multiple frames that are made up of multiple layers.

the format may not be effiecient but it's very easy to read & write.

### Example Structure

```
/Info.ini

/F0/0.Background
/F0/1.Player
/F0/2.Car

/F1/0.Background
/F1/1.Player
/F1/2.Car

/F2/0.Background
/F2/1.Player
/F2/2.Car
```

---
### License

all the sample code is licensed under the [BSD 3-Clause "New" or "Revised"](./LICENSE) License.

---

# Thanks
