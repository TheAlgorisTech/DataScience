
# Convolutional Neural Network
- Inspired by *multi-layer Perceptrons*
- Works best with unstructured data such as images, text, audio and speech
- Perform well whenever there is a topology associated with the data
- Impose local connectivity constraints between neurons of adjacent layers
- Process data through the convolution operation 
- Detect features based on filters learned by the CNN through training


## Linear Shift Invariant (LSI) Systems
System properties should satisfy the following constraints:
 - Scaling
 - Superposition
 - Time invariant

*When such systems work on time signals, they are referred to as linear time invariant (LTI) systems*

The computation of the response of the *LTI* system, requires the *response* of an *LSI* system corresponding to an impulse function. 
The impulse response of a system can ;
 - Be known
 - Be determined from the system by noting down its response to an impulse function

### Convolution Measures
*"Convolution measures the degree of overlap between one function and the reversed and translated version of another function"*

### Analog & Digital Signals

Any quantity of interest that shows variation in time &/or space represents a signal. So a signal is a function of time &/or space.

Example:
 - Stock Market Prices
 - Speech (Accoustic Signal)
 - Digital Image (RGB channels) signal is represented by a pixel intensity
 - Video is a squence of images witha temporal dimension


## 2D Convolution
Convolved images with the impulse response of an image-processing system can achieve;
 - Removing visible noise in the image throught noise-reduction filters
 - Detecting edges, to extract high-frequency components from an image

Image-Processing filters are;
 - Linear
 - Shift Invariant

*Based on the choice of image-processing filter, the nature of the output images will vary.*


### Image Processing Filters
- Different filters can detect different features from an image
- During Training process CNN learns the values of these filters
- Features extracted from the image depend on the number of filters

[//]: # (It doesn't matter which pixel location one chooses as the origin for the image signal while doing convolution.)

### Filters
1. __Mean Filter:__
 - Low-pass filter that computes the local average of the pixel intensities at any specific point
 - Impulse response is a square matrix
 - Reduce the noise in an image 
 - White noise of the zero mean will be suppressed

2. __Median Filter:__
 - Replaces each pixel in a neighborhoods with the median pixel intensity in that neighborhood based on the filter size 
 - Good for removing salt & pepper noise 
 - Salt & pepper nooise is presented as the form of black & white pixels (caused by sudden disturbances while capturing the images)

3. __Gaussian Filter:__
 - Impulse function are distributed normally around the origin
 - Weight is highest at the center of the filter
 - Reduce noise by suppressing the high-frequency components
 - May ends up producing a blurred image (Gaussian blur)
 - Substract blurred image from the original image to get the high-frequency component of the image  

4. __Gradiant-based Filter:__

5. __Sobel Edge-Detection Filter:__
 - Horizontal Sobel filter detects edges in the horizontal direction
 - Vertical Sobel filter detects edges in the vertical direction 
 - Both previous filter attenuate the low frequencies from the signals
 - Capture only the high-frequency components within the image
 - Edges are presented on the boundary between two regions in an image (first step in retrieving info from images)

__Supervised Learning:__ 
 - Filters are learned such a way that the overall cost function is reduced as much as possible
 - First convolution layer learns to detect edges
 - Second convolution layer learn to detect more complex shapes
 - Third layer and beyond learn much more complicated features based on the featues generated in the previous layers


### Convolution Neural Networks Architectures
*Layers combinations are stacked one after another*

__Input Layer:__
 - Input are images
 - Images are fed in batches as four dimensions
    1. Dimension One: Image index 
    2. Dimension Two & Three: Image height & width
    3. Dimension Four: Different channels (colored image channels are Red, Green and Blue)

__Convolutional Layer:__
 - Output feature maps are 2D convolved with 2D filters of the size specified
 - Deeper the convolutional layer in the network, more complex features and patterns are learned
 - Requires specifying the number and size of __filters__ that the layer must have
 - Under certain situations, it is recommended to add __padding__
 - Weights are initialized randomly, and are learned during the *CNN* training process

Similar to other layers, a convolutional layer will receive an input that transforms the input, then passes the transformed inputs to the next layer.
[//]: # (filters are what detect the patterns)

__Filters:__
 - Filter size is defined by width and height 
 - Filters help detect patterns,
    1. Multiple edges
    2. Shapes 
    3. Textures
    4. Objects etc...
 - Deeper the network, more sophisticated the filters are
 - Values in filters are initialized randomly
 - Filter convolves each pixel of width x height from input

__CONVOLVING__

![gif](https://img-blog.csdnimg.cn/20181129105210462.gif)

*The convolved image size is reduced, once the filter is applied over the original image, this occurs by convolving the image edges*
*Note:*
 - If image is n x n & filter is f x f then output size is (n-f+1) x (n-f+1)

*Issues:*
 - Image Size reduction may be a major problem, specially if significant data are available along the edges of the image
 - Image will shrink at each convolution operation, which may be problematic with a deeper convolutional layer ( contained output will get smaller and smaller)
 - Valuable data is being lost by discarding information at the periphery of the input since the filter does not analyze the edges of the input as much as inside parts of the input

__Padding:__
 - Convolved image by specific size filter, result smaller image than the original image
 - Padding adds zeros to the boundary of an image to control the size of the convolution output
 - Zero padding: 
   1. Adding border of pixels all with zeros value around input edges
   2. May require adding double, triple or more zero borders to maintain the original size of the input
 - Padding categories:
   1. Valid: no padding
   2. Same: padding to make output size same as input size


__Stride:__
 - Number of pixels to shift the filter as it is moved across the image

## Stride Equale 2

![gif](https://cdn-images-1.medium.com/max/1600/0*1PSMTM8Brk0hsJuF.)

__Pooling Layer:__
 - Added after a convolutional layer
 - Requires a __Filter__
 - Additional parameters such as __strides__ & __padding__ may be provided
 - Summarizes a locality of an image
 - Locality is given by the size of the filter kernel (receptive field)
 - Max-Pooling: (Similar to compression?)
   1. Maximum pixel intensity of a locality is taken as the repsentative of that locality (Check Gif Below)
   2. Reducing the resolution of a given output of a convolutional layer 
   3. Reducing the amount of parameters in the network
   4. Reducing computational load
   5. May help reducing overfitting

 - Average-Pooling: 
   1. Average pixel intensities around a locality is taken as the repsentative of that locality



## Max-Pooling Preserving Most Activated pixels

![gif](https://mlnotebook.github.io/img/CNN/poolfig.gif)

*Notes:*
 - Backpropagation through a convolution layer is much like propagation for multi-layer Perceptrons network
 - Only difference, weights connections are sparse since the same weights are shared by different input neighborhoods to create an output feature map
