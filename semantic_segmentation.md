### Semantic segmentation

##### Traditional segmentation method
Partioning an image into parts (Normalized Cuts, Graph Cuts, Grab Cuts, superpixels, etc.), however, the algorithm has no actual understanding of what these parts represent.


##### Another method 
1. Partition the image into meaningful parts
2. While at the same time, associate every pixel in an input image with a class label. (사람, 차, 길, 버스 등)

##### Use case

ENet
The semantic segmentation architecture we’re using for this tutorial is ENet, which is based on Paszke et al.’s 2016 publication, [ENet: A Deep Neural Network Architecture for Real-Time Semantic Segmentation.](https://arxiv.org/abs/1606.02147)

- Fast, model size 3.2MB

[Semantic segmentation with OpenCV and deep learning - PyImageSearch](https://www.pyimagesearch.com/2018/09/03/semantic-segmentation-with-opencv-and-deep-learning/)

