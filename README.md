# Caffe Simple Inferencer

## About this project

The Caffe Simple Inferencer is a deep learning framework used to deal with neural network
inference tasks. The major goal of this project is to provide a legible calculation tool
which can be configured easily. In order to achieve this goal, the main part of this
project uses no external library except the STL. In addition, the source data, the weight
data, the output data and even the intermediate results are all represented in a human
readable and edible way.

The main calculation part of this project is written in a C-like style, so that it can be
converted into a pure C program easily.

The file format of the nerual network information used by this program is the prototxt file
which is also used by caffe, and an folder of converted caffemodel files. These files are
in text format and the weight data of a single layer uses its unique file, so that you can
check and modify the weight data with ease. These converted caffemodel files can be converted
from a caffemodel file using the caffemodel converter offered in this project.

The input image file is also in text foramt. The image file can be generated by the image
converter offered by the project from a jpeg file. The image converter offers the subtract mean
function and would convert RGB image to BGR image which is default image mode for most caffemodels.
Yet it does not support rescale of the image, so before the conversion, you need to resize the
image file to the size that exactly required by the prototxt file.

## Environment and dependency

In order to compile the main part of this project, cmake, gcc and boost is needed.

In order to compile the caffemodel converter, Google Protobuf is needed.

In order to compile the image converter, libjpeg is needed.

For example, to run and to compile all parts of this project in a freshly installed ubuntu 18.04,
you may want to execute the following commends:

### sudo apt-get install build-essential, cmake, libboost-all-dev, libprotobuf-dev


## How to build

Each part of this project can all be build in the following way:

### cd [sub module path]
### mkdir build
### cd build
### cmake ../
### make


## How to use
Suppose you have a prototxt file and its corresponding caffemodel file, and an image file, and you
have successful compiled all sub-modules of this project.

First, convert the caffemodel file into a series of text files using caffemodel converter. You may
want to input:

./caffemodel_converter \--input [caffemodel_file] \--output [model_files_path]

Second, convert the jpeg file into the image file in text format using caffemodel converter. You
may want to input:

./image_converter \--input [jpeg_file] \--output [converted_image] \--mean [mean_values]

The converter would subscribe mean values. If your caffemodel is trained using the ilsvrc_2012 data
set, then this option can be omitted, for subscribe mean values of this data set has been stored in
 the program. Otherwise, you need input these values to get correct result. Mean value for different
channels separates by ",". For example, if you want to subscribe B by 111, G by 222, R by 11, you may
 want to add the option \--mean 111,222,11

Third, run the caffe_inference. You may want to input:

./caffe_inferencer \--prototxt [prototxt_file] \--model_dir [model_path] \--image [image_file] \--output [output_path]

You may also add -m option to output the intermediate results of the inference calculation.

## Currently supported layers
Currently this program supports batch normalization, convolution, element_wise, inner product, pooling,
relu, softmax and scale layers, making it possible to execute the Resnet_50 network. Additional layers
can be added simply by utilizing the map and reduce functions offered in the tensor.h.



