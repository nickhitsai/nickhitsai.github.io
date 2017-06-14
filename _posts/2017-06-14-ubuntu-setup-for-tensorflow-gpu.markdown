---
layout: post
title:  "Ubuntu setup for Tensorflow-gpu"
date:   2017-06-14 21:00:00 +0800
categories: Dev
---
最近剛好建起一個Ubuntu環境，用來跑Tensorflow，紀錄一下順便讓有興趣的人可以參考看看。

那有鑒於[Tensorflow 官方tutorial](https://www.tensorflow.org/install/install_linux)實在是點點點，根本就是直接
{% highlight shell %}
pip install tensorflow-gpu
{% endhighlight %}
然後事情很像就結束了一樣，坦白說這個教學也等於沒有，到底哪個人會寫Python卻不會用pip install？

要打這行以前，其實事前作業還不少，以下簡單列一下


 - Ubuntu 14.04 以上
 - Nvidia Driver 與 CUDA版本7.5以上
 - [NVIDIA cuDNN](https://developer.nvidia.com/cudnn)


整個流程其實重點就在NVIDIA的各項軟體上，其中driver以及cuda我都是用下載來的.run檔安裝，而不是用以下這種apt-get指令來安裝
{% highlight shell %}
sudo apt-get install nvidia-304
{% endhighlight %}
原因很簡單，就算有去更新來源，apt-get的版本通常都不是最新的，再來是我覺得apt-get有時候套件控制的還蠻糟的

整個過程只要注意，安裝cuda的時候，他也會有一個預設的driver版本，如果懶惰就可以直接用cuda的.run檔安裝即可，它也會幫你把driver給裝上。如果有自行安裝其他版本的driver，在安裝cuda的時候要記得不要讓他覆蓋掉你自己安裝的版本。

安裝完畢以後，通常檢查driver我會用這指令
{% highlight shell %}
nvidia-smi
{% endhighlight %}
他會顯示你現在所使用的顯示卡資訊，最起碼你一定看得到型號，溫度等等。高級一點的可以看到有哪些process正在使用顯示卡的資源。

檢查cuda的話就是檢查安裝的資料夾有沒有東西，一般是在以下這個目錄
{% highlight shell %}
/usr/local/cuda/
{% endhighlight %}

接下來這個[NVIDIA cuDNN](https://developer.nvidia.com/cudnn)，這是一個NVIDIA用來加速deep learning的library，tensorflow-gpu在編譯的時候有去link到這個東西，<strong>這邊需要注意一下你所安裝的tensorflow-gpu版本是使用哪一個版本的cuDNN，因為你必須去下載相對應的版本</strong>。當然如果不知道，也可以就隨便挑一個，這樣可以安全地裝完tensorflow-gpu，只是在跑起來的時候會報錯，如果是版本問題就再換檔案就好。

以我現在使用的tensorflow-gpu版本是python2.7的1.1版，使用的是5.1版的libcudnn，我就得到NVIDIA網站註冊後下載。

下載後會得到一個tar檔，解壓縮以後會得到數個.so檔以及至少一個.h檔，將相對應的檔案放到cuda預設目錄下即可，一般來說就是以下兩個地方
{% highlight shell %}
/usr/local/cuda/lib64/
/usr/local/cuda/include/
{% endhighlight %}
那要換版本也很簡單，把剛才複製進去的東西砍了，把新版本的複製進去即可。

基本上到這邊就算完成前置作業，接下來就可以依照[Tensorflow 官方tutorial](https://www.tensorflow.org/install/install_linux)安裝。
