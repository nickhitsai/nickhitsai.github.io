---
layout: post
title:  "Ubuntu setup for Tensorflow-gpu (English)"
date:   2017-06-14 22:00:00 +0800
categories: Dev
---
I have build up an Ubuntu for tensorflow-gpu. Just leave a record for myself and someone who is interested.

Because the [tutorial of Tensorflow](https://www.tensorflow.org/install/install_linux) is too awesome to understand, it did the same thing as the following command
{% highlight shell %}
pip install tensorflow-gpu
{% endhighlight %}
It is really stupid. Is there someone who can write Python and cannot use pip?

There are things that should be done before you type the above command.


 - Ubuntu 14.04 or newer
 - Nvidia Driver and CUDA 7.5 or newer
 - [NVIDIA cuDNN](https://developer.nvidia.com/cudnn)


All that matter is NVIDIA driver and cuda. I installed driver and cuda by using .run file downloaded from NVIDIA website. I would not use the following apt-get command to install.
{% highlight shell %}
sudo apt-get install nvidia-304
{% endhighlight %}
The reason is simple. Even if you keep update the source of apt-get, the version is always not the latest version. The other reason is that I feel that the software control by apt-get is awful. But it is really convenient.

There is just one place that need to pay attention. When start to install cuda, it contains a default driver. Of course that you can just install it. If you want to install the latest driver, you need to skip that step or it would replace the driver you have installed.

After installation, I would use the following command to check the driver status.
{% highlight shell %}
nvidia-smi
{% endhighlight %}
It would display the info about your graphic card. It would include your graphic card model and temperature at least. Some high level model would contain the process using the GPU resources.

For checking the cuda status, just check the following directory
{% highlight shell %}
/usr/local/cuda/
{% endhighlight %}

[NVIDIA cuDNN](https://developer.nvidia.com/cudnn) - This is a library for accelerate the computation of deep learning. Tensorflow-gpu uses it too. <string>You need to check the version of cuDNN that the version of tensorflow-gpu you used have linked. You must download that version.</strong> If you are not sure about that, you can just download any version of cuDNN. It would make you pass through all installation process. There would be an error when you execute program. You can change the version at that time.

At this time, the version of tensorflow-gpu I used is python2.7 rc1.1. It includes libcudnn version 5.1.

You need to download libcudnn from NVIDIA. After downloading, there is a tar file. Just decompress it and it contains header files(.h) and shared libraries(.so). Copy to the following path.
{% highlight shell %}
/usr/local/cuda/lib64/
/usr/local/cuda/include/
{% endhighlight %}
If you need to change the version, you can just delete the previous version and copy the new version into these directory.

We are done here. Then just follow the [tutorial of Tensorflow](https://www.tensorflow.org/install/install_linux).
