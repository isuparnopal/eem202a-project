---
title:  Exploration
layout: template
filename: method_explore
--- 


## Table of Contents
* [Discontinued Approaches](#discontinued-approaches)
  * [Direct CNN Approach](#direct-cnn-approach)
  * [SyncNet-Inspired Approach](#syncNet-inspired-approach)


## Discontinued Approaches

### Direct CNN Approach

This was the first attempted approach towards solving the audio/video synchronization problem. This was also the one highlighted in the initial proposal. The audio and video were trained separately in two convolutional neural networks (CNNs).

<p align="center">
	<img src="https://github.com/binhanle/eem202a-project/blob/master/Images/strat1.png" />
	<br/>
	<strong>CNN Architecture</strong>
</p>

The reason why we did not pursue this approach is...

This approach can be found under:
"Name for Strategy 1 colab notebook"

### SyncNet-Inspired Approach
The third attemtped strategy was based on the SyncNet paper [7]. The authors were able to accomplish audio-video synchronization at an accuracy of 81% with a window size of only 5 frames. SyncNet consists of two similar DNNs that output size-256 vectors. The inputs are a five-frame window and the MFCC features of the corresponding audio segment. The L2 distance between the output vectors determines whether an audio and video pair is synchronized. SyncNet is trained on genuine (in-sync) and false (out-of-sync) pairs. To find the audio-video offset of a particular video, one must extract audio and video pairs from the video, feed them to SyncNet, average the L2 distances over a set time, and repeat by manually sliding the audio and/or the video stream. The offset that returns the least average L2 distance is most likely the correct one.

<p align="center">
	<img src="https://github.com/binhanle/eem202a-project/blob/master/Images/strat3.png"/>
	<br/>
	<strong>Source: https://www.robots.ox.ac.uk/~vgg/publications/2016/Chung16a/chung16a.pdf</strong>
</p>
	
This strategy was not pursued for the following reasons:

- We had inadequate resources. The GPU provided by Google Colab barely had enough memory for training audio and video pairs from one video. In contrast, the authors trained SyncNet on hundreds of hours of video using high-end hardware.
- Although the SyncNet architecture was implemented on Google Colab using the parameters described in the paper, the model overfit. Possible factors include not enough training data, an unforeseen bug in the pair generation code, and poor video quality.

This approach can be found under:
"Name for Strategy 3 colab notebook"