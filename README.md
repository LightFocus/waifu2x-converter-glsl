# waifu2x-converter-glsl
================================================================================
# What is this?
Image Super-Resolution for Anime-style art using Deep Convolutional Neural Networks.

The original project (waifu2x) uses CUDA which requires a Nvidia GPU to make the best of it.

Due to the abandonment of Nvidia Cards on all new Macs, this project helps you to run waifu2x using Inter or AMD graphic cards on macOS.

# What did I do?

  - Write some instructions about how to build this project on macOS

Apparently, the original author has stopped maintaining this project and many people do not know how to build this project on macOS using Xcode.

# How to build this on macOS?
### Install dependencies

Make sure you have OpenCV and GLFW installed.

Install them using Homebrew

```sh
$ brew install opencv
$ brew install glfw
```

After the installation you can find them in 

```sh
/usr/local/Cellar
```

### Build setting in Xcode

Open the project in Xcode and go to Project Setting -> Choose 'Target' -> General -> Frameworks and Libararies

Make sure you have

- Cocoa.framework
- CoreFoundation.framework
- CoreGraphics.framework
- CoreVideo.framework
- IOKit.framework
- OpenGL.framework
- libglfw.x.x.dylib
- libopencv_core.x.x.x.dylib
- libopencv_imgcodecs.x.x.x.dylib
- libopencv_imgproc.x.x.x.dylib

added.

Note: You can find all .dylib files in

```sh
/usr/local/lib
```
simply drag and drop them to the Xcode.

### Copy OpenCV2 folder to your project

Go to 
```sh
/usr/local/Cellar/opencv/x.x.x/include/opencv*/
```
Copy the 'opencv2' folder to 

```sh
Yourprojectfolder/include/
```
### Build
In Xcode, press command+B to build this project.

Note: You can find the executable file on left side navigator -> Products, right click and choose 'Show in Finder'

# Dependencies

This executable file is NOT standalone, you must copy the 'models' and 'shaders' folders in the original project folder and put them in the same direaction as the executable file.


# Usage

##### The following contents are Google translated from the original author, please refer to https://github.com/ueshita/waifu2x-converter-glsl


This software is a command line tool. Start up the command prompt and use the following commands.

The following command outputs usage information to the screen.
```sh
./waifu2x-converter-glsl --help
```
The following commands are examples of commands that perform image conversion.
```sh
./waifu2x-converter-glsl -i mywaifu.png -m noise_scale -j 8 --scale_ratio 1.6 --noise_level 2
```
Executing the above will save the conversion result to mywaifu (noise_scale) (Level2) (x1.600000) .png.

#### In this software, the following options can be specified.

-i <string>, --input_file <string> (Required) Path to the image to convert (It is recommended to enter the full path)

-o, --output_file Path to the file to save the converted image (It is recommended to enter the full path.) Make sure to enter the extension (last .png etc.). If not specified, the file name is determined automatically and saved in that file. The rules for determining the file name are: [original image file name]  (mode name)  (noise removal level (in noise removal mode))  (enlargement ratio (in enlargement mode))  .png It is like this. The saved location is basically the same directory as the input image. (If the path to the input image is described as a relative path, unexpected things may occur.)

-m <noise | scale | noise_scale>, --mode <noise | scale | noise_scale> Specify the conversion mode. If not specified, noise_scale is selected. * noise: Noise removal (To be exact, image conversion is performed using a model for noise removal) * Scale: Enlargement (To be exact, after enlargement with existing algorithm, for enlargement image completion * Noise_scale: Noise removal and enlargement (After removing noise, enlargement is continued)

-b <integer value>, --block_size <integer value> Specify the reference block size for dividing the processing in the program. The number of threads specified by this option is started in the program. Increasing this number can make the process more efficient, but requires more graphics memory. The formula for calculating the required graphics memory size is as follows.
Required graphics memory = (block size) ^ 2 * 4 * 256 + α
An error will occur if it is impossible to process with the specified number. The default value is 512.

--scale_ratio <number with decimal point> Specify how many times to scale. The default value is 2.0, but you can specify a value other than 2.0. If a value other than 2.0 is specified, the following processing is performed. * First, repeat the 2x enlargement to cover the specified magnification sufficiently. * If a value other than a power of 2 is set, the enlarged image is reduced with a linear filter to the specified magnification.

--noise_level <1 | 2> Specify the noise removal level. Specify only 1 or 2 because the noise removal models are available only for level 1 and level 2. The default value is 1.

--model_dir <string> Specify the path to the directory where the model is stored. The default value is models. Basically, you don't have to specify it. Please specify when using your own model.

-, --ignore_rest Ignore all options after this option is done. For scripts and batch files.

--version Print version information and exit.

-h, --help Print a usage message and exit. Please when you want to check how to use easily.


