---
date: "2019-08-16T20:14:59+08:00"
publishdate: "2019-08-16+08:00"
lastmod: "2019-08-16+08:00"
draft: false
title: "ONNX : convert trained pytorch model to tensorflow model"
tags: ["machine_learning", "blog", "pytorch", "tensorflow"]
series: ["my_machine_learning_journey"]
categories: ["Tools"]
img: "images/blog/series/my_machine_learning_journey/2019-08/cover1.jpg"
toc: true
summary: "This post shows how to convert model between two Neural Network Framework by using a fantastic tool ONNX"
---



In this post, I would like to share how to convert a trained Pytorch model to a Tensorflow model.



# ONNX

What is ONNX?

[ONNX(Open Neural Network Exchange)](<https://github.com/onnx/onnx>) is an open ecosystem that empowers AI developers to choose the right tools as their project evolves. Briefly speaking, it enables interoperability between different frameworks and streamlining the path from research to production helps increase the speed of innovation in the AI community. To achieves this, it defines an extensible computation graph model, as well as built in operators and standard data types.

![onnx](/images/blog/series/my_machine_learning_journey/2019-08/onnx.png)



We can think the Deep Learning as calculation over data flow graphs. The graphs are divided into two types: `Dynamic` and `Static` graphs. Different deep learning framework uses different kind of graphs. For instance, frameworks like Tensorflow, Caffe2, CNTK, Theano prefer to use static graph while others such as Pytorch, Chainer use dynamic graphs. 

Both of them have Pros and Cons. As for static graph, once the graph is defined it can be used multiple times as fast as possible cause we are not going to create anything new. Also, the static computation graph can be used to schedule computation across a pool of computational devices so computational cost could be shared. So, once defined we can use the optimization compiler to optimize the graph so that large graph can be run efficiently on either CPUs or GPUs. However, it is not flexible. And, because many logic errors will wait to be uncovered until execution, static graph has difficulty in debugging. As for dynamic graph, it is more flaxible, you can define, change and execute the network as you go. There is no such special `sessions` like we do in static graphs. It is more pythonic and easy to debug. However it is not that fast compared to static graph. So, it will be really great if we could develop the model using dynamic graph and deploy it using static graph. And, here he comes -- ONNX. 

In the rest of this blog, I will use an example to illustrate how to convert a pytorch model to a tensorflow model.

 