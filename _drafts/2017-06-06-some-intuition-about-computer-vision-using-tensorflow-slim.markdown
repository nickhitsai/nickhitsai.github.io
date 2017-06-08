---
layout: post
title:  "Some intuition about Computer Vision using Tensorflow-Slim"
date:   2017-06-06 10:11:00 +0800
categories: Dev
---
我決定這篇還是先用中文寫，因為在自己尋找的過程中，深深感到中文資源非常的稀少，希望可以給中文讀者一點方向。

首先先介紹一個github repo，[tensorflow/models](https://github.com/tensorflow/models)，簡介就麻煩自己去看，我這邊要提的是裡面的[slim](https://github.com/tensorflow/models/tree/master/slim)和[inception](https://github.com/tensorflow/models/tree/master/inception)，[slim](https://github.com/tensorflow/models/tree/master/slim)是一個簡單版tensorflow的interface，而且點進去以後，在README中就有一個簡單的tutorial教你如何使用它已經寫好的code去train model，或是使用pre-trained model，以及如何evaluate你所train出來的model，非常的方便。

那現在的問題就是如何從我們手上的資料生出這些現有code可以吃的資料格式，因為是以Computer Vision為主，現有資料通常會是各式各樣的圖檔，大小可能也不一樣，這時候就需要[inception](https://github.com/tensorflow/models/tree/master/inception)，這裡面的[build_image_data.py](https://github.com/tensorflow/models/blob/master/inception/inception/data/build_image_data.py)，使用方式在檔案上方也有稍微說明，我就不再贅述。
